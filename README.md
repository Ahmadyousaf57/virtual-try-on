# 🛍️ Crowd Zero: E-Commerce with AR Virtual Try-On

An advanced, full-stack E-commerce platform that seamlessly integrates a PHP-based web storefront with a cutting-edge Python FastAPI backend to deliver Augmented Reality (AR) "Virtual Try-On" capabilities.

## 📁 Project Structure

This project is divided into distinct modular components:

*   **`a/` (Admin Panel):** A complete, dynamic PHP administration dashboard converted from static HTML. Features secure session management, login/logout (`Main.php`), product/category management, and activity logging.
*   **`e/` (Customer Storefront):** The main PHP-based e-commerce frontend. Includes user authentication (`login.php`, `signup.php`), a product catalog (`products.php`), shopping cart (`cart.php`), checkout workflow (`checkout.php`), and product detail pages.
*   **`d/` (Database):** Contains the core PostgreSQL/MySQL dump file (`crowd_zero.sql`) required to initialize the relational database tables for users, products, and transactions.
*   **`virtual-try-on/` (AR Backend):** A Python-based microservice utilizing FastAPI, OpenCV, and MediaPipe. This service detects facial landmarks and dynamically overlays 2D assets (like sunglasses, hats, or coats) onto user-uploaded photos.
*   **Scripts:**
    *   `generate_assets.py`: A utility script utilizing Pillow to generate default 2D placeholder product images (sunglasses, hats, coats) in the `virtual-try-on/frontend/assets/` directory.
    *   `verify_backend.py`: A test script to ensure the Python FastAPI try-on server is running correctly by querying the `/products` endpoint.

---

## ✨ Features

### 1. Augmented Reality (AR) Try-On Integration
*   Users can upload a photo of their face.
*   The Python backend detects 468 3D facial landmarks using `MediaPipe`.
*   The selected product (sunglasses, hats) is dynamically scaled, rotated, and overlaid onto the user's face using `OpenCV`.
*   Results are served seamlessly back to the PHP storefront.

### 2. Full-Fledged PHP Storefront
*   Secure User Registration and Authentication.
*   Dynamic product browsing, cart management, and checkout workflow.
*   Responsive, modern UI layout.

### 3. Secure Admin Dashboard
*   Session-based authentication (Default: `admin` / `admin123`).
*   Product inventory management (Add/Update/Delete).
*   Category and Order tracking interfaces.

---

## 🚀 Setup & Installation

### 1. Database Initialization
1.  Import the SQL dump located at `d/crowd_zero.sql` into your local database server (e.g., MySQL via phpMyAdmin).
2.  Update your PHP connection scripts (typically found in `e/config.php` and `a/AdminPanel_functions.php`) with your local database credentials.

### 2. Frontend & Admin Setup (PHP)
1.  Place the entire `eco1` directory into your local web server's document root (e.g., `htdocs` for XAMPP or `www` for WAMP).
2.  Start your Apache/Nginx and MySQL services.
3.  Access the storefront at: `http://localhost/eco1/e/index.php`
4.  Access the Admin Panel at: `http://localhost/eco1/a/Main.php`

### 3. Virtual Try-On Backend Setup (Python)
The AR try-on feature requires the Python microservice to be running.

```bash
# 1. Navigate to the virtual-try-on directory
cd virtual-try-on

# 2. Create and activate a Python virtual environment (recommended)
python3 -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`

# 3. Install dependencies
pip install -r requirements.txt

# 4. Generate default AR assets
cd ..
python3 generate_assets.py

# 5. Start the FastAPI server
cd virtual-try-on/backend
python3 app.py
```
*The AR backend will start on `http://0.0.0.0:8000`.*

### 4. Verify Backend Connection
You can verify the Python microservice is successfully running and communicating by executing the provided test script from the project root:
```bash
python3 verify_backend.py
```

---

## 🛠️ Technology Stack

*   **Frontend (Web):** HTML5, CSS3, JavaScript
*   **Backend (Web Store & Admin):** PHP 8+, MySQL/MariaDB
*   **Backend (AR Microservice):** Python 3.9+, FastAPI, Uvicorn
*   **Computer Vision:** OpenCV (`opencv-python`), Google MediaPipe
*   **Image Processing:** Pillow (PIL)

---

## 🔒 Security Notes
*   **Admin Panel:** Change the default admin credentials immediately before production deployment.
*   **Sessions:** Ensure PHP session security configurations are hardened.
*   **Data Validation:** Both the PHP and Python ends require strict input validation to prevent SQL Injection and malicious file uploads during the Try-On process.
