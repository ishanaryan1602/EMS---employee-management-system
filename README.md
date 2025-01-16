# Employee Management System (EMS)

## Overview

The Employee Management System (EMS) is a MERN stack application designed to facilitate task management within an organization. It allows employers to assign tasks to employees, modify task assignments, and track task completion. Employees can view and complete their tasks.

---

## Features

### Employer Features:

- Assign tasks to employees.
- Update task details (title, description, personnel assigned).
- Reassign tasks to different employees.
- View all tasks and their statuses.

### Employee Features:

- View assigned tasks.
- Mark tasks as completed.

---

## Basic Layout

### Backend:

1. **Models**:
    - **User Model**:
        - `name`: String
        - `email`: String
        - `password`: String (hashed)
        - `role`: String (either `employer` or `employee`)
    - **Task Model**:
        - `title`: String
        - `description`: String
        - `assignedTo`: Reference to User (employee)
        - `status`: String (default: `Pending`, values: `Pending`, `Completed`)
        - `createdBy`: Reference to User (employer)
2. **APIs**:
    - User Authentication:
        - **POST** `/api/auth/register`
        - **POST** `/api/auth/login`
    - Task Management:
        - **GET** `/api/tasks`: Get all tasks (employer) or assigned tasks (employee).
        - **POST** `/api/tasks`: Create a new task (employer only).
        - **PUT** `/api/tasks/:id`: Update task details (employer only).
        - **DELETE** `/api/tasks/:id`: Delete a task (employer only).
        - **PATCH** `/api/tasks/:id/complete`: Mark task as completed (employee only).

---

### Frontend:

1. **Pages**:
    - **Login Page**:
        - Form fields: `Email`, `Password`
    - **Dashboard Page**:
        - **Employer View**:
            - Display list of tasks with options to edit, reassign, or delete.
            - Button to create new tasks.
        - **Employee View**:
            - Display list of assigned tasks with a button to mark as completed.
    - **Task Form Modal**:
        - Fields: `Task Title`, `Task Description`, `Personnel Assigned`
2. **Components**:
    - **Task Card**:
        - Props: `title`, `description`, `assignedTo`, `status`, `actions`.
    - **Navbar**:
        - Links: `Dashboard`, `Logout`
    - **Protected Route**:
        - Redirects unauthorized users to the login page.
3. **State Management**:
    - Use `React Context` or `Redux` to manage authentication and tasks data.

---

## Documentation

### Setup Instructions:

1. **Clone the repository**:
    
    ```bash
    git clone <repository_url>
    cd employee-management-system
    ```
    
2. **Install dependencies**:
    - Backend:
        
        ```bash
        cd backend
        npm install
        ```
        
    - Frontend:
        
        ```bash
        cd frontend
        npm install
        ```
        
3. **Environment Variables**:
    - Create `.env` files in both `backend` and `frontend` directories.
    - Backend `.env`:
        
        ```
        PORT=5000
        MONGO_URI=<your_mongodb_connection_string>
        JWT_SECRET=<your_jwt_secret>
        ```
        
    - Frontend `.env`:
        
        ```
        REACT_APP_BACKEND_URL=http://localhost:5000
        ```
        
4. **Run the application**:
    - Backend:
        
        ```bash
        npm run dev
        ```
        
    - Frontend:
        
        ```bash
        npm start
        ```

---

### API Endpoints:

#### User Authentication:

- **POST** `/api/auth/register`
    - Request Body:
        
        ```json
        {
          "name": "John Doe",
          "email": "john.doe@example.com",
          "password": "password123",
          "role": "employee"
        }
        ```
        
- **POST** `/api/auth/login`
    - Request Body:
        
        ```json
        {
          "email": "john.doe@example.com",
          "password": "password123"
        }
        ```

#### Task Management:

- **GET** `/api/tasks`
    - Headers:
        
        ```json
        {
          "Authorization": "Bearer <jwt_token>"
        }
        ```
        
- **POST** `/api/tasks`
    - Request Body:
        
        ```json
        {
          "title": "Complete Report",
          "description": "Prepare the monthly financial report",
          "assignedTo": "employee_id"
        }
        ```
        
- **PUT** `/api/tasks/:id`
    - Request Body:
        
        ```json
        {
          "title": "Updated Title",
          "description": "Updated Description",
          "assignedTo": "new_employee_id"
        }
        ```
        
- **PATCH** `/api/tasks/:id/complete`
    - No request body needed.

---

### Notes:

- Ensure proper role-based access control for APIs.
- Validate all inputs on both frontend and backend.
- Use a robust state management library for efficient data handling.
