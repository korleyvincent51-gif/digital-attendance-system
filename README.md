#include <iostream>
#include <vector>
#include <fstream>
using namespace std;

class Student {
public:
    int id;
    string name;

    Student(int i, string n) {
        id = i;
        name = n;
    }
};

class AttendanceSession {
public:
    string date;
    vector<int> presentIDs;

    AttendanceSession(string d) {
        date = d;
    }
};

vector<Student> students;
vector<AttendanceSession> sessions;

//////////////////////////////////////////////////
// ADD STUDENT
//////////////////////////////////////////////////
void addStudent() {
    int id;
    string name;

    cout << "Enter Student ID: ";
    cin >> id;

    cin.ignore();
    cout << "Enter Student Name: ";
    getline(cin, name);

    students.push_back(Student(id, name));

    cout << "Student added successfully!\n";
}

//////////////////////////////////////////////////
// VIEW STUDENTS
//////////////////////////////////////////////////
void viewStudents() {
    if (students.size() == 0) {
        cout << "No students available.\n";
        return;
    }

    for (int i = 0; i < students.size(); i++) {
        cout << students[i].id << " - " << students[i].name << endl;
    }
}

//////////////////////////////////////////////////
// CREATE SESSION + MARK ATTENDANCE
//////////////////////////////////////////////////
void markAttendance() {
    if (students.size() == 0) {
        cout << "Add students first!\n";
        return;
    }

    string date;
    cout << "Enter session date: ";
    cin >> date;

    AttendanceSession session(date);

    for (int i = 0; i < students.size(); i++) {
        char choice;
        cout << "Is " << students[i].name << " present? (y/n): ";
        cin >> choice;

        if (choice == 'y' || choice == 'Y') {
            session.presentIDs.push_back(students[i].id);
        }
    }

    sessions.push_back(session);
    cout << "Attendance recorded!\n";
}

//////////////////////////////////////////////////
// VIEW REPORT
//////////////////////////////////////////////////
void viewReport() {
    if (sessions.size() == 0) {
        cout << "No sessions recorded.\n";
        return;
    }

    for (int i = 0; i < sessions.size(); i++) {
        cout << "\nDate: " << sessions[i].date << endl;
        cout << "Present students:\n";

        for (int j = 0; j < sessions[i].presentIDs.size(); j++) {
            cout << sessions[i].presentIDs[j] << endl;
        }
    }
}

//////////////////////////////////////////////////
// SAVE TO FILE
//////////////////////////////////////////////////
void saveData() {
    ofstream file("students.txt");

    for (int i = 0; i < students.size(); i++) {
        file << students[i].id << " " << students[i].name << endl;
    }

    file.close();
    cout << "Students saved to file.\n";
}

//////////////////////////////////////////////////
// LOAD FROM FILE
//////////////////////////////////////////////////
void loadData() {
    ifstream file("students.txt");

    students.clear();

    int id;
    string name;

    while (file >> id >> name) {
        students.push_back(Student(id, name));
    }

    file.close();
    cout << "Students loaded.\n";
}

//////////////////////////////////////////////////
// MENU
//////////////////////////////////////////////////
int main() {
    int choice;

    do {
        cout << "\n===== ATTENDANCE SYSTEM =====\n";
        cout << "1. Add Student\n";
        cout << "2. View Students\n";
        cout << "3. Mark Attendance\n";
        cout << "4. View Report\n";
        cout << "5. Save Students\n";
        cout << "6. Load Students\n";
        cout << "0. Exit\n";
        cout << "Choose: ";
        cin >> choice;

        switch(choice) {
            case 1: addStudent(); break;
            case 2: viewStudents(); break;
            case 3: markAttendance(); break;
            case 4: viewReport(); break;
            case 5: saveData(); break;
            case 6: loadData(); break;
            case 0: cout << "Goodbye!\n"; break;
            default: cout << "Invalid choice\n";
        }

    } while(choice != 0);

    return 0;
}
} digital-attendance-system
# Digital Attendance System

A simple attendance management system implemented in C++.

## Development Environment
- VS Code
- C++ Compiler 

## Author
Korley Vincent Kojo -01240218D
