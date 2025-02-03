import java.util.ArrayList;
import java.util.InputMismatchException;
import java.util.List;
import java.util.Scanner;

class Employee {
    int employeeID;
    String name;
    String designation;
    double salary;

    public Employee(int employeeID, String name, String designation, double salary) {
        this.employeeID = employeeID;
        this.name = name;
        this.designation = designation;
        this.salary = salary;
    }

    // Method to update salary
    public void updateSalary(double newSalary) {
        this.salary = newSalary;
    }

    @Override
    public String toString() {
        return "ID: " + employeeID + ", Name: " + name + ", Designation: " + designation + ", Salary: " + salary;
    }
}

public class Main {

    // List to store employees
    private static List<Employee> employees = new ArrayList<>();

    // Method to add an employee
    public static void addEmployee(int employeeID, String name, String designation, double salary) {
        Employee newEmployee = new Employee(employeeID, name, designation, salary);
        employees.add(newEmployee);
        System.out.println("Employee added: " + newEmployee);
    }

    // Method to update employee salary
    public static void updateSalary(int employeeID, double newSalary) {
        for (Employee employee : employees) {
            if (employee.employeeID == employeeID) {
                employee.updateSalary(newSalary);
                System.out.println("Updated salary for Employee ID " + employeeID + ": " + employee);
                return;
            }
        }
        System.out.println("Employee with ID " + employeeID + " not found.");
    }

    // Method to view employee details
    public static void viewEmployeeDetails(int employeeID) {
        for (Employee employee : employees) {
            if (employee.employeeID == employeeID) {
                System.out.println(employee);
                return;
            }
        }
        System.out.println("Employee with ID " + employeeID + " not found.");
    }

    // Method to list all employees
    public static void listEmployees() {
        if (employees.isEmpty()) {
            System.out.println("No employees in the system.");
        } else {
            System.out.println("List of Employees:");
            for (Employee employee : employees) {
                System.out.println(employee);
            }
        }
    }

    // Main method with menu
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\nEmployee Management System:");
            System.out.println("1. Add Employee");
            System.out.println("2. Update Employee Salary");
            System.out.println("3. View Employee Details");
            System.out.println("4. List All Employees");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            int choice;
            try {
                choice = scanner.nextInt();
            } catch (InputMismatchException e) {
                System.out.println("Invalid input. Please enter a number between 1 and 5.");
                scanner.next(); // Clear invalid input
                continue;
            }
            scanner.nextLine(); // Consume the newline character

            switch (choice) {
                case 1:
                    try {
                        System.out.print("Enter Employee ID: ");
                        int employeeID = scanner.nextInt();
                        scanner.nextLine(); // Consume newline
                        System.out.print("Enter Name: ");
                        String name = scanner.nextLine();
                        System.out.print("Enter Designation: ");
                        String designation = scanner.nextLine();
                        System.out.print("Enter Salary: ");
                        double salary = scanner.nextDouble();
                        scanner.nextLine(); // Consume newline
                        addEmployee(employeeID, name, designation, salary);
                    } catch (InputMismatchException e) {
                        System.out.println("Invalid input. Please try again.");
                        scanner.nextLine(); // Clear the invalid input
                    }
                    break;

                case 2:
                    try {
                        System.out.print("Enter Employee ID to update salary: ");
                        int updateID = scanner.nextInt();
                        System.out.print("Enter New Salary: ");
                        double newSalary = scanner.nextDouble();
                        scanner.nextLine(); // Consume newline
                        updateSalary(updateID, newSalary);
                    } catch (InputMismatchException e) {
                        System.out.println("Invalid input. Please try again.");
                        scanner.nextLine();
                    }
                    break;

                case 3:
                    try {
                        System.out.print("Enter Employee ID to view details: ");
                        int viewID = scanner.nextInt();
                        scanner.nextLine(); // Consume newline
                        viewEmployeeDetails(viewID);
                    } catch (InputMismatchException e) {
                        System.out.println("Invalid input. Please try again.");
                        scanner.nextLine();
                    }
                    break;

                case 4:
                    listEmployees();
                    break;

                case 5:
                    System.out.println("Exiting system...");
                    scanner.close();
                    return;

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
