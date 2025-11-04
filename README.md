# Energy Management System

A distributed microservices-based energy management system that allows authenticated users to monitor and manage smart energy devices.

## System Architecture
- **Frontend**: React application serving the user interface
- **API Gateway**: Traefik reverse proxy routing requests to microservices
- **Auth Service**: Handles user authentication and JWT token generation
- **User Service**: Manages user CRUD operations
- **Device Service**: Manages device CRUD operations and device-user associations
- **PostgreSQL Database**: Three separate databases (auth_db, user_db, device_db)

### Backend
- **Java 21** with Spring Boot
- **Spring Security** for authentication/authorization
- **JWT** for token-based authentication
- **Spring Data JPA** for database operations
- **PostgreSQL 16** for data persistence
- **Maven** for dependency management

### Frontend
- **React 18** with React Router
- **Reactstrap** and **Bootstrap 5** for UI components

### Infrastructure
- **Docker** and **Docker Compose** for containerization
- **Traefik v3.0** as API Gateway and reverse proxy

## 📁 Project Structure

```
.
├── backend/
│   ├── auth-service/          # Authentication microservice
│   ├── device-service/        # Device management microservice
│   └── user-service/          # User management microservice
├── frontend/                  # React application
├── db-init/                   # Database creation scripts
├── docker-compose.yml         # Docker orchestration file
└── README.md
```
## Build
### Option 1: Building with Docker
1. **Clone the repository**:
```bash
git clone <repository-url>
cd <repository-folder>
```
3. **Build all services**:
```bash
docker-compose build
```
### Option 2: Building Locally

#### Backend Services
For each service (auth-service, user-service, device-service)
```bash
cd backend/<service-name>
mvnw.cmd spring-boot:run 
```
#### Frontend
```bash
cd frontend
npm install
npm run build
```

## API & User Roles

### Administrator
- Full CRUD operations on users and devices
- Assign/unassign devices to users
- Access to all system features

### Client (User)
- View their assigned devices
- Cannot modify users or devices
- Limited to personal device view


### Authentication Endpoints

**Base URL**: `http://localhost/api/auth` or `http://localhost:8083/api/auth`

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/register` | Register new user | No |
| POST | `/login` | User login | No |
| GET | `/validate?token={jwt}` | Validate JWT token | No |

### User Management Endpoints

**Base URL**: `http://localhost/api/users` or `http://localhost:8080/api/users`

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | List all users | Admin only |
| GET | `/{id}` | Get user by ID | Admin only |
| GET | `/username/{username}` | Get user ID by username | Admin only |
| POST | `/` | Create new user | Admin only |
| PUT | `/{id}` | Update user | Admin only |
| DELETE | `/{id}` | Delete user | Admin only |

### Device Management Endpoints

**Base URL**: `http://localhost/api/devices` or `http://localhost:8081/api/devices`

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | List all devices | Admin only |
| GET | `/{id}` | Get device by ID | Admin only |
| POST | `/` | Create device | Admin only |
| PUT | `/{id}` | Update device | Admin only |
| DELETE | `/{id}` | Delete device | Admin only |
| POST | `/{id}/assign/{ownerId}` | Assign device to user | Admin only |
| POST | `/{id}/unassign` | Unassign device | Admin only |
| GET | `/owner/{ownerId}` | Get devices by owner | Admin only |

### My Devices Endpoint

**Base URL**: `http://localhost/api/my-devices` or `http://localhost:8081/api/my-devices`

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | Get current user's devices | User only|




