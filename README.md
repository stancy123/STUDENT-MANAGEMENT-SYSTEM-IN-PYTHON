# STUDENT-MANAGEMENT-SYSTEM-IN-PYTHON
How to Run the System

Ensure Python is Installed: Make sure Python is installed on your system. Or any IDE which supports python.
Copy the Code: Copy the provided code into a Python file, for example, student_management_system.py.
Run the Code:
Open your terminal or command prompt.
oNavigate to the directory where your student_management_system.py file is located.
oRun the script by typing python student_management_system.py.

Interact with the Menu:

After running the script, you’ll see a menu with options to add, delete, update, view students, or exit the system.
Choose an option by typing the corresponding number and pressing Enter.
Follow the on-screen prompts to enter student details or perform other actions.
The system will continue to display the menu until you choose to exit by selecting option 5.
Explanation of Key Changes
Adherence to SOLID Principles:

Single Responsibility Principle: Each class now has a single responsibility. The Student class is solely for storing student data, StudentDatabase manages the collection of students, and StudentManagementSystem handles user interactions.
Open/Closed Principle: The system is designed to be open for extension but closed for modification. For example, adding a new type of student information would only require extending the Student class or modifying the StudentDatabase, without changing existing functionality.
oDependency Inversion Principle: StudentManagementSystem depends on the abstraction of StudentDatabase rather than a concrete implementation, making it easier to change the database implementation in the future.
Elimination of Redundancy (DRY):
oThe find_student method in StudentDatabase centralizes the logic for finding a student by id, avoiding code repetition.
Simplification (KISS):
oSimplified the update_student_info method to directly update fields if provided, making the code easier to read and maintain.
Avoiding Unnecessary Complexity (YAGNI):
Removed unnecessary iterations and complex method signatures. The use of a dictionary for storing students simplifies lookups and updates.

THE CODE


class StudentDatabase:
    def __init__(self):
        self.students = {}

    def add_student(self, student):
        self.students[student.id] = student

    def remove_student(self, student_id):
        if student_id in self.students:
            del self.students[student_id]

    def find_student(self, student_id):
        return self.students.get(student_id, None)

    def update_student(self, student_id, name=None, age=None, major=None):
        student = self.find_student(student_id)
        if student:
            if name:
                student.name = name
            if age:
                student.age = age
            if major:
                student.major = major

    def get_all_students(self):
        return list(self.students.values())
class Student:
    def __init__(self, id, name, age, major):
        self.id = id
        self.name = name
        self.age = age
        self.major = major
class StudentManagementSystem:
    def __init__(self, database):
        self.database = database

    def add_new_student(self, id, name, age, major):
        student = Student(id, name, age, major)
        self.database.add_student(student)

    def delete_student(self, student_id):
        self.database.remove_student(student_id)

    def update_student_info(self, student_id, name=None, age=None, major=None):
        self.database.update_student(student_id, name, age, major)

    def show_all_students(self):
        students = self.database.get_all_students()
        for student in students:
            self.display_student(student)

    @staticmethod
    def display_student(student):
        print(f"ID: {student.id}, Name: {student.name}, Age: {student.age}, Major: {student.major}")

def main_menu():
    system = StudentManagementSystem(StudentDatabase())
    while True:
        print("""\n

      ------------------------------------------------------
     |======================================================| 
     |======== Welcome To Student Management System	========|
     |======================================================|
      ------------------------------------------------------""")
        print("1. Add Student")
        print("2. Delete Student")
        print("3. Update Student")
        print("4. View All Students")
        print("5. Exit")
        
        choice = input("Choose an option: ")

        if choice == '1':
            id = input("Enter ID: ")
            name = input("Enter Name: ")
            age = input("Enter Age: ")
            major = input("Enter Major: ")
            system.add_new_student(id, name, age, major)
        elif choice == '2':
            id = input("Enter ID of student to delete: ")
            system.delete_student(id)
        elif choice == '3':
            id = input("Enter ID of student to update: ")
            name = input("Enter new Name (leave blank to skip): ") or None
            age = input("Enter new Age (leave blank to skip): ") or None
            major = input("Enter new Major (leave blank to skip): ") or None
            system.update_student_info(id, name, age, major)
        elif choice == '4':
            system.show_all_students()
        elif choice == '5':
            break
        else:
            print("Invalid option. Please try again.")

if __name__ == "__main__":
    main_menu()
