#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Base Class demonstrating Inheritance & Abstraction
class Person {
protected:
    int id;
    string name;

public:
    // Constructor
    Person(int pId, string pName) : id(pId), name(pName) {}

    // Destructor
    virtual ~Person() {}

    // Virtual Function for Polymorphism
    virtual void displayInfo() const {
        cout << "ID: " << id << " | Name: " << name;
    }

    // Getters
    int getId() const { return id; }
    string getName() const { return name; }
};

// Derived Class demonstrating Inheritance & Polymorphism
class Student : public Person {
private:
    double grade;

public:
    // Constructor using Base Class Constructor
    Student(int sId, string sName, double sGrade) 
        : Person(sId, sName), grade(sGrade) {}

    // Destructor
    ~Student() override {}

    // Getter for Grade
    double getGrade() const { return grade; }

    // Overriding Virtual Function (Polymorphism)
    void displayInfo() const override {
        Person::displayInfo();
        cout << " | Grade: " << grade << endl;
    }
};

// Management Class
class StudentManagementSystem {
private:
    vector<Student> students;

public:
    // Add Student
    void addStudent(int id, string name, double grade) {
        students.push_back(Student(id, name, grade));
        cout << "-> Student added successfully!\n";
    }

    // Display All Students
    void displayAllStudents() const {
        if (students.empty()) {
            cout << "-> No students found in the system.\n";
            return;
        }
        cout << "\n--- All Registered Students ---\n";
        for (const auto& student : students) {
            student.displayInfo(); // Polymorphic call
        }
    }

    // Function Overloading 1: Search by ID (int)
    void searchStudent(int id) const {
        for (const auto& student : students) {
            if (student.getId() == id) {
                cout << "\n[Student Found by ID]:\n";
                student.displayInfo();
                return;
            }
        }
        cout << "-> Student with ID " << id << " not found.\n";
    }

    // Function Overloading 2: Search by Name (string)
    void searchStudent(const string& name) const {
        for (const auto& student : students) {
            if (student.getName() == name) {
                cout << "\n[Student Found by Name]:\n";
                student.displayInfo();
                return;
            }
        }
        cout << "-> Student with Name '" << name << "' not found.\n";
    }
};

int main() {
    StudentManagementSystem system;
    int choice;

    do {
        cout << "\n====================================\n";
        cout << "   Student Management System (C++)  \n";
        cout << "====================================\n";
        cout << "1. Add Student\n";
        cout << "2. Display All Students\n";
        cout << "3. Search Student by ID\n";
        cout << "4. Search Student by Name\n";
        cout << "5. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        if (choice == 1) {
            int id;
            string name;
            double grade;
            cout << "Enter Student ID: ";
            cin >> id;
            cout << "Enter Student Name: ";
            cin.ignore();
            getline(cin, name);
            cout << "Enter Student Grade: ";
            cin >> grade;
            system.addStudent(id, name, grade);
        } else if (choice == 2) {
            system.displayAllStudents();
        } else if (choice == 3) {
            int id;
            cout << "Enter Student ID to search: ";
            cin >> id;
            system.searchStudent(id);
        } else if (choice == 4) {
            string name;
            cout << "Enter Student Name to search: ";
            cin.ignore();
            getline(cin, name);
            system.searchStudent(name);
        } else if (choice == 5) {
            cout << "Exiting system. Goodbye!\n";
        } else {
            cout << "Invalid choice! Try again.\n";
        }
    } while (choice != 5);

    return 0;
}
