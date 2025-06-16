import json
from datetime import datetime, timedelta

# Function to load tasks from a JSON file
def load_tasks():
    try:
        with open('tasks.json', 'r') as file:
            tasks = json.load(file)
    except FileNotFoundError:
        tasks = []
    return tasks

# Function to save tasks to a JSON file
def save_tasks(tasks):
    with open('tasks.json', 'w') as file:
        json.dump(tasks, file, indent=4)

# Function to display all tasks
def display_tasks(tasks, filter_type=None):
    if filter_type == "completed":
        tasks = [task for task in tasks if task['status'] == 'completed']
    elif filter_type == "pending":
        tasks = [task for task in tasks if task['status'] == 'pending']
    elif filter_type == "due_soon":
        today = datetime.today()
        tasks = [task for task in tasks if task['due_date'] and (datetime.strptime(task['due_date'], "%Y-%m-%d") - today).days <= 3]

    if tasks:
        for i, task in enumerate(tasks, 1):
            print(f"{i}. {task['description']} (Due: {task['due_date']}) - {task['status']}")
    else:
        print("No tasks to display.")

# Function to add a new task
def add_task(tasks):
    description = input("Enter task description: ")
    due_date = input("Enter due date (YYYY-MM-DD) or press Enter to skip: ")
    due_date = due_date if due_date else None
    task = {
        'description': description,
        'due_date': due_date,
        'status': 'pending'
    }
    tasks.append(task)
    save_tasks(tasks)
    print("Task added successfully.")

# Function to mark a task as completed
def mark_task_completed(tasks):
    task_id = int(input("Enter task number to mark as completed: ")) - 1
    if 0 <= task_id < len(tasks):
        tasks[task_id]['status'] = 'completed'
        save_tasks(tasks)
        print("Task marked as completed.")
    else:
        print("Invalid task number.")

# Function to edit a task
def edit_task(tasks):
    task_id = int(input("Enter task number to edit: ")) - 1
    if 0 <= task_id < len(tasks):
        print(f"Current task: {tasks[task_id]['description']} (Due: {tasks[task_id]['due_date']})")
        description = input("Enter new description (leave blank to keep current): ")
        if description:
            tasks[task_id]['description'] = description
        due_date = input("Enter new due date (YYYY-MM-DD) or press Enter to keep current: ")
        if due_date:
            tasks[task_id]['due_date'] = due_date
        save_tasks(tasks)
        print("Task updated successfully.")
    else:
        print("Invalid task number.")

# Function to delete a task
def delete_task(tasks):
    task_id = int(input("Enter task number to delete: ")) - 1
    if 0 <= task_id < len(tasks):
        tasks.pop(task_id)
        save_tasks(tasks)
        print("Task deleted successfully.")
    else:
        print("Invalid task number.")

# Function to display the main menu and handle user input
def main():
    tasks = load_tasks()

    while True:
        print("\nTo-Do List Manager")
        print("1. Add a new task")
        print("2. View all tasks")
        print("3. View completed tasks")
        print("4. View pending tasks")
        print("5. View tasks due soon")
        print("6. Mark a task as completed")
        print("7. Edit a task")
        print("8. Delete a task")
        print("9. Exit")

        choice = input("Choose an option: ")

        if choice == '1':
            add_task(tasks)
        elif choice == '2':
            display_tasks(tasks)
        elif choice == '3':
            display_tasks(tasks, filter_type="completed")
        elif choice == '4':
            display_tasks(tasks, filter_type="pending")
        elif choice == '5':
            display_tasks(tasks, filter_type="due_soon")
        elif choice == '6':
            mark_task_completed(tasks)
        elif choice == '7':
            edit_task(tasks)
        elif choice == '8':
            delete_task(tasks)
        elif choice == '9':
            print("Exiting...")
            break
        else:
            print("Invalid choice, please try again.")

if __name__ == '__main__':
    main()
