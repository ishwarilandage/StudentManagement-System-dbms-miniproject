# Student Management System

A web-based Student Management System built with Flask and SQLite/MySQL for managing student records, attendance, and departments.

## Features

- **Student Management**: Add, edit, delete, and view student records
- **Department Management**: Create and manage academic departments
- **Attendance Tracking**: Record and track student attendance
- **User Authentication**: Secure login and signup system
- **Search Functionality**: Search students by roll number
- **Responsive UI**: Modern, mobile-friendly interface

## Technology Stack

- **Backend**: Python Flask
- **Database**: SQLite (default) / MySQL (production)
- **Frontend**: HTML, CSS, JavaScript, Bootstrap
- **Authentication**: Flask-Login

## Prerequisites

- Python 3.8 or higher
- pip (Python package installer)
- MySQL (optional, for production use)

## Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd StudentManagement-System-dbms-miniproject
```

### 2. Navigate to Project Directory

```bash
cd "student management"
```

### 3. Create Virtual Environment

```bash
# Create virtual environment
py -m venv .venv

# Activate virtual environment
# On Windows:
.\.venv\Scripts\Activate.ps1

# On macOS/Linux:
source .venv/bin/activate
```

### 4. Install Dependencies

```bash
# Upgrade pip
python -m pip install --upgrade pip wheel

# Install project dependencies
pip install -r requirements.txt
```

### 5. Database Setup

#### Option A: SQLite (Recommended for Development)

The project is configured to use SQLite by default. No additional setup required - the database will be created automatically when you run the application.

#### Option B: MySQL (For Production)

1. **Install MySQL** and start the service:
   ```bash
   # Windows (run as Administrator)
   net start MySQL80
   
   # macOS (using Homebrew)
   brew services start mysql
   
   # Linux (Ubuntu/Debian)
   sudo systemctl start mysql
   ```

2. **Create Database**:
   ```bash
   mysql -u root -p -e "CREATE DATABASE IF NOT EXISTS students CHARACTER SET utf8mb4;"
   ```

3. **Import Schema** (if you have a students.sql file):
   ```bash
   mysql -u root -p students < students.sql
   ```

4. **Update Database URI** in `main.py`:
   ```python
   # Change line 27 from:
   app.config['SQLALCHEMY_DATABASE_URI']='sqlite:///students.db'
   
   # To:
   app.config['SQLALCHEMY_DATABASE_URI']='mysql+pymysql://root:your_password@localhost/students'
   ```

### 6. Run the Application

```bash
python main.py
```

The application will start on `http://127.0.0.1:5000/`

## Usage

### 1. Access the Application

Open your web browser and navigate to `http://127.0.0.1:5000/`

### 2. User Registration

- Click on "Sign Up" to create a new account
- Fill in the required details (username, email, password)
- Use the registered credentials to log in

### 3. Student Management

- **Add Student**: Navigate to the student form and fill in student details
- **View Students**: Access the student details page to see all registered students
- **Edit Student**: Click on edit option to modify student information
- **Delete Student**: Remove student records as needed

### 4. Department Management

- Add new academic departments
- Manage existing departments

### 5. Attendance Tracking

- Record student attendance
- View attendance records
- Search attendance by roll number

## Project Structure

```
student management/
├── main.py                 # Main Flask application
├── requirements.txt        # Python dependencies
├── students.sql           # Database schema (if using MySQL)
├── static/                # Static files (CSS, JS, images)
│   ├── assets/
│   │   ├── css/
│   │   ├── js/
│   │   └── vendor/        # Third-party libraries
│   └── images/
├── templates/             # HTML templates
│   ├── base.html
│   ├── index.html
│   ├── login.html
│   ├── signup.html
│   ├── student.html
│   ├── studentdetails.html
│   ├── edit.html
│   ├── attendance.html
│   ├── department.html
│   ├── search.html
│   └── triggers.html
└── students.db           # SQLite database (created automatically)
```

## Database Models

- **User**: User authentication (username, email, password)
- **Student**: Student information (roll number, name, semester, gender, branch, email, phone, address)
- **Department**: Academic departments (branch name)
- **Attendance**: Student attendance records
- **Trig**: Audit trail for database changes

## Development

### Adding New Features

1. **Create new routes** in `main.py`
2. **Add database models** if needed
3. **Create HTML templates** in the `templates/` directory
4. **Add static files** (CSS/JS) in the `static/` directory

### Database Migrations

When adding new models or modifying existing ones:

```python
# In main.py, add this before app.run()
with app.app_context():
    db.create_all()  # This creates tables based on your models
```

### Testing

To test the database connection:

```python
# Visit http://127.0.0.1:5000/test
# This will show "My database is Connected" if everything is working
```

## Troubleshooting

### Common Issues

1. **Module Import Errors**:
   ```bash
   # Make sure virtual environment is activated
   .\.venv\Scripts\Activate.ps1
   
   # Reinstall dependencies
   pip install -r requirements.txt --force-reinstall
   ```

2. **Database Connection Issues**:
   - For SQLite: Check file permissions
   - For MySQL: Verify service is running and credentials are correct

3. **Port Already in Use**:
   ```bash
   # Kill process using port 5000
   # Windows:
   netstat -ano | findstr :5000
   taskkill /PID <PID_NUMBER> /F
   
   # Or change port in main.py:
   app.run(debug=True, port=5001)
   ```

4. **Permission Denied (MySQL)**:
   - Run PowerShell as Administrator
   - Or use SQLite for development

### Error Messages

- **"Access is denied"**: Run terminal as Administrator
- **"Can't connect to MySQL"**: Start MySQL service
- **"Module not found"**: Activate virtual environment and install dependencies

## Production Deployment

### Environment Variables

Create a `.env` file for production:

```env
FLASK_ENV=production
DATABASE_URL=mysql+pymysql://username:password@localhost/students
SECRET_KEY=your-secret-key-here
```

### Security Considerations

- Change default secret key in `main.py`
- Use environment variables for sensitive data
- Implement proper password hashing (currently using plain text)
- Add input validation and sanitization
- Use HTTPS in production

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is created for educational purposes as part of a college mini-project.

## Contact

For questions or support, contact the development team.

---

**Note**: This is a college mini-project for learning purposes. For production use, additional security measures and optimizations are recommended.
