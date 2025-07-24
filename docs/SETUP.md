# Developer Setup Guide - project-##-medisync:-a

## Prerequisites

* **Required Software Versions:**
    * **Docker:** 20.10.0 or later (Recommended for Option 1)
    * **Node.js:** 16.x (LTS) or later (For both options)
    * **Python:** 3.9 or later (For Option 2)
    * **PostgreSQL:** 14 or later (For both options, adjust as needed)
    * **Git:** 2.30 or later

* **Development Tools:**
    * Git client (e.g., GitKraken, Sourcetree, command-line Git)
    * Text editor or IDE (see IDE recommendations below)
    * Database client (e.g., pgAdmin, DBeaver)

* **IDE Recommendations and Configurations:**
    * **VS Code:**  Highly recommended. Install the following extensions:
        * Python extension (for backend)
        * ESLint (for frontend)
        * Prettier (for code formatting)
        * Docker extension
    * **PyCharm (Professional):** Good for Python backend development.
    * **WebStorm:** Good for frontend JavaScript development.


## Local Development Setup

### Option 1: Docker Development (Recommended)

1. **Clone Repository:**
   ```bash
   git clone <repository_url>
   cd project-##-medisync:-a
   ```

2. **Docker Setup:** Ensure Docker and Docker Compose are installed and running.

3. **Development `docker-compose.yml` Configuration:**  (Example - adapt to your project's structure)

   ```yaml
   version: "3.9"
   services:
     backend:
       build: ./backend
       ports:
         - "8000:8000"  # Adjust port as needed
       depends_on:
         - db
       environment:
         - DATABASE_URL=postgresql://postgres:password@db:5432/medisync  # Adjust as needed
     frontend:
       build: ./frontend
       ports:
         - "3000:3000"  # Adjust port as needed
       depends_on:
         - backend
     db:
       image: postgres:14
       ports:
         - "5432:5432"
       environment:
         - POSTGRES_USER=postgres
         - POSTGRES_PASSWORD=password
         - POSTGRES_DB=medisync
   ```

4. **Hot Reload Setup:**  (This will depend on your frontend framework - example using Nodemon)
   * In the `frontend` directory, ensure you have `nodemon` installed (`npm install -g nodemon`).
   * Start the frontend with `nodemon` instead of `npm start` to automatically restart on changes.

### Option 2: Native Development

1. **Backend Setup:**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```

2. **Frontend Setup:**
   ```bash
   cd frontend
   npm install
   ```

3. **Database Setup:**
   * Download and install PostgreSQL.
   * Create a database named `medisync`.
   * Create a user `postgres` (or your preferred username) with a password.  Adjust the `DATABASE_URL` in your `.env` file accordingly.


## Environment Configuration

1. **Required Environment Variables:** (Example)
   * `DATABASE_URL`: Database connection string.
   * `API_KEY`:  For external API integrations.
   * `SECRET_KEY`: For session management (backend).
   * `FRONTEND_URL`: URL of the frontend application.

2. **Local Development `.env` File Setup:** Create a `.env` file in the root directory (or as specified in your project structure) and populate it with your local environment variables.  Example:
   ```
   DATABASE_URL=postgresql://postgres:password@localhost:5432/medisync
   API_KEY=your_api_key
   SECRET_KEY=a_very_secret_key
   FRONTEND_URL=http://localhost:3000
   ```

3. **Configuration for Different Environments:**  Use environment variables and configuration files (e.g., YAML) to manage settings for development, staging, and production environments.  Consider using a configuration management tool like `dotenv` (Python) or similar for Node.js.


## Running the Application

1. **Start Commands for Development:**
   * **Option 1 (Docker):** `docker-compose up -d`
   * **Option 2 (Native):**  Start the backend server (e.g., `python manage.py runserver` if using Django), then start the frontend server (`npm start` or `nodemon`).

2. **How to Access Frontend and Backend:**
   * **Frontend:** Access the frontend at `http://localhost:3000` (or the port specified in `docker-compose.yml` or your setup).
   * **Backend:** Access the backend API endpoints at `http://localhost:8000/api/` (or the port specified).

3. **API Documentation Access:**  Use tools like Swagger or OpenAPI to generate and host API documentation.


## Development Workflow

1. **Git Workflow and Branching Strategy:** Use Git for version control.  Employ a branching strategy like Gitflow (feature branches, develop branch, master branch).

2. **Code Formatting and Linting Setup:**  Configure linters (e.g., ESLint for JavaScript, Pylint for Python) and formatters (e.g., Prettier) to ensure consistent code style.

3. **Testing Procedures:** Write unit tests, integration tests, and end-to-end tests.  Use a testing framework like pytest (Python) or Jest (JavaScript).

4. **Debugging Setup:** Use your IDE's debugger or command-line debuggers (e.g., `pdb` in Python, `node inspect` in Node.js).


## Database Management

1. **Running Migrations:** Use database migration tools (e.g., Alembic for Python, Prisma Migrate for Node.js) to manage database schema changes.

2. **Seeding Development Data:** Create scripts to populate the database with sample data for development and testing.

3. **Database Reset Procedures:**  Implement scripts to easily reset the database to a clean state.


## Testing

1. **Running Unit Tests:** `pytest` (Python) or `jest` (JavaScript).

2. **Running Integration Tests:**  Use appropriate testing frameworks to test interactions between different components.

3. **Test Coverage Reports:** Generate test coverage reports to track progress and identify areas needing more testing.


## Common Development Tasks

1. **Adding New API Endpoints:**  Follow the project's API design guidelines.  Write tests to ensure functionality.

2. **Adding New Frontend Components:**  Use the project's frontend framework (React, Vue, Angular, etc.) to create new components.  Ensure proper styling and integration with the backend API.

3. **Database Schema Changes:**  Use migration tools to manage changes.  Update any affected code and tests.

4. **Adding Dependencies:** Use `pip` (Python) or `npm` (Node.js) to add new dependencies. Update the `requirements.txt` or `package.json` files accordingly.


## Troubleshooting

1. **Common Setup Issues:** Check the logs for error messages.  Ensure all dependencies are installed correctly.

2. **Port Conflicts Resolution:** Change the port numbers in your configuration files if there are conflicts.

3. **Dependency Issues:** Use tools like `pip-tools` (Python) or `npm ls` (Node.js) to diagnose dependency problems.

4. **Environment Variable Problems:** Verify that your environment variables are set correctly and accessible to the application.


## Contributing

1. **Code Style Guidelines:** Adhere to the project's code style guidelines (e.g., PEP 8 for Python, Airbnb style guide for JavaScript).

2. **Pull Request Process:** Create clear and concise pull requests with detailed descriptions of changes.  Ensure code is reviewed and tested before merging.

3. **Issue Reporting:**  Report issues using the project's issue tracker, providing detailed descriptions and reproduction steps.  Include relevant logs and error messages.


This guide provides a foundation.  Adapt it to your specific project's technology stack and requirements.  Remember to consult the project's documentation for more detailed information.
