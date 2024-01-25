# User authentication service

## Curriculum - User Authentication Service

### Project Overview

This project focuses on creating a user authentication service using Flask and SQLAlchemy. The goal is to implement key functionalities related to user authentication, including user registration, login, session management, password reset, and more.

### Project Structure

The project is structured into various tasks, each with its specific requirements and objectives. Below is a brief overview of each task:

1. **User Model (Task 0):**

   - Create a SQLAlchemy model named User for a database table named users.
   - Define attributes such as id, email, hashed_password, session_id, and reset_token.

2. **Create User (Task 1):**

   - Implement the add_user method in the DB class to add a user to the database.

3. **Find User (Task 2):**

   - Implement the find_user_by method in the DB class to locate a user based on input arguments.

4. **Update User (Task 3):**

   - Implement the update_user method in the DB class to update user attributes.

5. **Hash Password (Task 4):**

   - Define a \_hash_password method in the auth module to hash a given password.

6. **Register User (Task 5):**

   - Implement the register_user method in the Auth class to register a new user.

7. **Basic Flask App (Task 6):**

   - Set up a basic Flask app with a single GET route ("/") returning a JSON payload.

8. **Register User Endpoint (Task 7):**

   - Implement the endpoint to register a user, handling duplicate registrations.

9. **Credentials Validation (Task 8):**

   - Implement the valid_login method in the Auth class to validate user credentials.

10. **Generate UUIDs (Task 9):**

    - Implement a \_generate_uuid function in the auth module to generate a new UUID.

11. **Get Session ID (Task 10):**

    - Implement the create_session method in the Auth class to create and return a session ID.

12. **Log In (Task 11):**

    - Implement the login function for the POST /sessions route, handling authentication.

13. **Find User by Session ID (Task 12):**

    - Implement the get_user_from_session_id method in the Auth class.

14. **Destroy Session (Task 13):**

    - Implement the destroy_session method in the Auth class to reset a user's session.

15. **Log Out (Task 14):**

    - Implement the logout function for the DELETE /sessions route.

16. **User Profile (Task 15):**

    - Implement the profile function for the GET /profile route.

17. **Generate Reset Password Token (Task 16):**

    - Implement the get_reset_password_token method in the Auth class.

18. **Get Reset Password Token Endpoint (Task 17):**

    - Implement the endpoint for the POST /reset_password route.

19. **Update Password (Task 18):**

    - Implement the update_password method in the Auth class.

20. **Update Password Endpoint (Task 19):**
    - Implement the endpoint for the PUT /reset_password route.

### End-to-End Integration Test (Task 20)

To test the end-to-end functionality of the authentication service, a main.py module has been provided. This module contains functions for various actions such as user registration, login, profile access, password reset, etc. The provided code at the end of main.py demonstrates how to use these functions to perform a series of actions.

### Running the App

1. Ensure that the required packages are installed:

   ```bash
   pip3 install Flask SQLAlchemy bcrypt requests
   ```

2. Run the Flask app:

   ```bash
   python3 app.py
   ```

3. Open a new terminal window and run the end-to-end integration test:

   ```bash
   python3 main.py
   ```

   If everything is correct, there should be no output.

### Disclaimer

Copyright © 2024 ALX, All rights reserved.

Please refer to the provided GitHub repository for the complete project code and files: [alx-backend-user-data](https://github.com/mugambi12/alx-backend-user-data).
