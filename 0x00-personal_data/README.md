# alx-backend-user-data

## 0x00. Personal data

### Back-end Authentication
- **Author:** Emmanuel Turlay, Staff Software Engineer at Cruise
- **Weight:** 1
- **Project Timeline:** Ongoing second chance project - started Jan 10, 2024, must end by Jan 14, 2024
- **Reviews:** Manual QA review must be done (request it when you are done with the project). An auto review will be launched at the deadline.
- **Review Status:** In a nutshell…
  - Manual QA review: In the second deadline
  - Auto QA review: 0.0/32 mandatory
  - Altogether: Waiting on some reviews

### Resources
Read or watch:
- [What Is PII, non-PII, and Personal Data?](#)
- [Logging Documentation](#)
- [Bcrypt Package](#)
- [Logging to Files, Setting Levels, and Formatting](#)

### Learning Objectives
At the end of this project, you are expected to be able to explain to anyone, without the help of Google:
- Examples of Personally Identifiable Information (PII)
- How to implement a log filter that will obfuscate PII fields
- How to encrypt a password and check the validity of an input password
- How to authenticate to a database using environment variables

### Requirements
- All your files will be interpreted/compiled on Ubuntu 18.04 LTS using python3 (version 3.7)
- All your files should end with a new line
- The first line of all your files should be exactly `#!/usr/bin/env python3`
- A `README.md` file, at the root of the folder of the project, is mandatory
- Your code should use the `pycodestyle` style (version 2.5)
- All your files must be executable
- The length of your files will be tested using `wc`
- All your modules should have documentation (`python3 -c 'print(__import__("my_module").__doc__)'`)
- All your classes should have documentation (`python3 -c 'print(__import__("my_module").MyClass.__doc__)'`)
- All your functions (inside and outside a class) should have documentation (`python3 -c 'print(__import__("my_module").my_function.__doc__)' and `python3 -c 'print(__import__("my_module").MyClass.my_function.__doc__)'`)
- A documentation is not a simple word, it’s a real sentence explaining what’s the purpose of the module, class, or method (the length of it will be verified)
- All your functions should be type annotated

### Tasks

#### 0. Regex-ing
- **Score:** 0.0% (Checks completed: 0.0%)
- Write a function called `filter_datum` that returns the log message obfuscated:
  - **Arguments:**
    - `fields`: a list of strings representing all fields to obfuscate
    - `redaction`: a string representing by what the field will be obfuscated
    - `message`: a string representing the log line
    - `separator`: a string representing by which character is separating all fields in the log line (message)
  - The function should use a regex to replace occurrences of certain field values.
  - `filter_datum` should be less than 5 lines long and use `re.sub` to perform the substitution with a single regex.
  - Example:
    ```python
    # Example usage
    filter_datum(["password", "date_of_birth"], 'xxx', "name=egg;email=eggmin@eggsample.com;password=eggcellent;date_of_birth=12/12/1986;", ';')
    # Output: name=egg;email=eggmin@eggsample.com;password=xxx;date_of_birth=xxx;
    ```
  - [Repo: alx-backend-user-data](#)

#### 1. Log formatter
- **Score:** 0.0% (Checks completed: 0.0%)
- Copy the given code into `filtered_logger.py` and update the class to accept a list of strings `fields` constructor argument.
- Implement the `format` method to filter values in incoming log records using `filter_datum`. Values for fields in `fields` should be filtered.
- **Note:** Do not extrapolate `FORMAT` manually. The `format` method should be less than 5 lines long.
- Example:
  ```python
  # Example usage
  RedactingFormatter = __import__('filtered_logger').RedactingFormatter
  message = "name=Bob;email=bob@dylan.com;ssn=000-123-0000;password=bobby2019;"
  log_record = logging.LogRecord("my_logger", logging.INFO, None, None, message, None, None)
  formatter = RedactingFormatter(fields=("email", "ssn", "password"))
  print(formatter.format(log_record))
  # Output: [HOLBERTON] my_logger INFO 2019-11-19 18:24:25,105: name=Bob; email=***; ssn=***; password=***;
  ```
  - [Repo: alx-backend-user-data](#)

#### 2. Create logger
- **Score:** 0.0% (Checks completed: 0.0%)
- Implement a `get_logger` function that takes no arguments and returns a `logging.Logger` object.
- The logger should be named "user_data" and only log up to `logging.INFO` level. It should not propagate messages to other loggers.
- It should have a `StreamHandler` with `RedactingFormatter` as the formatter.
- Create a tuple `PII_FIELDS` constant at the root of the module containing the fields from `user_data.csv` that are considered PII. `PII_FIELDS` can contain only 5 fields - choose the right list of fields that can are considered as “important” PIIs or information that you must hide in your logs. Use it to parameterize the formatter.
- Example:
  ```python
  # Example usage
  get_logger = __import__('filtered_logger').get_logger
  PII_FIELDS = __import__('filtered_logger').PII_FIELDS
  print(get_logger.__annotations__.get('return'))
  print("PII_FIELDS: {}".format(len(PII_FIELDS)))
  # Output: <class 'logging.Logger'> PII_FIELDS: 5
  ```
  - [Repo: alx-backend-user-data](#)

#### 3. Connect to a secure database
- **Score:** 0.0% (Checks completed: 0.0%)
- Implement a `get_db` function that returns a connector to the database (`mysql.connector.connection.MySQLConnection` object).
- Use the `os` module to obtain credentials from the environment.
- Use the module `mysql-connector-python` to connect to the MySQL database (`pip3 install mysql-connector-python`).
- Example:
  ```python
  # Example usage
  get_db = __import__('filtered_logger').get_db
  db = get_db()
  cursor = db.cursor()
  cursor.execute("SELECT COUNT(*) FROM users

;")
  for row in cursor:
      print(row[0])
  cursor.close()
  db.close()
  ```
  - [Repo: alx-backend-user-data](#)

#### 4. Read and filter data
- **Score:** 0.0% (Checks completed: 0.0%)
- Implement a `main` function that takes no arguments and returns nothing.
- The function will obtain a database connection using `get_db` and retrieve all rows in the `users` table and display each row under a filtered format.
- Example:
  ```python
  # Example usage
  # Assuming the database is already set up and populated with data
  ./filtered_logger.py
  # Output: [HOLBERTON] user_data INFO 2019-11-19 18:37:59,596: name=***; email=***; phone=***; ssn=***; password=***; ip=***; last_login=***; user_agent=***;
  Filtered fields:
  - name
  - email
  - phone
  - ssn
  - password
  ```
  - [Repo: alx-backend-user-data](#)

#### 5. Encrypting passwords
- **Score:** 0.0% (Checks completed: 0.0%)
- User passwords should NEVER be stored in plain text in a database.
- Implement a `hash_password` function that expects one string argument named `password` and returns a salted, hashed password, which is a byte string.
- Use the `bcrypt` package to perform the hashing (with `hashpw`).
- Example:
  ```python
  # Example usage
  hash_password = __import__('encrypt_password').hash_password
  password = "MyAmazingPassw0rd"
  print(hash_password(password))
  print(hash_password(password))
  ```
  - [Repo: alx-backend-user-data](#)

#### 6. Check valid password
- **Score:** 0.0% (Checks completed: 0.0%)
- Implement an `is_valid` function that expects 2 arguments and returns a boolean.
- **Arguments:**
  - `hashed_password`: bytes type
  - `password`: string type
- Use `bcrypt` to validate that the provided password matches the hashed password.
- Example:
  ```python
  # Example usage
  hash_password = __import__('encrypt_password').hash_password
  is_valid = __import__('encrypt_password').is_valid
  password = "MyAmazingPassw0rd"
  encrypted_password = hash_password(password)
  print(encrypted_password)
  print(is_valid(encrypted_password, password))
  ```
  - [Repo: alx-backend-user-data](#)

---
