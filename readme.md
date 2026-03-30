# Todo Backend API

A robust and secure RESTful API for managing todos with user authentication. Built with Node.js, Express, and MongoDB, this backend provides comprehensive features for user management and todo operations.

## Features

- **User Authentication**: Secure user registration and login with JWT token-based authentication
- **Todo Management**: Create, read, update, and delete todos
- **User Profiles**: User avatar and cover image support via Cloudinary integration
- **Password Security**: Bcrypt hashing for secure password storage
- **CORS Support**: Cross-origin resource sharing configuration
- **File Uploads**: Multer middleware for file handling
- **Error Handling**: Comprehensive error handling with custom error utilities
- **Async Operations**: Promise-based async request handling

## Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js (v5.2.1)
- **Database**: MongoDB with Mongoose (v9.3.3)
- **Authentication**: JWT (jsonwebtoken v9.0.3)
- **Security**: Bcrypt (v6.0.0)
- **File Upload**: Multer (v2.1.1)
- **Cloud Storage**: Cloudinary (v2.9.0)
- **Utilities**: Cookie-parser, CORS, dotenv
- **Development**: Nodemon, Prettier

## Installation

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local or Atlas cluster)
- npm or yarn package manager
- Cloudinary account (for image uploads)

### Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Todo-backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set environment variables**
   
   Create a `.env` file in the root directory with the following variables:
   ```env
   PORT=8000
   MONGODB_URI=<your-mongodb-connection-string>
   CORS_ORIGIN=http://localhost:3000
   
   # JWT Configuration
   ACCESS_TOKEN_SECRET=<your-access-token-secret>
   ACCESS_TOKEN_EXPIRY=7d
   REFRESH_TOKEN_SECRET=<your-refresh-token-secret>
   REFRESH_TOKEN_EXPIRY=10d
   
   # Cloudinary Configuration
   CLOUDINARY_NAME=<your-cloudinary-name>
   CLOUDINARY_API_KEY=<your-cloudinary-api-key>
   CLOUDINARY_API_SECRET=<your-cloudinary-api-secret>
   ```

## Running the Project

### Development Mode
Start the server with hot-reload using Nodemon:
```bash
npm run dev
```
The server will start at `http://localhost:8000` (or configured PORT)

### Production Mode
```bash
npm start
```

## Project Structure

```
src/
├── app.js                 # Express app configuration
├── index.js              # Server entry point
├── constants.js          # Project constants
├── controllers/          # Route controllers
│   ├── todo.controllers.js
│   └── user.controllers.js
├── models/              # Database schemas
│   ├── todo.models.js
│   └── user.models.js
├── routes/              # API routes
│   ├── todo.routes.js
│   └── user.routes.js
├── middlewares/         # Custom middlewares
│   ├── auth.middleware.js
│   └── multer.middleware.js
├── db/                  # Database connection
│   └── index.js
└── utils/               # Utility functions
    ├── ApiError.js      # Custom error handling
    ├── ApiResponse.js   # Standard response format
    ├── AsyncHandler.js  # Async error wrapper
    └── cloudinary.js    # Cloudinary integration

public/                 # Static files
├── temp/               # Temporary file storage
└── ...

```

## API Endpoints

### User Routes (`/users`)
- `POST /users/register` - Register a new user
- `POST /users/login` - User login
- `POST /users/logout` - User logout
- `POST /users/refresh-token` - Refresh access token
- `GET /users/profile` - Get user profile
- `PUT /users/profile` - Update user profile
- `POST /users/avatar` - Upload user avatar
- `POST /users/cover-image` - Upload cover image

### Todo Routes (`/todo`)
- `GET /todo` - Get all todos for authenticated user
- `POST /todo` - Create a new todo
- `PUT /todo/:todoId` - Update a specific todo
- `DELETE /todo/:todoId` - Delete a specific todo
- `PATCH /todo/:todoId/toggle` - Toggle todo completion status

## Database Models

### User Schema
```javascript
{
  username: String (unique, required),
  email: String (unique, required),
  fullName: String (required),
  password: String (hashed, required),
  avatar: String (Cloudinary URL),
  coverImage: String (Cloudinary URL),
  refreshToken: String,
  timestamps: true
}
```

### Todo Schema
```javascript
{
  title: String,
  content: String,
  completed: Boolean (default: false),
  createdBy: ObjectId (ref: User),
  timestamps: true
}
```

## Security Features

- **Password Hashing**: Passwords are hashed using bcrypt with salt rounds of 10
- **JWT Authentication**: Token-based authentication with access and refresh tokens
- **CORS**: Configured with credentials support
- **Input Validation**: Request payload size limits (16kb for JSON)
- **Cookie Security**: Cookie parser for secure cookie handling

## Development

### Code Style
The project uses Prettier for code formatting. Format code with:
```bash
npm run format
```

### Environment Variables
Always use a `.env` file for sensitive data. Never commit the `.env` file to version control.

## Error Handling

The API uses custom error handling utilities:
- **ApiError**: Custom error class for API errors
- **ApiResponse**: Standardized response format for all endpoints
- **AsyncHandler**: Wrapper for async route handlers with automatic error catching

## Dependencies Management

### Main Dependencies
- `express` - Web framework
- `mongoose` - MongoDB ODM
- `jsonwebtoken` - JWT authentication
- `bcrypt` - Password hashing
- `cloudinary` - Image cloud storage
- `multer` - File upload handling
- `cors` - Cross-origin resource sharing
- `dotenv` - Environment variables

### Dev Dependencies
- `nodemon` - Auto-reload during development
- `prettier` - Code formatting

## Contributing

1. Create a feature branch (`git checkout -b feature/AmazingFeature`)
2. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
3. Push to the branch (`git push origin feature/AmazingFeature`)
4. Open a Pull Request

## License

This project is licensed under the ISC License - see the package.json file for details.

## Support

For support, please create an issue in the repository or contact the project maintainer.

---

**Last Updated**: March 2026
