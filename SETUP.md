# T-Shirt Store Backend Setup Guide

## Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- Virtual environment (recommended)

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/Aryankaushik541/tshirt-store-backend.git
cd tshirt-store-backend
```

### 2. Create Virtual Environment

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Environment Configuration

Create a `.env` file in the root directory:

```env
SECRET_KEY=your-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
CORS_ALLOWED_ORIGINS=http://localhost:3000,http://localhost:5173
STRIPE_SECRET_KEY=your-stripe-secret-key
```

### 5. Database Setup

```bash
# Run migrations
python manage.py makemigrations
python manage.py migrate

# Create superuser for admin access
python manage.py createsuperuser
```

### 6. Load Sample Data (Optional)

Create sample categories and products through Django admin or shell:

```bash
python manage.py shell
```

```python
from products.models import Category, Product

# Create categories
casual = Category.objects.create(name="Casual", slug="casual", description="Casual wear t-shirts")
sports = Category.objects.create(name="Sports", slug="sports", description="Sports and athletic wear")
formal = Category.objects.create(name="Formal", slug="formal", description="Formal t-shirts")

# Create sample products
Product.objects.create(
    name="Classic White Tee",
    slug="classic-white-tee",
    description="Premium quality white t-shirt made from 100% cotton",
    price=29.99,
    category=casual,
    stock=50,
    available_sizes=["S", "M", "L", "XL"],
    colors=["white", "black", "gray"],
    featured=True
)

Product.objects.create(
    name="Sports Performance Tee",
    slug="sports-performance-tee",
    description="Moisture-wicking athletic t-shirt for peak performance",
    price=39.99,
    category=sports,
    stock=30,
    available_sizes=["M", "L", "XL"],
    colors=["blue", "red", "black"],
    featured=True
)
```

### 7. Run Development Server

```bash
python manage.py runserver
```

The API will be available at `http://localhost:8000`

### 8. Access Admin Panel

Navigate to `http://localhost:8000/admin` and login with your superuser credentials.

## API Endpoints

### Products
- `GET /api/products/` - List all products
- `GET /api/products/{slug}/` - Get product details
- `GET /api/products/featured/` - Get featured products
- `GET /api/products/categories/` - List categories

### Orders
- `POST /api/orders/` - Create new order
- `GET /api/orders/{id}/` - Get order details
- `GET /api/orders/{order_number}/track/` - Track order

## Testing the API

You can test the API using:

1. **Browser**: Navigate to the endpoints directly
2. **Postman**: Import the endpoints and test
3. **curl**: Command line testing

Example curl command:
```bash
curl http://localhost:8000/api/products/
```

## Troubleshooting

### Port Already in Use
```bash
python manage.py runserver 8001
```

### Database Issues
```bash
# Delete database and start fresh
rm db.sqlite3
python manage.py migrate
python manage.py createsuperuser
```

### Static Files Not Loading
```bash
python manage.py collectstatic
```

## Production Deployment

For production deployment:

1. Set `DEBUG=False` in settings
2. Configure proper database (PostgreSQL recommended)
3. Set up proper static file serving
4. Configure ALLOWED_HOSTS
5. Use environment variables for sensitive data
6. Set up HTTPS
7. Use a production WSGI server (gunicorn)

```bash
gunicorn tshirt_store.wsgi:application --bind 0.0.0.0:8000
```
