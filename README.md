# FILEPATH

"""
This code snippet demonstrates the installation of Python, creating a virtual environment, installing libraries, and creating a Django web application.

Installation Steps for Python (Latest Version) on Windows:
1. Visit the official Python website at https://www.python.org/downloads/ and download the latest version of Python for Windows.
2. Run the downloaded installer and follow the installation wizard.
3. Make sure to check the option "Add Python to PATH" during the installation process.
4. Verify the installation by opening the command prompt and running the command "python --version".

Installation Steps for Python (Latest Version) on Linux:
1. Open the terminal and run the following command to update the package list: 
    sudo apt update
2. Install Python by running the following command:
    sudo apt install python3
3. Verify the installation by running the command "python3 --version" in the terminal.

Creating a Virtual Environment:
1. Open the command prompt or terminal.
2. Navigate to the project directory using the "cd" command.
3. Run the following command to create a virtual environment:
    python -m venv myenv
4. Activate the virtual environment:
    - On Windows: Run the command "myenv\Scripts\activate".
    - On Linux: Run the command "source myenv/bin/activate".

Installing Libraries:
1. Activate the virtual environment.
2. Use the package manager "pip" to install libraries. For example:
    pip install django

Creating a Django Web Application:
1. Activate the virtual environment.
2. Navigate to the project directory.
3. Run the following command to create a new Django project:
    django-admin startproject myproject
4. Change to the project directory:
    cd myproject
5. Run the following command to start the development server:
    python manage.py runserver
6. Open a web browser and visit http://localhost:8000 to see your Django web application.

Note: Make sure to replace "myenv" with the desired name for your virtual environment, and "myproject" with the desired name for your Django project.
"""
