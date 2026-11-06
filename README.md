#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Student {
private:
    int id;
    string name;
    double grade;

public:
    Student(int sId, string sName, double sGrade) {
        id = sId;
        name = sName;
        grade = sGrade;
    }

    int getId() const { return id; }
    string getName() const { return name; }
    double getGrade() const { return grade; }

    void displayStudent() const {
        cout << "ID: " << id << " | Name: " << name << " | Grade: " << grade << endl;
    }
};

class StudentManagementSystem {
private:
    vector<Student> students;

public:
    void addStudent(int id, string name, double grade) {
        Student newStudent(id, name, grade);
        students.push_back(newStudent);
        cout << "Student added successfully!\n";
    }

    void displayAllStudents() const {
        if (students.empty()) {
            cout << "No students found.\n";
            return;
        }
        cout << "\n--- Student List ---\n";
        for (const auto& student : students) {
            student.displayStudent();
        }
    }

    void searchStudent(int id) const {
        for (const auto& student : students) {
            if (student.getId() == id) {
                cout << "\nStudent Found:\n";
                student.displayStudent();
                return;
            }
        }
        cout << "Student with ID " << id << " not found.\n";
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
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
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
            cout << "Exiting system. Goodbye!\n";
        } else {
            cout << "Invalid choice! Try again.\n";
        }
    } while (choice != 4);

    return 0;
}
