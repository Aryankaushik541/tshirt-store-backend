# T-Shirt Store Backend (Django REST API)

Django REST API backend for a T-shirt e-commerce store.

## Features

- Product catalog with categories
- Multiple product images
- Size and color variants
- Order management
- Admin panel
- RESTful API endpoints

## Setup

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Run migrations:
```bash
python manage.py makemigrations
python manage.py migrate
```

3. Create superuser:
```bash
python manage.py createsuperuser
```

4. Run server:
```bash
python manage.py runserver
```

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

## Environment Variables

Create a `.env` file:
```
SECRET_KEY=your-secret-key
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
CORS_ALLOWED_ORIGINS=http://localhost:3000
STRIPE_SECRET_KEY=your-stripe-key
```
