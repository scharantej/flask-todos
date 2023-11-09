 ### Problem

Design a Flask application that allows users to create and manage a todo list.

### Design

The application will consist of the following HTML files:

* `index.html`: The main page of the application. This page will display the user's todo list and allow them to add new tasks.
* `add_task.html`: A page that allows the user to add a new task to their todo list.
* `edit_task.html`: A page that allows the user to edit a task on their todo list.
* `delete_task.html`: A page that allows the user to delete a task from their todo list.

The application will also have the following routes:

* `/`: The main page of the application.
* `/add_task`: A route that handles the addition of a new task to the user's todo list.
* `/edit_task/<int:task_id>`: A route that handles the editing of a task on the user's todo list.
* `/delete_task/<int:task_id>`: A route that handles the deletion of a task from the user's todo list.

### Implementation

The following code is the implementation of the Flask application:

```python
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

tasks = []

@app.route("/")
def index():
    return render_template("index.html", tasks=tasks)

@app.route("/add_task", methods=["GET", "POST"])
def add_task():
    if request.method == "POST":
        task = request.form.get("task")
        tasks.append(task)
        return redirect(url_for("index"))
    return render_template("add_task.html")

@app.route("/edit_task/<int:task_id>", methods=["GET", "POST"])
def edit_task(task_id):
    if request.method == "POST":
        task = request.form.get("task")
        tasks[task_id] = task
        return redirect(url_for("index"))
    return render_template("edit_task.html", task_id=task_id, task=tasks[task_id])

@app.route("/delete_task/<int:task_id>")
def delete_task(task_id):
    tasks.pop(task_id)
    return redirect(url_for("index"))

if __name__ == "__main__":
    app.run(debug=True)
```