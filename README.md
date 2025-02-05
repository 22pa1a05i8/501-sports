# Sports Session Management App

## Description
The **Sports Session Management App** is a web-based platform designed to facilitate the organization and management of sports sessions. Users can register, log in, create sessions, and join them. The app supports two types of users:
- **Admins**: Manage sports, create and manage sessions, and view reports.
- **Players**: View available sessions, join sessions, and participate in sports activities.

## Features
- **Authentication**: Users can register, log in, and log out.
- **Admin Dashboard**: Admins can manage sports, sessions, and view detailed reports.
- **Player Dashboard**: Players can view and join available sessions.
- **Session Management**: Admins can create, delete, and cancel sessions; players can join and leave sessions.
- **Reports**: Admins can generate reports on session popularity by sport.

## Technologies Used
- **Node.js**: Backend framework to run the application.
- **Express**: Web framework for building the app.
- **bcryptjs**: For password hashing and authentication security.
- **PostgreSQL**: Database for storing user data, sports, and sessions.
- **EJS**: Template engine for rendering dynamic HTML content.
- **express-session**: For handling user sessions.

---

## Installation

### Prerequisites
Ensure you have the following installed:
- **Node.js** (>=14.x)
- **npm** (Node package manager)
- **PostgreSQL** (>=12.x)

### Steps to Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/sports-session-management-app.git
   ```

2. **Navigate to the project directory:**
   ```bash
   cd sports-session-management-app
   ```

3. **Install dependencies:**
   ```bash
   npm install
   ```

4. **Set up PostgreSQL:**
   - Create a PostgreSQL database (e.g., `sports_sessions`).
   - Update the database connection configuration in `./database.js`.
   - Run the following SQL migrations to create necessary tables:

   ```sql
   CREATE TABLE users (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100),
     email VARCHAR(100) UNIQUE NOT NULL,
     password VARCHAR(255) NOT NULL,
     role VARCHAR(50) CHECK (role IN ('admin', 'player')) NOT NULL
   );

   CREATE TABLE sports (
     id SERIAL PRIMARY KEY,
     name VARCHAR(100) NOT NULL
   );

   CREATE TABLE sessions (
     id SERIAL PRIMARY KEY,
     sport_id INT REFERENCES sports(id),
     creator_id INT REFERENCES users(id),
     team1 VARCHAR(100),
     team2 VARCHAR(100),
     additional_players INT DEFAULT 0,
     date TIMESTAMP,
     venue VARCHAR(255),
     cancelled BOOLEAN DEFAULT FALSE,
     cancellation_reason TEXT
   );

   CREATE TABLE session_players (
     session_id INT REFERENCES sessions(id),
     player_id INT REFERENCES users(id),
     PRIMARY KEY (session_id, player_id)
   );
   ```

5. **Start the server:**
   ```bash
   npm start
   ```

6. **Access the application:**
   Open your browser and visit `http://localhost:3000`.

---

## Application Routes
| Method | Endpoint             | Description |
|--------|----------------------|-------------|
| GET    | `/`                  | Home page |
| GET    | `/login`             | Login page |
| POST   | `/login`             | Login action |
| GET    | `/register`          | Registration page |
| POST   | `/register`          | Register user |
| GET    | `/admin-dashboard`   | Admin dashboard |
| POST   | `/create-sport`      | Create a new sport |
| POST   | `/delete-session`    | Delete a session |
| GET    | `/player-dashboard`  | Player dashboard |
| POST   | `/create-session`    | Create a new session |
| POST   | `/join-session`      | Join a session |
| POST   | `/cancel-session`    | Cancel a session |
| GET    | `/reports`           | View session popularity reports |

---

## User Roles
### **Admin:**
- Create and manage sports and sessions.
- View reports on session popularity.
- Delete or cancel sessions.

### **Player:**
- Register and log in.
- View available sessions.
- Join sports sessions and interact with other players.

---

## Security Considerations
- Passwords are securely hashed using **bcryptjs**.
- User sessions are managed using **express-session**.
- Only authorized users can create or manage sessions.

---

## Contributing
Contributions are welcome! Follow these steps to contribute:
1. Fork the repository.
2. Create a new branch (`feature-branch`).
3. Commit your changes.
4. Push the changes and create a pull request.

