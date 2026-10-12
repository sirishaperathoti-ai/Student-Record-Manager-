import re

FILE_NAME = "students.txt"

def add_student():
    try:
        name = input("Enter student name: ")
        email = input("Enter student email: ")

        if not re.match(r"^[\w.-]+@[\w.-]+\.\w+$", email):
            print("Invalid email address!")
            return

        with open(FILE_NAME, "a") as file:
            file.write(f"{name},{email}\n")

        print("Student added successfully!")

    except Exception as error:
        print("Error:", error)


def view_students():
    try:
        with open(FILE_NAME, "r") as file:
            records = file.readlines()

        if not records:
            print("No student records found.")
            return

        print("\nStudent Records:")
        for record in records:
            print(record.strip())

    except FileNotFoundError:
        print("No records found yet. Add a student first.")


while True:
    print("\n===== STUDENT RECORD MANAGER =====")
    print("1. Add Student")
    print("2. View Students")
    print("3. Exit")

    try:
        choice = input("Enter your choice: ")

        if choice == "1":
            add_student()
        elif choice == "2":
            view_students()
        elif choice == "3":
            print("Thank you!")
            break
        else:
            print("Invalid choice. Enter 1, 2, or 3.")

    except Exception as error:
        print("Error:", error)
