# Student-grade-system
package whileloop;

import java.util.*;

public class Student_Grade_System {
    static final String[] SUBJECTS = {"Math", "Science", "English", "Computer", "History"};

    static class Student {
        int rollNumber;
        String name;
        int[] marks;

        Student(int rollNumber, String name, int[] marks) {
            this.rollNumber = rollNumber;
            this.name = name;
            this.marks = marks;
        }

        double calculateAverage() {
            int total = 0;
            for (int mark : marks) {
                total += mark;
            }
            return total / (double) marks.length;
        }

        char calculateGrade() {
            double average = calculateAverage();
            if (average >= 90) return 'A';
            else if (average >= 80) return 'B';
            else if (average >= 70) return 'C';
            else if (average >= 60) return 'D';
            else if (average >= 50) return 'E';
            else return 'F';
        }

        String getRemarks() {
            char grade = calculateGrade();
            switch (grade) {
                case 'A': return "Excellent";
                case 'B': return "Very Good";
                case 'C': return "Good";
                case 'D': return "Average";
                case 'E': return "Below Average";
                default: return "Fail";
            }
        }
    }

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.println("========================================");
        System.out.println("         STUDENT GRADE SYSTEM");
        System.out.println("========================================");
        System.out.print("Enter number of students: ");

        int totalStudents = input.nextInt();
        input.nextLine();

        if (totalStudents <= 0) {
            System.out.println("Number of students must be greater than 0.");
            input.close();
            return;
        }

        Student[] students = new Student[totalStudents];

        for (int i = 0; i < totalStudents; i++) {
            System.out.println("\nEnter details for student " + (i + 1));
            System.out.print("Name: ");
            String name = input.nextLine();

            int[] marks = new int[SUBJECTS.length];
            for (int j = 0; j < SUBJECTS.length; j++) {
                while (true) {
                    System.out.print(SUBJECTS[j] + " marks (0-100): ");
                    int mark = input.nextInt();
                    if (mark >= 0 && mark <= 100) {
                        marks[j] = mark;
                        break;
                    }
                    System.out.println("Invalid marks! Please enter a number between 0 and 100.");
                }
            }
            input.nextLine();
            students[i] = new Student(i + 1, name, marks);
        }

        displayReport(students);
        input.close();
    }

    static void displayReport(Student[] students) {
        System.out.println("\n========================================");
        System.out.println("           STUDENT REPORT");
        System.out.println("========================================");
        System.out.println("Roll No\tName\t\tMath\tScience\tEnglish\tComputer\tHistory\tAverage\tGrade\tRemarks");

        Student topper = students[0];

        for (Student student : students) {
            double average = student.calculateAverage();
            char grade = student.calculateGrade();

            if (average > topper.calculateAverage()) {
                topper = student;
            }

            System.out.printf("%d\t%s\t", student.rollNumber, student.name);
            for (int m : student.marks) {
                System.out.printf("%d\t", m);
            }
            System.out.printf("%.2f\t%c\t%s\n", average, grade, student.getRemarks());
        }

        System.out.println("\n========================================");
        System.out.println("             TOPPER DETAILS");
        System.out.println("========================================");
        System.out.println("Roll No : " + topper.rollNumber);
        System.out.println("Name    : " + topper.name);
        System.out.printf("Average : %.2f%n", topper.calculateAverage());
        System.out.println("Grade   : " + topper.calculateGrade());
        System.out.println("Remarks : " + topper.getRemarks());
    }
}
