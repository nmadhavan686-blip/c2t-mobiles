# C2T MOBILES - Second-Hand Smartphone E-Commerce Platform

**C2T MOBILES** is a complete, modern, production-ready second-hand / refurbished smartphone e-commerce web application.

> **Core Business Model**:
> C2T MOBILES sells pre-owned smartphones through direct WhatsApp communication. There is **NO** direct online purchase, cart checkout, or payment gateway on the website.
> Clicking **"BUY ON WHATSAPP"** logs the inquiry analytics and immediately opens WhatsApp with a pre-filled, product-specific message containing device name, storage, colour, battery health %, condition, price, and product ID.

---

## 🌟 Key Features

### Customer Features:
- **Premium Dark + Light Identity**: Modern dark header and accents combined with crisp, high-contrast product cards and clean typography.
- **Direct WhatsApp Commerce**: Every product features a prominent "Buy on WhatsApp" CTA.
- **Mobile-First Responsive Layout**: Includes sticky bottom navigation bar (Home, Mobiles, Search, WhatsApp), mobile drawer menu, and floating WhatsApp CTA.
- **Comprehensive Product Details**: 15-point "Phone Condition Details" inspection matrix (Display, Body, Camera, Battery, Speaker, Mic, Charging Port, Face ID, Network, Repairs).
- **Dynamic Image Gallery**: Multi-photo switcher with lightbox view and zoom.
- **Real-time Search & Multi-Filter**: Filter by Brand (Apple, Samsung, OnePlus, Pixel, etc.), Price Range, Condition Grade, Storage, and Availability.
- **Indian Rupee Formatting**: Prices rendered as `₹32,999` with proper Indian digit grouping.

### Admin Panel (`/admin`):
- **Secured Authentication**: Protected dashboard routes with session cookies and bcrypt password hashing.
- **Store Overview KPIs**: Track total inventory, available devices, sold-out items, and total WhatsApp enquiries.
- **Full Inventory Stock Management**: Add, Edit, Delete devices with 15-point condition matrix inputs.
- **Multi-Image Management**: Drag/upload multiple device photos with automatic compression and optimization.
- **Sold Status Toggle**: Switch status between `AVAILABLE` and `SOLD` with custom product badges (`HOT DEAL`, `FEATURED`, `SALE`, `SOLD OUT`).
- **Configurable WhatsApp Settings**: Update `OWNER_WHATSAPP_NUMBER` dynamically from backend settings.

---

## 🛠️ Technology Stack

- **Frontend**: Semantic HTML5, CSS3 (CSS Variables, Flexbox, Grid), Vanilla JavaScript (ES6+ Modules).
- **Backend**: Python 3.14 / 3.x with Flask REST API architecture.
- **Database**: SQLite (SQL schema designed for seamless migration to MySQL/PostgreSQL).
- **Security**: Werkzeug password hashing, session management, file upload type validation.
- **Image Processing**: Pillow (PIL) for image thumbnailing and optimization.

---

## 🚀 Quick Setup & Local Execution

### 1. Prerequisites
Ensure Python 3.9+ is installed on your system.

### 2. Create Virtual Environment & Install Dependencies
Open terminal/cmd in the project root:

```bash
# Create virtual environment
py -m venv venv

# Activate virtual environment
# On Windows PowerShell:
.\venv\Scripts\Activate.ps1
# On CMD:
.\venv\Scripts\activate.bat

# Install required Python packages
pip install -r requirements.txt
```

### 3. Environment Configuration
Copy `.env.example` to `.env`:

```bash
cp .env.example .env
```

Ensure `.env` contains your desired settings:

```env
SECRET_KEY=c2t_mobiles_secret_key_change_in_production_2026
DATABASE_URL=sqlite:///database/c2t_mobiles.db
OWNER_WHATSAPP_NUMBER=919994645492
ADMIN_USERNAME=admin
ADMIN_PASSWORD=admin123
BUSINESS_EMAIL=contact@c2tmobiles.com
BUSINESS_NAME=C2T MOBILES
PORT=5000
```

### 4. Seed Database with Sample Stock
Run the database seed script to generate tables and populate sample smartphones (iPhone 13, iPhone 14, Galaxy S23 Ultra, OnePlus 12, Google Pixel 8, etc.):

```bash
python -m backend.seed
```

### 5. Run the Server
Start the Flask application:

```bash
python -m backend.app
```

The application will start at:
- **Customer Web Application**: `http://127.0.0.1:5000`
- **Owner Admin Portal**: `http://127.0.0.1:5000/admin/login.html`

**Default Admin Credentials**:
- **Username**: `admin`
- **Password**: `admin123`

---

## 📂 Project Directory Structure

```text
c2t-mobiles/
├── backend/
│   ├── app.py                  # Main Flask application entrypoint & static route handler
│   ├── config.py               # Application configuration manager
│   ├── database.py             # SQLite connection & schema initialization
│   ├── seed.py                 # Seed script for initial sample smartphone stock
│   ├── routes/
│   │   ├── api_public.py       # REST API endpoints for catalog, detail, search & enquiries
│   │   └── api_admin.py        # Protected REST API endpoints for admin inventory CRUD & settings
│   └── utils/
│       ├── auth.py             # Password hashing & session auth decorators
│       └── helpers.py          # WhatsApp message generator, INR formatting & image optimizer
├── frontend/
│   ├── index.html              # Homepage
│   ├── products.html           # Mobiles catalog page with filter sidebar & search bar
│   ├── product.html            # Product detail view with gallery & condition matrix
│   ├── about.html              # About Us page
│   ├── contact.html            # Contact Us page
│   ├── faq.html                # FAQ page with educational buyer guide
│   ├── privacy.html            # Privacy Policy
│   ├── terms.html              # Terms & Conditions
│   ├── sitemap.xml             # Search engine XML sitemap
│   ├── robots.txt              # Search engine directives
│   ├── css/
│   │   ├── style.css           # C2T MOBILES design system stylesheet
│   │   └── responsive.css      # Mobile drawer & mobile bottom nav stylesheet
│   ├── js/
│   │   ├── api.js              # REST API wrapper client
│   │   ├── app.js              # Core UI, drawer & WhatsApp link builder
│   │   ├── products.js         # Catalog filtering, search & grid renderer
│   │   └── product.js          # Detail view, gallery switcher & condition inspector
│   └── admin/
│       ├── login.html          # Secure Admin Login screen
│       ├── dashboard.html      # Overview KPI statistics & enquiry tracking
│       ├── products.html       # Inventory table with status toggle & delete modal
│       ├── add-product.html    # Add mobile stock form with 15-point condition matrix
│       ├── edit-product.html   # Edit mobile stock & image manager
│       ├── settings.html       # WhatsApp & site configuration
│       ├── css/
│       │   └── admin.css       # Admin dashboard styles
│       └── js/
│           ├── admin-auth.js   # Admin session authentication guard
│           ├── admin-dashboard.js
│           ├── admin-products.js
│           └── admin-form.js
├── database/
│   ├── schema.sql              # SQL table schema definitions & performance indexes
│   └── c2t_mobiles.db          # SQLite database instance
├── uploads/
│   └── products/               # Optimized mobile stock photos directory
├── .env.example                # Sample environment variables
├── requirements.txt            # Python dependencies
└── README.md                   # Full documentation
```

---

## 🔒 Production Deployment Notes

1. **Production WSGI Server**:
   Use `gunicorn` or `waitress` instead of the development server:
   ```bash
   pip install gunicorn
   gunicorn backend.app:app -w 4 -b 0.0.0.0:5000
   ```

2. **Reverse Proxy & SSL**:
   Run behind Nginx or Cloudflare with HTTPS enabled for security.

3. **Database Migration to PostgreSQL/MySQL**:
   Replace `sqlite3` driver in `backend/database.py` with `psycopg2` or `pymysql` when scaling to multi-server environments.
