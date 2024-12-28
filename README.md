# Employee Management System

## Project Description
This project is a web-based Employee Management System designed to manage employee information efficiently. The application features a **Laravel** backend and a **Vue.js** frontend. It allows users to add, update, and delete employee records, including details such as name, address, phone number, and more. The application includes a user-friendly interface and supports responsive design.

---

## Features

- **CRUD Operations**: Add, update, and delete employee information.
- **Employee Details**: Manage employee data such as name, address, phone number, and more.
- **Responsive UI**: Optimized for various devices.

---

## Tech Stack

### Frontend:
- **Vue.js**
- **Tailwind CSS** 

### Backend:
- **Laravel**
- **MySQL** (via phpMyAdmin)

---

## Installation Guide

### Prerequisites

1. **PHP** (>= 8.0)
2. **Composer**
3. **Node.js** and **npm**
4. **MySQL**
5. **phpMyAdmin**

### Steps

#### 1. Clone the Repository
```bash
   git clone https://github.com/ishuuupishu/Employee_Management.git
   cd employee-management-system
```

#### 2. Install Backend Dependencies
```bash
   composer install
```

#### 3. Install Frontend Dependencies
```bash
   npm install
```

#### 4. Configure Environment Variables
1. Duplicate the `.env.example` file and rename it to `.env`.
2. Update the following fields in `.env`:
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=employee_management
DB_USERNAME=root
DB_PASSWORD=
```

#### 5. Generate Laravel Keys
```bash
   php artisan key:generate
```

#### 6. Run Database Migrations
```bash
   php artisan migrate
```

#### 7. Start the Development Servers
- Start the Laravel server:
```bash
   php artisan serve
```
- Start the Vue development server:
```bash
   npm run dev
```

#### 8. Access the Application
Visit the application in your browser:
```
http://127.0.0.1:8000
```

---

## Usage

2. **Manage Employees**:
   - Add new employee records.
   - Edit existing records.
   - Delete records no longer needed.
3. **Search and Filter**: Find employees using the search and filter options.

---
