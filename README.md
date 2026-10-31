package studentmanagement;

import java.util.Scanner;

/**
 * Main entry point for the Student Management System.
 * Demonstrates: Scanner, do-while loop, switch statement, try-catch
 */
public class Main {

    public static void main(String[] args) {

        Scanner        sc      = new Scanner(System.in);
        StudentService service = new StudentService(sc);

        printWelcome();

        // Load previously saved records from file
        service.loadStudents();

        int choice = 0;

        do {
            printMenu(service.getStudentCount());

            try {
                choice = Integer.parseInt(sc.nextLine().trim());
            } catch (NumberFormatException e) {
                System.out.println("\n  ⚠ Please enter a valid menu number (1-7)!");
                continue;   // restart the loop without executing the switch
            }

            switch (choice) {
                case 1 -> service.addStudent();
                case 2 -> service.viewStudents();
                case 3 -> service.searchStudent();
                case 4 -> service.updateStudent();
                case 5 -> service.deleteStudent();
                case 6 -> service.showStatistics();
                case 7 -> System.out.println("\n  👋 Thank you for using SMS! Goodbye!\n");
                default -> System.out.println("\n  ⚠ Invalid choice! Please select 1–7.");
            }

        } while (choice != 7);

        sc.close();
    }

    // ── UI helpers ─────────────────────────────────────────────────────────────

    private static void printWelcome() {
        System.out.println();
        System.out.println("  ╔══════════════════════════════════════════╗");
        System.out.println("  ║     STUDENT MANAGEMENT SYSTEM  v1.0     ║");
        System.out.println("  ║         Core Java Console App            ║");
        System.out.println("  ╚══════════════════════════════════════════╝");
        System.out.println();
    }

    private static void printMenu(int count) {
        System.out.println("\n  ┌─────────────────────────────────────────┐");
        System.out.printf ("  │  MAIN MENU          [%3d student(s)]    │%n", count);
        System.out.println("  ├─────────────────────────────────────────┤");
        System.out.println("  │   1. ➕  Add Student                    │");
        System.out.println("  │   2. 📋  View All Students              │");
        System.out.println("  │   3. 🔍  Search Student by ID           │");
        System.out.println("  │   4. ✏️   Update Student                │");
        System.out.println("  │   5. 🗑️   Delete Student               │");
        System.out.println("  │   6. 📊  Class Statistics               │");
        System.out.println("  │   7. 🚪  Exit                          │");
        System.out.println("  └─────────────────────────────────────────┘");
        System.out.print  ("  Enter Your Choice: ");
    }
}
