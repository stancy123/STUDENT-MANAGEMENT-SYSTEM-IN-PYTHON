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
