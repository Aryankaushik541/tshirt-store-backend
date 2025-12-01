# T-Shirt E-Commerce Store - Complete Project Overview

## 🎯 Project Description

A full-stack e-commerce platform for selling t-shirts, built with Django REST Framework backend and React frontend. Features include product catalog, shopping cart, checkout process, and order management.

## 🏗️ Architecture

### Backend (Django REST Framework)
- **Framework**: Django 4.2.7 with Django REST Framework
- **Database**: SQLite (development) / PostgreSQL (production ready)
- **API**: RESTful API with JSON responses
- **Authentication**: Ready for JWT/Token authentication
- **File Storage**: Local storage with Pillow for image handling

### Frontend (React + Vite)
- **Framework**: React 18 with Vite
- **Routing**: React Router v6
- **State Management**: Zustand for cart management
- **Styling**: Tailwind CSS
- **HTTP Client**: Axios
- **UI Components**: Custom components with Lucide icons

## 📦 Features

### Product Management
- ✅ Product catalog with categories
- ✅ Multiple product images support
- ✅ Size and color variants
- ✅ Stock management
- ✅ Featured products
- ✅ Search and filtering
- ✅ Product detail pages

### Shopping Experience
- ✅ Shopping cart with persistent storage
- ✅ Add/remove/update cart items
- ✅ Real-time cart updates
- ✅ Size and color selection
- ✅ Quantity management
- ✅ Order summary

### Checkout & Orders
- ✅ Customer information form
- ✅ Shipping address collection
- ✅ Order creation and tracking
- ✅ Order confirmation page
- ✅ Unique order numbers
- ✅ Order status management

### Admin Panel
- ✅ Django admin interface
- ✅ Product management
- ✅ Category management
- ✅ Order management
- ✅ Customer information

## 🗂️ Database Schema

### Products App

**Category Model**
- id (Primary Key)
- name
- slug (Unique)
- description
- created_at

**Product Model**
- id (Primary Key)
- name
- slug (Unique)
- description
- price (Decimal)
- category (Foreign Key)
- image (ImageField)
- stock (Integer)
- available_sizes (JSON)
- colors (JSON)
- featured (Boolean)
- created_at
- updated_at

**ProductImage Model**
- id (Primary Key)
- product (Foreign Key)
- image (ImageField)
- alt_text
- created_at

### Orders App

**Order Model**
- id (Primary Key)
- order_number (Unique)
- email
- first_name
- last_name
- phone
- address
- city
- state
- zip_code
- country
- total_amount (Decimal)
- status (Choice Field)
- payment_method
- payment_id
- notes
- created_at
- updated_at

**OrderItem Model**
- id (Primary Key)
- order (Foreign Key)
- product (Foreign Key)
- quantity
- size
- color
- price (Decimal)

## 🔌 API Endpoints

### Products
```
GET    /api/products/              # List all products
GET    /api/products/{slug}/       # Get product by slug
GET    /api/products/featured/     # Get featured products
GET    /api/products/categories/   # List categories
GET    /api/products/categories/{slug}/  # Get category by slug
```

### Orders
```
POST   /api/orders/                # Create new order
GET    /api/orders/{id}/           # Get order by ID
GET    /api/orders/{order_number}/track/  # Track order
```

## 🚀 Quick Start

### Backend Setup
```bash
cd tshirt-store-backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

### Frontend Setup
```bash
cd tshirt-store-frontend
npm install
cp .env.example .env
npm run dev
```

## 🔧 Technology Stack

### Backend
- Django 4.2.7
- Django REST Framework 3.14.0
- django-cors-headers 4.3.1
- Pillow 10.1.0
- python-decouple 3.8
- psycopg2-binary 2.9.9
- gunicorn 21.2.0
- whitenoise 6.6.0

### Frontend
- React 18.2.0
- Vite 5.0.8
- React Router 6.20.0
- Zustand 4.4.7
- Axios 1.6.2
- Tailwind CSS 3.3.6
- React Hot Toast 2.4.1
- Lucide React 0.294.0

## 📱 Pages & Routes

### Frontend Routes
- `/` - Home page with hero and featured products
- `/products` - Product listing with search and filters
- `/products/:slug` - Product detail page
- `/cart` - Shopping cart
- `/checkout` - Checkout form
- `/order-success/:orderNumber` - Order confirmation

## 🎨 UI/UX Features

- Responsive design (mobile, tablet, desktop)
- Modern and clean interface
- Smooth transitions and animations
- Toast notifications for user feedback
- Loading states
- Error handling
- Form validation
- Persistent cart storage

## 🔐 Security Features

- CORS configuration
- CSRF protection
- SQL injection prevention (Django ORM)
- XSS protection
- Environment variable management
- Secure password hashing

## 📈 Future Enhancements

### Planned Features
- [ ] User authentication and profiles
- [ ] Wishlist functionality
- [ ] Product reviews and ratings
- [ ] Payment gateway integration (Stripe)
- [ ] Email notifications
- [ ] Order tracking with status updates
- [ ] Admin dashboard analytics
- [ ] Inventory management
- [ ] Discount codes and promotions
- [ ] Multi-currency support
- [ ] Social media integration
- [ ] Product recommendations
- [ ] Advanced search with filters
- [ ] Image zoom and gallery

### Technical Improvements
- [ ] Unit and integration tests
- [ ] CI/CD pipeline
- [ ] Docker containerization
- [ ] Redis caching
- [ ] Elasticsearch for search
- [ ] CDN for static files
- [ ] Performance optimization
- [ ] SEO optimization
- [ ] PWA features
- [ ] Internationalization (i18n)

## 🧪 Testing

### Backend Testing
```bash
python manage.py test
```

### Frontend Testing
```bash
npm run test
```

## 📊 Performance Considerations

- Lazy loading for images
- Code splitting
- API pagination
- Database indexing
- Static file compression
- Browser caching
- Optimized queries

## 🌐 Deployment

### Backend Deployment Options
- Railway
- Heroku
- DigitalOcean
- AWS EC2
- Google Cloud Platform

### Frontend Deployment Options
- Vercel
- Netlify
- GitHub Pages
- AWS S3 + CloudFront

## 📝 License

This project is open source and available under the MIT License.

## 👥 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Support

For support, email support@teestore.com or open an issue in the repository.

## 🙏 Acknowledgments

- Django and DRF communities
- React and Vite teams
- Tailwind CSS
- All open-source contributors

---

**Repository Links:**
- Backend: https://github.com/Aryankaushik541/tshirt-store-backend
- Frontend: https://github.com/Aryankaushik541/tshirt-store-frontend
