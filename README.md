# Install the necessary libraries (e.g., Flask, SQLAlchemy) if not already installed

from flask import Flask, request
from flask_sqlalchemy import SQLAlchemy

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///time_management.db'
db = SQLAlchemy(app)

# Define the Task model
class Task(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(100), nullable=False)
    description = db.Column(db.Text)
    deadline = db.Column(db.DateTime)
    status = db.Column(db.String(20))

# Define the Appointment model
class Appointment(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(100), nullable=False)
    description = db.Column(db.Text)
    start_time = db.Column(db.DateTime)
    end_time = db.Column(db.DateTime)

# Define the API routes for CRUD operations

@app.route('/tasks', methods=['GET'])
def get_tasks():
    # Retrieve all tasks from the database
    tasks = Task.query.all()
    # Convert tasks to a list of dictionaries for JSON serialization
    tasks_data = [{'id': task.id, 'title': task.title, 'description': task.description, 'deadline': task.deadline, 'status': task.status} for task in tasks]
    return {'tasks': tasks_data}

@app.route('/tasks/<task_id>', methods=['GET'])
def get_task(task_id):
    # Retrieve a specific task by its ID from the database
    task = Task.query.get(task_id)
    if task:
        task_data =
