# Internship#codingsamurai
// internship.cpp : main project file.

#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct Student {
    char studentname[50];
    int Registration_num;
    char departmentname[50];
    double gpa;
    double assignmentmarks;
    double quizmarks;
    double exammarks;
    double totalmarks;
    string Grade;
    string Comment; // Changed from char to string
};

// Function to calculate overall marks in a subject
double overallmarks(double assignmentweightage, double quizweightage, double examweightage, double assignmentmarks, double quizmarks, double exammarks) 
{
    return (assignmentweightage * assignmentmarks + quizweightage * quizmarks + examweightage * exammarks);
}

// Function to calculate GPA based on total marks
double calculateGPA(double totalmarks) 
{
    double gpa;
    // Your GPA calculation logic here
    if (totalmarks >= 80) {
        gpa = 4.00;
    } else if (totalmarks >= 72) {
        gpa = 3.5;
    } else if (totalmarks >= 65) {
        gpa = 3;
    } else if (totalmarks >= 60) {
        gpa = 2.5;
    } else if (totalmarks >= 55) {
        gpa = 2;
    } else if (totalmarks >= 50) {
        gpa = 1.5;
    } else {
        gpa = 1;
    }

    return gpa;
}

string grade(double gpa)
{
    if (gpa >= 80)
        return "A+";
    else if (gpa >= 70)
        return "A";
    else if (gpa >= 60)
        return "B";
    else if (gpa >= 55)
        return "C";
    else if (gpa >= 50)
        return "D";
    else
        return "F";
}

string comment(string Grade)
{
    if (Grade == "A+")
        return "EXCELLENT";
    else if (Grade == "B")
        return "FAIR";
    else if (Grade == "C")
        return "AVERAGE";
    else if (Grade == "D")
        return "POOR";
    else if (Grade == "F")
        return "FAIL";
    else
        return ""; // You may want to handle other cases here
}

int main() 
{
    int studentnum;
    cout << "Enter the number of students: ";
    cin >> studentnum;
    
    vector<Student> students;

    for (int i = 0; i < studentnum; i++) {
        Student student;
        
        // Input student details
        cin.ignore(); // Clear the newline character from the previous input
        cout << "Enter student name: ";
        cin.getline(student.studentname, sizeof(student.studentname));
        cout << "Enter student ID: ";
        cin >> student.Registration_num;
        cin.ignore(); // Clear the newline character from the previous input
        cout << "Enter department name: ";
        cin.getline(student.departmentname, sizeof(student.departmentname));
        
        // Input scores
        cout << "Enter assignment marks: ";
        cin >> student.assignmentmarks;
        cout << "Enter quiz marks: ";
        cin >> student.quizmarks;
        cout << "Enter exam marks: ";
        cin >> student.exammarks;
        
        // Calculate overall marks
        double assignmentWeightage = 0.3; // You need to set the correct weightages
        double quizWeightage = 0.2;
        double examWeightage = 0.5;
        student.totalmarks = overallmarks(assignmentWeightage, quizWeightage, examWeightage, student.assignmentmarks, student.quizmarks, student.exammarks);
        
        // Calculate GPA and assign grade and comment
        student.gpa = calculateGPA(student.totalmarks);
        student.Grade = grade(student.gpa);
        student.Comment = comment(student.Grade);
        
        // Add the student to the vector
        students.push_back(student);
        
        cout << "Student Name: " << student.studentname << endl;
        cout << "Student ID: " << student.Registration_num << endl;
        cout << "Department Name: " << student.departmentname << endl;
        cout << "Overall Marks: " << student.totalmarks << endl;
        cout << "GPA: " << student.gpa << endl;
        cout << "Grade: " << student.Grade << endl;
        cout << "Comment: " << student.Comment << endl;
        cout << "-------------------------------------------" << endl;
    }
    
    system("pause");
    return 0;
}