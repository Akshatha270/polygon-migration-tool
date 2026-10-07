# Polygon Migration Tool

A Django-based migration tool for fetching competitive programming problems from Codeforces Polygon and migrating problem data and test cases to PostgreSQL and Azure Blob Storage.

## Features

- Fetch problem statements from Polygon using the Polygon API
- Fetch reference solutions and test cases
- Store problem information in PostgreSQL
- Store test cases in Azure Blob Storage
- Assign difficulty levels and problem tags
- Preview problem details and test cases through a web interface
- Support authenticated access through the Django application

## Technology Stack

- Python
- Django
- PostgreSQL
- Microsoft Azure Blob Storage
- Codeforces Polygon API
- HTML, CSS, JavaScript
- Python dotenv

## Migration Flow

```text
Codeforces Polygon
        |
        | Polygon API
        v
Polygon Migration Tool
        |
        +--------------------+
        |                    |
        v                    v
   PostgreSQL          Azure Blob Storage
 Problem Metadata       Test Cases
 Solutions              Input / Output
 Tags & Difficulty

 Main Features
1. Polygon Problem Fetching
The application accepts a Polygon problem ID and retrieves:
- Problem statement
- Problem metadata
- Reference solution
- Test cases
- Checker information
2. Problem Migration
The user can select:
- Difficulty level
- Problem tags
The selected problem is then stored in PostgreSQL.
3. Test Case Migration
Test cases are migrated to Azure Blob Storage.
The storage structure is organized by problem and test case.
test_cases/
└── <problem_id>/
    ├── <test_number>
    └── <test_number>.a

4. Verification
The application allows the migrated problem and test cases to be verified after migration.
Database
PostgreSQL is used to store problem-related information such as:
- Polygon problem ID
- Problem title
- Problem statement
- Difficulty
- Tags
- Reference solution
- Test case information
Azure Blob Storage
Microsoft Azure Blob Storage is used for storing test case input and output files.
The test cases are organized using a problem-specific folder structure.
Example Problem
The application was tested using a simple Sum of Two Numbers problem created in Polygon.
Reference Solution
The problem reads two integers and outputs their sum.
Test Cases
The migration was tested with 14 test cases, including:
- Positive numbers
- Negative numbers
- Zero values
- Mixed positive and negative values
- Large integer values
Migration Result
The migration was successfully verified with:
- 1 problem stored in PostgreSQL
- 14 test cases stored in the database
- 14 input/output test case pairs stored in Azure Blob Storage
- Reference solution successfully retrieved from Polygon


Project Structure
PolygonMigration/
│
├── PolygonMigration/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── problems/
│   ├── models.py
│   ├── views.py
│   ├── polygon_api.py
│   ├── AzureTestcase.py
│   ├── urls.py
│   └── templates/
│
├── contents/
│   ├── models.py
│   ├── views.py
│   └── migrations/
│
├── users/
│   ├── models.py
│   ├── views.py
│   ├── backends.py
│   └── templates/
│
├── manage.py
└── .gitignore

Setup
1. Clone the repository
git clone https://github.com/Akshatha270/polygon-migration-tool.git
cd polygon-migration-tool

2. Create a virtual environment
python -m venv venv

For Windows:
venv\Scripts\activate

3. Install dependencies
pip install -r requirements.txt

4. Configure environment variables
Create a .env file in the project directory and configure the required:
- PostgreSQL settings
- Polygon API credentials
- Azure Blob Storage settings
Do not commit the .env file or any credentials to GitHub.
5. Run Django migrations
python manage.py migrate

6. Create a superuser
python manage.py createsuperuser

7. Start the Django application
python manage.py runserver

The application can then be accessed at:
http://127.0.0.1:8000/

Security
Sensitive configuration such as API keys, database passwords, Azure credentials, and client secrets are stored in environment variables.
The .env file is excluded from Git using .gitignore