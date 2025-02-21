# Website Login & Registration System (PHP & MySQL)
This is a simple web-based login and registration system built using PHP for server-side logic and MySQL for database management. It allows users to register for an account, log in, and manage their session securely.

* Features
User Registration: Allows users to create an account by providing a username, email, and password.
User Login: Authenticated login system with session management.
Password Hashing: User passwords are securely hashed using bcrypt for enhanced security.
Session Management: Users maintain their session and can log out when they wish.
Input Validation: Ensures proper validation of user inputs during both registration and login to prevent incorrect data and security risks.
Email Verification (optional): Users may receive an email verification link upon registration.

* Prerequisites
Before you begin, ensure you have the following installed on your local machine:
PHP (version 7.4 or above recommended)
MySQL (or any compatible database server)
A local server environment such as XAMPP, Apache server, VSCode live server.
Composer (if using any PHP libraries)

## STEPS:
* Step 1: Set Up the Database
Create a Database in MySQL for the project (e.g., login_system).
Import the Database Schema: You can find the SQL schema file (e.g., database.sql) inside the database/ folder.
sql ->CREATE TABLE users (
    id INT(11) AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
Configure Database Connection: Open config.php and enter your database connection details.
php:
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "login_system";  // Your database name

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
  die("Connection failed: " . $conn->connect_error);
}

* Step 2: Set Up the Project
Install Dependencies: If your project uses any PHP libraries via Composer, run:
bash -> composer install
Start Your Server: If using XAMPP or WAMP, make sure Apache and MySQL are running. Then, navigate to http://localhost/website-login-register-system/ in your web browser.

* Step 3: Create an Admin User (Optional)
If needed, you can insert a test admin user into the users table manually:
sql -> INSERT INTO users (username, email, password) VALUES ('admin', 'admin@example.com', 'hashed_password_here');
Make sure to hash the password using PHP's password_hash() method before inserting it into the database.

## Usage
~Registering a New Account
Navigate to the Registration page (register.php).
Enter a username, email, and password. The password will be hashed automatically for security purposes.
After successful registration, you will be redirected to the login page.
~Logging In
Navigate to the Login page (login.php).
Enter your username/email and password.
After successful authentication, you will be logged in, and your session will be started.
~Logging Out
Click on the Logout link in the navigation bar (or go to logout.php).
You will be logged out and redirected to the login page.
~Password Reset (Optional)
If you want to implement a password reset feature, you can integrate PHP mailer or another email service to send a password reset link to the user’s email.

### Security Features
Password Hashing: User passwords are hashed using PHP’s password_hash() function, making them secure.
Example:
php
$hashedPassword = password_hash($password, PASSWORD_BCRYPT);
Prepared Statements: SQL queries are executed using prepared statements to prevent SQL injection.

Example:
php
$stmt = $conn->prepare("INSERT INTO users (username, email, password) VALUES (?, ?, ?)");
$stmt->bind_param("sss", $username, $email, $password);
$stmt->execute();
Session Management: After a user logs in, a session is initiated to keep the user logged in until they log out.

