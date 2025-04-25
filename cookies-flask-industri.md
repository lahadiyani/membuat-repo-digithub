Berikut adalah **cheatsheet** Markdown untuk membuat aplikasi Flask dengan **Application Factory Pattern** dan **MVC (Model-View-Controller)**.

---

# Flask Application Factory Pattern & MVC Cheatsheet

## Struktur Direktori

```
/flask_app
    /app
        /__init__.py
        /config.py
        /models.py
        /views.py
        /controllers.py
    /migrations
    /instance
    /templates
    /static
    /.env
    run.py
```

## 1. **File `run.py`**

```python
from app import create_app

# Membaca konfigurasi dari environment
app = create_app()

if __name__ == "__main__":
    app.run(debug=True)
```

## 2. **File `app/__init__.py`**

```python
from flask import Flask
from .config import Config
from .models import db
from .controllers import main_controller

def create_app():
    app = Flask(__name__, instance_relative_config=True)

    # Mengonfigurasi aplikasi dari file .env
    app.config.from_object(Config)

    # Inisialisasi database
    db.init_app(app)

    # Daftarkan blueprint dari controllers (MVC)
    app.register_blueprint(main_controller)

    return app
```

## 3. **File `app/config.py`**

```python
import os
from dotenv import load_dotenv

# Muat variabel dari .env
load_dotenv()

class Config:
    SECRET_KEY = os.getenv('SECRET_KEY', 'defaultsecretkey')
    SQLALCHEMY_DATABASE_URI = os.getenv('DATABASE_URL', 'sqlite:///site.db')
    SQLALCHEMY_TRACK_MODIFICATIONS = False
    COOKIE_SECURE = os.getenv('COOKIE_SECURE', 'False').lower() == 'true'
    COOKIE_MAX_AGE = int(os.getenv('COOKIE_MAX_AGE', 86400))  # Default 1 hari
```

## 4. **File `app/models.py`**

```python
from flask_sqlalchemy import SQLAlchemy

# Inisialisasi database
db = SQLAlchemy()

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(100), nullable=False)

    def __repr__(self):
        return f"User('{self.username}')"
```

## 5. **File `app/views.py`**

```python
from flask import render_template

def login_view():
    return render_template('login.html')

def dashboard_view(user):
    return render_template('dashboard.html', user=user)
```

## 6. **File `app/controllers.py`**

```python
from flask import Blueprint, request, redirect, url_for, make_response
from .models import User, db
from .views import login_view, dashboard_view
import os

# Membuat Blueprint untuk main controller
main_controller = Blueprint('main', __name__)

@main_controller.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form['username']
        
        # Simpan username ke dalam cookie
        resp = make_response(redirect(url_for('main.dashboard')))
        
        resp.set_cookie('username', username, httponly=True, secure=os.getenv('COOKIE_SECURE', 'False').lower() == 'true', max_age=int(os.getenv('COOKIE_MAX_AGE', 86400)), samesite='Strict')
        
        return resp

    return login_view()

@main_controller.route('/dashboard')
def dashboard():
    # Ambil username dari cookie
    username = request.cookies.get('username', 'Guest')

    # Cari user di database
    user = User.query.filter_by(username=username).first()

    return dashboard_view(user)
```

## 7. **File `templates/login.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
</head>
<body>
    <form action="/login" method="POST">
        <input type="text" name="username" placeholder="Enter username" required>
        <button type="submit">Login</button>
    </form>
</body>
</html>
```

## 8. **File `templates/dashboard.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dashboard</title>
</head>
<body>
    <h1>Welcome, {{ user.username }}!</h1>
</body>
</html>
```

## 9. **File `.env`**

```
FLASK_APP=run.py
FLASK_ENV=development
SECRET_KEY=supersecretkey
DATABASE_URL=sqlite:///site.db
COOKIE_SECURE=False
COOKIE_MAX_AGE=86400
```

## 10. **Menjalankan Aplikasi**

Setelah semua file selesai, jalankan aplikasi dengan perintah berikut:

```bash
python run.py
```

---

### **Penjelasan**

- **Application Factory Pattern**: Menggunakan `create_app()` untuk memisahkan pembuatan aplikasi dan konfigurasi, memungkinkan fleksibilitas di lingkungan yang berbeda.
- **MVC Pattern**: Aplikasi dibagi menjadi tiga bagian:
  - **Model** (di `models.py`): Menangani struktur data dan logika database.
  - **View** (di `views.py`): Merender tampilan halaman HTML.
  - **Controller** (di `controllers.py`): Menangani logika aplikasi dan request.
- **File `.env`**: Digunakan untuk menyimpan variabel konfigurasi dan rahasia aplikasi seperti `SECRET_KEY`, `DATABASE_URL`, dan pengaturan cookie.
  
Dengan struktur ini, aplikasi menjadi lebih modular dan mudah dipelihara karena tanggung jawab antara model, tampilan, dan kontroler terpisah dengan jelas.
