# TaskFlow - Task Management System

A comprehensive task management web application built with Django, featuring user authentication, task organization, and productivity tracking.

## 🌟 Features

### Core Functionality
- **User Authentication**: Secure signup, login, and logout
- **Task Management**: Create, read, update, and delete tasks
- **Task Organization**: Priority levels (High, Medium, Low) and due dates
- **Bulk Operations**: Complete or delete multiple tasks at once
- **Task Filtering**: Filter by status (pending, completed), priority, and overdue tasks
- **Search**: Find tasks by title or description
- **Pagination**: Efficient handling of large task lists

### User Experience
- **Dashboard**: Overview with task statistics and completion rates
- **Profile Management**: Update personal information and change passwords
- **Responsive Design**: Mobile-friendly interface
- **Real-time Feedback**: Success/error messages for all operations
- **Overdue Detection**: Visual indicators for overdue tasks

### Security Features
- **Environment Variables**: Secure configuration management
- **Password Validation**: Strong password requirements
- **CSRF Protection**: Built-in Django security features
- **User Isolation**: Tasks are user-specific and secure

## 🛠️ Technology Stack

### Backend
- **Framework**: Django 5.2
- **Database**: PostgreSQL (Production) / SQLite (Development)
- **Authentication**: Django's built-in authentication system
- **Static Files**: WhiteNoise for production static file serving

### Frontend
- **Template Engine**: Django Templates
- **Styling**: Custom CSS
- **JavaScript**: Vanilla JS for interactive features
- **Icons**: Unicode emojis for visual appeal

### Deployment
- **Frontend**: GitHub Pages (Static landing page)
- **Backend**: Render (Django application)
- **Database**: PostgreSQL on Render

## 📁 Project Structure

```
taskflow/
├── taskflow/
│   ├── __init__.py
│   ├── settings.py          # Django settings with environment variables
│   ├── urls.py              # URL configuration
│   └── wsgi.py              # WSGI configuration
├── todo/
│   ├── models.py            # Task model definition
│   ├── views.py             # All view functions
│   └── urls.py              # App URL patterns
├── templates/
│   ├── index.html           # Landing page
│   ├── login.html           # User login
│   ├── signup.html          # User registration
│   ├── dashboard.html       # Main task dashboard
│   └── profile.html         # User profile
├── static/
│   ├── css/
│   ├── js/
│   └── img/
├── staticfiles/             # Production static files
├── requirements.txt         # Python dependencies
└── README.md               # This file
```

## 🚀 Installation & Setup

### Prerequisites
- Python 3.8+
- PostgreSQL (for production)
- Git

### Local Development Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd taskflow
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Environment Variables**
   Create a `.env` file in the root directory:
   ```env
   SECRET_KEY=your-secret-key-here
   DEBUG=True
   ALLOWED_HOSTS=127.0.0.1 localhost
   DATABASE_URL=sqlite:///db.sqlite3
   ```

5. **Database Setup**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   python manage.py createsuperuser
   ```

6. **Run Development Server**
   ```bash
   python manage.py runserver
   ```

### Production Deployment

#### Environment Variables for Production
```env
SECRET_KEY=your-production-secret-key
DEBUG=False
ALLOWED_HOSTS=your-domain.com yourdomain.onrender.com
DATABASE_URL=postgresql://user:password@host:port/database
```

#### Deployment on Render
1. Connect your GitHub repository to Render
2. Set the build command: `pip install -r requirements.txt && python manage.py collectstatic --noinput`
3. Set the start command: `python manage.py migrate && gunicorn taskflow.wsgi:application`
4. Add environment variables in Render dashboard

## 📊 Database Schema

### User Model (Django's built-in)
- `username` (email)
- `email`
- `first_name`
- `last_name`
- `password`

### Task Model
- `user` (ForeignKey to User)
- `title` (CharField)
- `description` (TextField)
- `priority` (CharField: 'low', 'medium', 'high')
- `due_date` (DateField)
- `completed` (BooleanField)
- `created_at` (DateTimeField)
- `updated_at` (DateTimeField)

## 🔧 Configuration

### Settings Overview
- **Database**: Configured for both SQLite (development) and PostgreSQL (production)
- **Static Files**: WhiteNoise middleware for production
- **Security**: Environment-based configuration
- **Authentication**: Email as username

### Key Settings
```python
# Security
SECRET_KEY = os.environ.get("SECRET_KEY")
DEBUG = os.environ.get("DEBUG", "False").lower() == "true"
ALLOWED_HOSTS = os.environ.get("ALLOWED_HOSTS").split(" ")

# Database
DATABASE_URL = os.environ.get("DATABASE_URL", "sqlite:///db.sqlite3")
DATABASES = {'default': dj_database_url.parse(DATABASE_URL)}

# Static Files
STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / "staticfiles"
STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
```

## 🎯 Usage

### For Users
1. **Register**: Create an account with email and password
2. **Login**: Access your personal dashboard
3. **Create Tasks**: Add tasks with title, description, priority, and due date
4. **Manage Tasks**: Edit, complete, or delete tasks
5. **Filter & Search**: Find tasks using filters and search functionality
6. **Bulk Operations**: Select multiple tasks for batch operations
7. **Profile**: Update personal information and change password

### For Administrators
- Access admin panel at `/admin/`
- Manage users and tasks
- Monitor system usage

## 🔐 Security Features

- **CSRF Protection**: All forms include CSRF tokens
- **Password Validation**: Minimum 8 characters required
- **User Isolation**: Users can only access their own tasks
- **Secure Headers**: Security middleware enabled
- **Environment Variables**: Sensitive data stored securely

## 🎨 Frontend Features

### Dashboard
- Task statistics (total, completed, pending, completion rate)
- Task list with filtering and pagination
- Inline task editing
- Bulk selection and operations

### Responsive Design
- Mobile-friendly interface
- Flexible grid layouts
- Touch-friendly buttons

### User Experience
- Real-time feedback with Django messages
- Visual indicators for task status
- Intuitive navigation
- Clean, modern design

## 📈 Performance Optimizations

- **Pagination**: Efficient handling of large datasets
- **Database Indexing**: Optimized queries
- **Static File Compression**: WhiteNoise compression
- **Caching**: Never-cache decorators for sensitive views

## 🔄 API Endpoints

### Authentication
- `GET /` - Landing page
- `GET /login/` - Login page
- `POST /login/` - User login
- `GET /signup/` - Registration page
- `POST /signup/` - User registration
- `GET /logout/` - User logout

### Task Management
- `GET /dashboard/` - Task dashboard
- `POST /add-task/` - Create new task
- `POST /update-task/<id>/` - Update task
- `POST /delete-task/<id>/` - Delete task
- `POST /toggle-task/<id>/` - Toggle task completion
- `POST /bulk-operations/` - Bulk task operations

### User Profile
- `GET /profile/` - User profile page
- `POST /update-profile/` - Update profile information
- `POST /change-password/` - Change password

## 🐛 Troubleshooting

### Common Issues

1. **Database Connection Error**
   - Check DATABASE_URL environment variable
   - Ensure PostgreSQL is running (production)
   - Verify database credentials

2. **Static Files Not Loading**
   - Run `python manage.py collectstatic`
   - Check STATIC_ROOT and STATIC_URL settings
   - Verify WhiteNoise configuration

3. **Authentication Issues**
   - Clear browser cache and cookies
   - Check SECRET_KEY consistency
   - Verify email format for username

## 📝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make changes with proper testing
4. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- Django framework for robust web development
- Render for reliable hosting
- GitHub Pages for static site hosting
- WhiteNoise for static file serving

## 📞 Support

For support, please open an issue in the GitHub repository or contact the development team.

---

**Live Demo**: [TaskFlow Landing Page](https://deceptiveneeraj.github.io/taskflow/)

**Author**: Neeraj Solanki
**Version**: 1.0.0
**Last Updated**: 2025