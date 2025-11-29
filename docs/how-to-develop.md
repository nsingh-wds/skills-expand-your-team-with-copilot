# Development Guide

## Initial Setup

This project is best developed using GitHub Codespaces, which provides a consistent development environment with all the necessary tools pre-configured.

### Setting up your development environment

1. Open the repository in a codespace
2. Wait for the container to finish building and installing dependencies
3. Install Python dependencies by running:

   ```bash
   pip install -r src/requirements.txt
   ```

### Dependencies

The project requires the following Python packages:

- FastAPI - Modern web framework for building APIs
- Uvicorn - ASGI server implementation for running the FastAPI application
- PyMongo - MongoDB driver for Python
- Argon2-cffi - Password hashing library used for database initialization

These dependencies will be installed when you run `pip install -r src/requirements.txt`

> [!NOTE]
> This project requires a MongoDB instance running locally on port 27017. Make sure MongoDB is installed and running before starting the application.

## Debugging

### Running the website locally

1. From VS Code's Run and Debug view (Ctrl+Shift+D), select "Launch Mergington WebApp" from the launch configuration dropdown
2. Press F5 or click the green play button to start debugging
3. The website will be available at `http://localhost:8000`
4. The API documentation will be available at `http://localhost:8000/docs`

### Debugging tips

- FastAPI's auto-reload feature will automatically restart the server when you make code changes
- Use the interactive API documentation at `/docs` to test your endpoints

## Usage

### Running the application

1. Install the dependencies:

   ```bash
   pip install -r src/requirements.txt
   ```

2. Run the application:

   ```bash
   python -m uvicorn src.app:app --host 0.0.0.0 --port 8000
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

### API Endpoints

#### Activities

| Method | Endpoint                           | Description                                                                                                              |
| ------ | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| GET    | `/activities`                      | Get all activities with their details. Supports optional query parameters: `day`, `start_time`, `end_time` for filtering |
| GET    | `/activities/days`                 | Get a list of all days that have activities scheduled                                                                    |
| POST   | `/activities/{activity_name}/signup` | Sign up a student for an activity. Requires `email` query parameter and `teacher_username` for authentication        |
| POST   | `/activities/{activity_name}/unregister` | Remove a student from an activity. Requires `email` query parameter and `teacher_username` for authentication    |

#### Authentication

| Method | Endpoint              | Description                                      |
| ------ | --------------------- | ------------------------------------------------ |
| POST   | `/auth/login`         | Login a teacher account with username and password |
| GET    | `/auth/check-session` | Check if a session is valid by username          |

> [!IMPORTANT]
> All data is stored in MongoDB database running locally on port 27017.
