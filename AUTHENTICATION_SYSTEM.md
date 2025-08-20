# Crimora - Complete Authentication & Dashboard System

## Overview

The Crimora system has been enhanced with a complete authentication system using MongoDB and JWT tokens. The system now supports user registration, login, and role-based access control with separate dashboards for users and administrators.

## Features

### Authentication System
- **User Registration** - Users can create accounts with email and password
- **User Login** - Secure login with JWT token generation
- **Role-based Access** - Separate access levels for users and administrators
- **Password Security** - Passwords are hashed using bcrypt
- **Token Management** - JWT tokens for session management

### User Dashboard
- **Case Status Overview** - View status of reported crimes (pending, in progress, solved, closed)
- **Personal Crime Reports** - Users can only see their own reported cases
- **Navigation Menu** - Access to Home, Map, Report Crime, IPC, News, and Dashboard
- **Case Statistics** - Visual representation of case counts by status

### Admin Dashboard
- **System Statistics** - Total cases, users, solved percentage
- **Case Management** - View and manage all cases in the system
- **Status & Priority Control** - Update case status and priority levels
- **High Priority Cases** - Quick access to urgent cases
- **User Management** - Overview of total system users
- **Data Visualization** - Charts showing case distribution

### Security Features
- **JWT Authentication** - Secure token-based authentication
- **Password Hashing** - bcrypt for secure password storage
- **Protected Routes** - API endpoints require authentication
- **Role Verification** - Admin-only endpoints with role checking

## API Endpoints

### Authentication Endpoints
```
POST /auth/signup/          - User registration
POST /auth/login/           - User login
GET  /auth/profile/         - Get user profile (requires token)
```

### Dashboard Endpoints
```
GET  /dashboard/user/              - User dashboard data (user only)
GET  /dashboard/admin/             - Admin dashboard data (admin only)
POST /dashboard/admin/update-case/ - Update case status/priority (admin only)
```

### Crime Endpoints (Protected)
```
GET  /crimes/               - Get crimes (filtered by user role)
POST /crimes/               - Report new crime (requires authentication)
```

### Other Protected Endpoints
```
GET  /ipc/                  - Get IPC sections (requires authentication)
GET  /ipc/<id>/             - Get IPC section detail (requires authentication)
GET  /news/                 - Get news (requires authentication)
POST /news/                 - Add news (admin only)
```

## Database Structure

### Users Collection
```javascript
{
    "_id": ObjectId,
    "name": "User Name",
    "email": "user@example.com",
    "password": "hashed_password",
    "phone": "1234567890",
    "role": "user" | "admin",
    "created_at": Date,
    "is_active": true
}
```

### Crime Reports Collection (Enhanced)
```javascript
{
    "_id": ObjectId,
    "reporterEmail": "user@example.com",
    "reporterName": "User Name",
    "crimeType": "Theft",
    "location": "Location details",
    "description": "Crime description",
    "status": "pending" | "in_progress" | "solved" | "closed",
    "priority": "low" | "medium" | "high",
    "created_at": Date,
    "updated_at": Date,
    "updated_by": "admin@example.com",
    // ... other crime details
}
```

### News Collection
```javascript
{
    "_id": ObjectId,
    "title": "News Title",
    "content": "News content",
    "category": "announcement" | "statistics" | "safety",
    "created_at": Date,
    "created_by": "admin@example.com"
}
```

## Default Admin Account

A default admin account is automatically created:
- **Email**: `admin@crimora.com`
- **Password**: `admin123`
- **Role**: `admin`

## Frontend Integration

### React Context Setup
The system includes a React Context (`AuthContext`) for managing authentication state across components.

### Key Components
- **AuthProvider** - Context provider for authentication
- **LoginForm** - User login interface
- **UserDashboard** - User-specific dashboard
- **AdminDashboard** - Administrator dashboard

### API Service Classes
- **AuthService** - Authentication operations
- **DashboardService** - Dashboard data operations
- **CrimeService** - Crime-related operations
- **NewsService** - News management operations

## Installation & Setup

### Backend Setup

1. **Install Dependencies**
   ```bash
   pip install bcrypt PyJWT
   ```

2. **MongoDB Configuration**
   Update your `.env` file:
   ```
   MONGO_URI=mongodb://localhost:27017
   MONGO_DB=crimora
   ```

3. **Populate Sample Data**
   ```bash
   python populate_data.py
   ```

4. **Start Server**
   ```bash
   python manage.py runserver
   ```

### Frontend Setup

1. **Install Dependencies**
   ```bash
   npm install
   ```

2. **Update API Base URL**
   In `apiService.js`, ensure the API_BASE_URL matches your backend:
   ```javascript
   const API_BASE_URL = 'http://127.0.0.1:8000';
   ```

## Usage Examples

### User Registration
```javascript
const authService = new AuthService();
const result = await authService.signup({
    name: "John Doe",
    email: "john@example.com",
    password: "secure123",
    phone: "1234567890"
});
```

### User Login
```javascript
const result = await authService.login("user@example.com", "password");
if (result.success) {
    // Redirect to appropriate dashboard
    window.location.href = result.user.role === 'admin' ? '/admin-dashboard' : '/dashboard';
}
```

### Report Crime (Authenticated)
```javascript
const crimeService = new CrimeService(authService);
const result = await crimeService.reportCrime({
    crimeType: "Theft",
    location: "Main Street",
    description: "Stolen bike",
    latitude: 12.345,
    longitude: 67.890
});
```

### Update Case Status (Admin Only)
```javascript
const dashboardService = new DashboardService(authService);
const result = await dashboardService.updateCaseStatus("case_id", "solved", "high");
```

## Security Considerations

1. **Token Management**
   - JWT tokens are stored in localStorage
   - Tokens expire after 24 hours
   - Always include Authorization header for protected routes

2. **Password Security**
   - Passwords are hashed using bcrypt
   - Never store plain text passwords
   - Implement password strength requirements in frontend

3. **API Security**
   - All sensitive endpoints require authentication
   - Role-based access control for admin functions
   - CSRF protection is disabled for API endpoints (configure properly for production)

## User Journey

### For Regular Users:
1. **Registration/Login** → Access granted to system
2. **Navigation Menu** → Access to Home, Map, Report Crime, IPC, News, Dashboard
3. **Report Crime** → Submit crime reports with automatic status tracking
4. **Dashboard** → View personal case status and statistics
5. **Case Tracking** → Monitor progress of reported cases

### For Administrators:
1. **Admin Login** → Full system access
2. **Admin Dashboard** → Complete system overview with statistics
3. **Case Management** → Update status and priority of all cases
4. **User Management** → View total users and system metrics
5. **News Management** → Add system announcements and updates

## System Benefits

1. **Security** - Robust authentication and authorization
2. **Role Management** - Clear separation of user and admin functions
3. **Real-time Updates** - MongoDB integration for live data
4. **User Experience** - Intuitive dashboards for different user types
5. **Case Tracking** - Complete lifecycle management of crime reports
6. **Scalability** - JWT tokens and MongoDB support system growth

## Testing the System

1. **Test User Registration**
   ```bash
   curl -X POST http://127.0.0.1:8000/auth/signup/ \
        -H "Content-Type: application/json" \
        -d '{"name":"Test User","email":"test@example.com","password":"test123"}'
   ```

2. **Test Login**
   ```bash
   curl -X POST http://127.0.0.1:8000/auth/login/ \
        -H "Content-Type: application/json" \
        -d '{"email":"admin@crimora.com","password":"admin123"}'
   ```

3. **Test Protected Endpoint**
   ```bash
   curl -X GET http://127.0.0.1:8000/dashboard/admin/ \
        -H "Authorization: Bearer YOUR_JWT_TOKEN"
   ```

## Next Steps

1. **Frontend Integration** - Integrate the provided React components
2. **UI Enhancement** - Style the components with your preferred CSS framework
3. **Mobile Optimization** - Ensure responsive design for mobile devices
4. **Testing** - Implement comprehensive testing for all endpoints
5. **Production Setup** - Configure proper security settings for production deployment

The system is now ready with complete authentication, role-based dashboards, and secure API endpoints. Users can register, login, report crimes, and track their cases, while administrators have full system oversight and management capabilities.
