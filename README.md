# Crimora - Crime Management System

![Crimora Logo](https://via.placeholder.com/600x200/1e40af/ffffff?text=CRIMORA)

**Crimora** is a comprehensive web-based crime management platform designed for India. It enables real-time crime reporting, tracking, analysis, and provides interactive crime mapping with live news integration.

## 🚀 Features

### Core Functionalities
- **🔐 User Authentication**: JWT-based secure login/registration with role-based access
- **📋 Crime Reporting**: Interactive forms with image uploads and location mapping
- **🗺️ Live Crime Map**: Interactive Leaflet maps with crime hotspots and risk indicators
- **📰 Real-time News**: Live web scraping from 7+ major Indian news sources
- **📊 Dashboard Analytics**: Charts and statistics using Chart.js and Recharts
- **📚 IPC Code Reference**: Comprehensive Indian Penal Code database
- **👨‍💼 Admin Panel**: User management and crime case oversight

### User Roles
- **Citizens**: Crime reporting and awareness
- **Law Enforcement**: Case management and tracking
- **Administrators**: System oversight and analytics

## 🛠️ Tech Stack

### Frontend (React 19.1.1)
- **Framework**: React with functional components and hooks
- **Styling**: Tailwind CSS for responsive design
- **Animations**: Framer Motion for smooth transitions
- **Routing**: React Router DOM v7.7.1
- **Maps**: Leaflet with React-Leaflet for interactive mapping
- **Charts**: Chart.js, React-ChartJS-2, Recharts for data visualization
- **Icons**: Lucide React icon library
- **HTTP Client**: Axios for API communication

### Backend (Django 5.2.5)
- **Framework**: Django REST API architecture
- **Database**: MongoDB with PyMongo client (4 collections)
- **Authentication**: JWT tokens with bcrypt password hashing
- **Web Scraping**: Beautiful Soup 4 + Requests for live news
- **File Handling**: Django media files for image uploads
- **CORS**: Django-CORS-Headers for frontend integration

### Python Libraries Used
- **Django 5.2.5**: Web framework
- **PyMongo 4.11.3**: MongoDB driver
- **PyJWT 2.8.0**: JSON Web Token implementation
- **bcrypt 3.2.0**: Password hashing
- **Beautiful Soup 4.12.3**: Web scraping
- **requests 2.32.2**: HTTP library
- **python-dotenv 0.21.0**: Environment variable management
- **Pillow 10.3.0**: Image processing

## 📁 Project Structure

```
Crimora/
├── backend/
│   ├── crimora_backend/
│   │   ├── core/
│   │   │   ├── auth_views.py          # JWT authentication
│   │   │   ├── dashboard_views.py     # API endpoints
│   │   │   ├── live_scraper.py        # News scraping
│   │   │   ├── models.py              # Database models
│   │   │   ├── urls.py                # URL routing
│   │   │   └── utils/
│   │   │       └── db.py              # MongoDB connection
│   │   ├── crimora_backend/
│   │   │   ├── settings.py            # Django settings
│   │   │   └── urls.py                # Main URL config
│   │   └── manage.py                  # Django management
│   └── env/                           # Virtual environment
├── frontend/
│   ├── public/                        # Static assets
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.js              # Navigation component
│   │   │   ├── Login.js               # Authentication
│   │   │   └── CrimeCard.js           # Crime display
│   │   ├── pages/
│   │   │   ├── Home.js                # Landing page
│   │   │   ├── Dashboard.js           # Analytics dashboard
│   │   │   ├── CrimeMap.js            # Interactive map
│   │   │   ├── News.js                # Live crime news
│   │   │   └── ReportCrime.js         # Crime reporting
│   │   └── services/
│   │       └── api.js                 # API service layer
│   ├── package.json                   # Dependencies
│   └── tailwind.config.js             # Styling config
├── .gitignore                         # Git ignore rules
└── README.md                          # Project documentation
```

## 🚀 Installation & Setup

### Prerequisites
- Node.js (v16 or higher)
- Python 3.8+
- MongoDB Atlas account or local MongoDB
- Git

### Backend Setup

1. **Clone the repository**:
```bash
git clone https://github.com/yourusername/crimora.git
cd crimora
```

2. **Create virtual environment**:
```bash
cd backend
python -m venv env
# Windows
env\Scripts\activate
# Linux/Mac
source env/bin/activate
```

3. **Install dependencies**:
```bash
pip install django==5.2.5 pymongo==4.11.3 pyjwt==2.8.0 bcrypt==3.2.0 beautifulsoup4==4.12.3 requests==2.32.2 python-dotenv==0.21.0 pillow==10.3.0 django-cors-headers
```

4. **Environment variables**:
Create `.env` file in backend directory:
```env
MONGO_URI=mongodb://localhost:27017
MONGO_DB=crimora
JWT_SECRET_KEY=your-secret-key-here
DEBUG=True
```

5. **Run the server**:
```bash
cd crimora_backend
python manage.py runserver
```

### Frontend Setup

1. **Install dependencies**:
```bash
cd frontend
npm install
```

2. **Start development server**:
```bash
npm start
```

The application will be available at:
- Frontend: http://localhost:3000
- Backend API: http://localhost:8000

## 🌐 API Endpoints

### Authentication
- `POST /api/signup/` - User registration
- `POST /api/login/` - User login
- `GET /api/profile/` - Get user profile

### Crime Management
- `GET /api/crimes/` - Get crime reports
- `POST /api/crimes/` - Create crime report
- `GET /api/live-news/` - Get live crime news

### Dashboard
- `GET /api/dashboard/stats/` - Get crime statistics
- `GET /api/dashboard/charts/` - Get chart data

## 📊 Database Schema

### MongoDB Collections
1. **Users**: User authentication and profiles
2. **Crime Reports**: Crime incident data
3. **News**: Scraped crime news articles
4. **IPC Sections**: Indian Penal Code reference

## 🔧 Configuration

### News Sources
The system scrapes crime news from:
- NDTV
- Times of India
- Hindustan Times
- Indian Express
- News18
- Zee News
- ABP News

### Security Features
- JWT token-based authentication
- bcrypt password hashing
- CORS protection
- Input validation and sanitization
- Environment variable configuration

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Your Name**
- GitHub: [@patel-avinash](https://github.com/patel-avinash)
- LinkedIn: [Avinash J Patel]((https://www.linkedin.com/in/avinash-j-patel-0174a129b/))

## 🙏 Acknowledgments

- Django community for the excellent web framework
- React team for the powerful frontend library
- MongoDB for the flexible database solution
- All the open-source contributors

## 📞 Support

If you have any questions or need help, please open an issue in the GitHub repository.

---

**Made with ❤️ for safer communities in India**
