# Midterm Project: Enhanced Calculator Command-Line Application

Initialize Git Repository:

Ensure your Git repository is properly initialized and pushed to GitHub.
Directory Structure: Organize your project with a well-structured directory layout as follows:
project_root/
├── app/
│   ├── __init__.py
│   ├── calculator.py
│   ├── calculation.py
│   ├── calculator_config.py
│   ├── calculator_memento.py
│   ├── exceptions.py
│   ├── history.py
│   ├── input_validators.py
│   ├── operations.py
│   └── logger.py
├── tests/
│   ├── __init__.py
│   ├── test_calculator.py
│   ├── test_calculation.py
│   ├── test_operations.py
│   └── ...
├── .env
├── requirements.txt
├── README.md
└── .github/
    └── workflows/
        └── python-app.yml
Virtual Environment:

Create and activate a virtual environment for your project.
Example using venv:
python3 -m venv venv
source venv/bin/activate
Install Dependencies:

Ensure all necessary packages are listed in requirements.txt.
Install dependencies using:
pip install -r requirements.txt
Git Usage:

Commit your changes regularly with clear and descriptive commit messages to track your progress.
Use branches for feature development if necessary.
Ensure that your Git history reflects the development process, which will be part of your grade.
IMPORTANT: YOU MUST HAVE A CLEAR COMMIT HISTORY OF YOUR PROGRESS. PROJECTS WITHOUT A CLEAR COMMIT HISTORY AS JUDGED BY THE INSTRUCTOR WILL BE FLAGGED AS A POSSIBLE ACADEMIC INTEGRITY VIOLATION
Application Development:
Enhance the calculator application with the following features:

Additional Arithmetic Operations:

Mandatory Operations:
Power: Raise one number to the power of another.
Root: Calculate the nth root of a number.
Modulus: Compute the remainder of the division of two numbers.
Integer Division: Perform division that results in an integer quotient, discarding any fractional part.
Percentage Calculation: Calculate the percentage of one number with respect to another (e.g., Percentage(a, b) computes (a / b) * 100).
Absolute Difference: Calculate the absolute difference between two numbers.
Implementation Details:
Utilize the Factory Design Pattern to manage the creation of different operation instances.
Ensure that each operation takes exactly two numerical inputs and returns the correct result.
Handle invalid operations gracefully with appropriate error messages.
History Management with Undo/Redo:

Implement Undo and Redo functionalities using the Memento Design Pattern.
Allow users to revert the last calculation or redo an undone calculation.
Ensure that the history stack accurately reflects the state after each operation.
Observer Pattern for Logging and Auto-Save:

Implement the Observer Design Pattern to allow observers to respond to new calculations.
Observers to Implement:
LoggingObserver: Logs each calculation with details (operation, operands, result) to a log file.
AutoSaveObserver: Automatically saves the calculation history to a CSV file using pandas whenever a new calculation is performed.
Ensure that observers are registered with the Calculator and respond appropriately to events.
Configuration Management:

Manage configuration settings using a .env file and the python-dotenv package.
Configuration Parameters:
Base Directories:
CALCULATOR_LOG_DIR: Directory for log files.
CALCULATOR_HISTORY_DIR: Directory for history files.
History Settings:
CALCULATOR_MAX_HISTORY_SIZE: Maximum number of history entries.
CALCULATOR_AUTO_SAVE: Whether to auto-save history (true or false).
Calculation Settings:
CALCULATOR_PRECISION: Number of decimal places for calculations.
CALCULATOR_MAX_INPUT_VALUE: Maximum allowed input value.
CALCULATOR_DEFAULT_ENCODING: Default encoding for file operations.
Implementation Details:
Use python-dotenv to load environment variables from the .env file.
Ensure that the application can load and validate these configurations on startup.
Provide default values for configurations if environment variables are not set.
Error Handling and Input Validation:

Implement robust error handling using custom exceptions (OperationError, ValidationError, etc.).
Validate user inputs to ensure they are numerical and within allowed ranges.
Use pandas to manage data-related errors, such as issues with reading or writing CSV files.
Provide meaningful error messages to guide the user in correcting their input.
Logging:

Implement comprehensive logging strategies using Python’s logging module.
Log important events, errors, and calculation details with appropriate logging levels (INFO, WARNING, ERROR).
Configure logging to write to a file specified in the configuration (CALCULATOR_LOG_FILE).
Ensure that all new operations are logged appropriately using the existing Logger class.
Command-Line Interface (REPL):

Develop a user-friendly command-line interface using the Read-Eval-Print Loop (REPL) pattern.
Supported Commands:
add, subtract, multiply, divide, power, root, modulus, int_divide, percent, abs_diff – Perform calculations.
history – Display calculation history.
clear – Clear calculation history.
undo – Undo the last calculation.
redo – Redo the last undone calculation.
save – Manually save calculation history to file using pandas.
load – Load calculation history from file using pandas.
help – Display available commands.
exit – Exit the application gracefully.
Unit Testing:

Write comprehensive unit tests using pytest for all new functionalities.
Cover typical use cases and edge cases (e.g., division by zero, negative exponents).
Implement parameterized tests to efficiently cover multiple scenarios.
Achieve 90% Test Coverage or Better using tools like pytest-cov.
Handling Coverage Exceptions: Use coverage comments (e.g., # pragma: no cover) for lines that are intentionally excluded from coverage metrics.
Serialization and Data Persistence:

Saving History:
Use pandas to serialize calculation history to a CSV file.
Implement a method to convert the history (a list of Calculation instances) into a pandas DataFrame and save it to the file specified in the configuration (CALCULATOR_HISTORY_FILE).
Ensure that the CSV file includes columns for operation, operands, result, and timestamp.
Loading History:
Use pandas to deserialize calculation history from a CSV file.
Implement a method to read the CSV file into a pandas DataFrame and convert each row back into a Calculation instance.
Handle cases where the CSV file does not exist or is malformed gracefully, providing appropriate error messages.
GitHub Actions for Continuous Integration (CI):

Set up GitHub Actions to automatically run your tests and measure test coverage on each push or pull request to the main branch.
Workflow Requirements:
Check Out Code: Use actions/checkout to access the repository.
Set Up Python Environment: Use actions/setup-python to specify the Python version.
Install Dependencies: Install all required packages from requirements.txt.
Run Tests: Execute pytest with coverage measurement using pytest-cov.
Enforce Coverage Threshold: Ensure that the CI pipeline fails if test coverage falls below 90%.
Example Workflow File (.github/workflows/python-app.yml):
name: Python application

on:
  push:
    branches:
      - main  # Run tests on any push to the main branch
  pull_request:
    branches:
      - main  # Run tests on any pull request to the main branch

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Check out the code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'  # Set your desired Python version

      - name: Install dependencies from requirements.txt
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
          pip install pytest pytest-cov  # Ensure pytest-cov is installed

      - name: Run tests with pytest and enforce 90% coverage
        run: |
          pytest --cov=app --cov-fail-under=90
Handling Coverage Exceptions: In your code, add comments like # pragma: no cover to lines that are intentionally excluded from coverage metrics (e.g., lines with pass or continue). This ensures that your coverage report accurately reflects the test coverage without being penalized for these lines.
if some_condition:
    pass  # pragma: no cover
Documentation:

Create a detailed README.md file with setup and usage instructions.
README.md Should Include:
Project Description: Overview of the calculator application and its features.
Installation Instructions: Steps to set up the virtual environment and install dependencies.
Configuration Setup: Instructions on creating and configuring the .env file with necessary environment variables.
Usage Guide: Detailed explanation of how to use the command-line interface and its supported commands.
Testing Instructions: How to run unit tests and check test coverage.
CI/CD Information: Overview of GitHub Actions workflow and its purpose.
Document your code with meaningful comments and docstrings to enhance readability and maintainability.
Include instructions on setting up .env files and configuring logging.
Best Practices:
DRY Principle: Apply the DRY (Don't Repeat Yourself) principle and other best practices to ensure your code is maintainable and efficient.
Modular Design: Organize your code into modules and classes to enhance readability and reusability.
Logging: Ensure that all new operations are logged appropriately using the existing Logger class.