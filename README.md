# Employee Management System

## Table of Contents
- [Project Description](#project-description)
- [Project Features](#project-features)
- [Key Concepts](#key-concepts)
- [Project Structure](#project-structure)
- [File Descriptions](#file-descriptions)
  - [Employee.h and Employee.cpp](#employeeh-and-employeecpp)
  - [FullTimeEmployee.h and FullTimeEmployee.cpp](#fulltimeemployeeh-and-fulltimeemployeecpp)
  - [PartTimeEmployee.h and PartTimeEmployee.cpp](#parttimeemployeeh-and-parttimeemployeecpp)
  - [EmployeeStatus.h and EmployeeStatus.cpp](#employeestatush-and-employeestatuscpp)
  - [Utility.h and Utility.cpp](#utilityh-and-utilitycpp)
  - [main.cpp](#maincpp)
- [Expected Output Examples](#expected-output-examples)
- [Building and Running the Project](#building-and-running-the-project)

## Project Description
The **Employee Management System** is a C++ application designed to manage employee records using a single `Employee` class hierarchy. It employs an `enum class` for roles (e.g., `Intern`, `Junior`, `Middle`, `Senior`), each associated with a rate multiplier for salary calculations. The system leverages polymorphism for key behaviors such as calculating salaries and promoting employees. Promotions update an employee’s role (e.g., `Intern` to `Junior`) using the `++` operator on the `Role` enum and adjust the salary rate accordingly. Employment types (`Full-Time`, `Part-Time`) determine the base salary calculation logic.

## Project Features
- **Add Employee**: Add employees with a specific role (e.g., `Intern`, `Junior`) and employment type (`Full-Time`, `Part-Time`).
- **Calculate Salary**: Compute salaries based on employment type, role, and rate using a virtual function.
- **Display Employee Details**: Show employee details including ID, name, salary, role, employment type, and status.
- **List All Employees**: Display a list of all employees with their calculated salaries.
- **Promote Employee**: Promote employees by updating their role (e.g., `Intern` to `Junior`) using the `++` operator on the `Role` enum and adjusting their rate.
- **Update Employee Status**: Modify an employee’s status (e.g., `Active`, `On Leave`, `Inactive`, `Retired`).
- **Search Employees**: Search for employees by name or employee ID.

## Key Concepts
- **Inheritance and Polymorphism**:
  - A base `Employee` class defines common attributes and virtual methods.
  - Derived classes (`FullTimeEmployee`, `PartTimeEmployee`) inherit from `Employee` and override methods for specific salary calculations.
  - Virtual functions (`calculateSalary()`, `promote()`) provide polymorphic behavior with default implementations.
- **Enumerated Types for Roles**:
  - `enum class Role { Intern, Junior, Middle, Senior }` represents employee positions.
  - The `++` operator is overloaded for `Role` to handle promotions.
  - Each role has an associated rate multiplier (e.g., `Intern: 1.0`, `Junior: 1.2`, `Middle: 1.5`, `Senior: 2.0`).
- **Employment Type**:
  - `enum class EmploymentType { FullTime, PartTime }` determines the base salary calculation logic.
- **Encapsulation**:
  - Employee attributes (e.g., `employeeID`, `name`, `baseSalary`, `role`, `employmentType`, `status`, `rate`) are private, with public getter and setter methods.
- **Promotion Logic**:
  - Promotions increment the role using the `++` operator and adjust the rate based on the new role.

## Project Structure
```
EmployeeManagementSystem/
│
├── include/                    # Directory for header files
│   ├── Employee.h              # Base class declaration with virtual functions
│   ├── FullTimeEmployee.h      # FullTimeEmployee class declaration
│   ├── PartTimeEmployee.h      # PartTimeEmployee class declaration
│   ├── EmployeeStatus.h        # Enums for managing employee roles, statuses
│   └── Utility.h               # Helper functions declarations (input validation, search)
│
├── src/                        # Directory for source files
│   ├── main.cpp                # Entry point for user interaction and system management
│   ├── Employee.cpp            # Base class implementation
│   ├── FullTimeEmployee.cpp    # FullTimeEmployee class implementation
│   ├── PartTimeEmployee.cpp    # PartTimeEmployee class implementation
│   ├── EmployeeStatus.cpp      # Implementation for enums and helper functions
│   └── Utility.cpp             # Implementation of helper functions
│
├── test/                       # Directory for test files
│   ├── TestEmployee.cpp        # Tests for Employee class functionality
│   ├── TestFullTimeEmployee.cpp # Tests for FullTimeEmployee class functionality
│   ├── TestPartTimeEmployee.cpp # Tests for PartTimeEmployee class functionality
│   ├── TestEmployeeStatus.cpp  # Tests for EmployeeStatus functionality
│   └── TestUtility.cpp         # Tests for Utility functions
│
├── Makefile                    # Makefile for building the project and running tests
└── README.md                   # Project documentation (this file)
```

## File Descriptions

### Employee.h and Employee.cpp
- **Description**: The base class `Employee` defines common attributes and virtual methods for all employees.
- **Enums**:
  - `enum class Role { Intern, Junior, Middle, Senior }`: Represents the employee’s position with `++` operator overloading.
  - `enum class EmploymentType { FullTime, PartTime }`: Represents the employment type.
  - `enum class EmployeeStatus { Active, OnLeave, Inactive, Retired }`: Represents the employee’s status.
- **Attributes**:
  - `employeeID` (string): Unique identifier for the employee.
  - `name` (string): Employee’s name.
  - `baseSalary` (double): Base salary for calculations.
  - `role` (Role): Current role of the employee.
  - `employmentType` (EmploymentType): Type of employment.
  - `status` (EmployeeStatus): Current status of the employee.
  - `rate` (double): Multiplier based on the role (e.g., `Intern: 1.0`, `Junior: 1.2`, `Middle: 1.5`, `Senior: 2.0`).
- **Virtual Methods**:
  - `virtual double calculateSalary()`: Default implementation returns `baseSalary * rate` (overridable).
  - `virtual void promote()`: Default implementation increments the role using `++` and updates the rate.
  - `virtual void displayDetails() const`: Displays employee details (overridable for specific formatting).
- **Other Methods**:
  - Getters and setters for attributes.
  - `updateStatus(EmployeeStatus newStatus)`: Updates the employee’s status.
  - `updateRole(Role newRole)`: Updates the employee’s role and adjusts the rate.

### FullTimeEmployee.h and FullTimeEmployee.cpp
- **Description**: Represents full-time employees with a fixed monthly salary adjusted by role rate.
- **Attributes**: Inherits all attributes from `Employee`.
- **Overrides**:
  - `calculateSalary()`: Returns `baseSalary * rate`.
  - `promote()`: Calls the base class `promote()` or adds specific logic if needed.
  - `displayDetails()`: Shows full-time-specific details.
- **Additional Benefits**: Full-time employees receive health insurance, gym memberships, and paid time off.
- **Additional Logic**: Ensures `employmentType` is set to `FullTime`.

### PartTimeEmployee.h and PartTimeEmployee.cpp
- **Description**: Represents part-time employees with an hourly wage adjusted by role rate.
- **Attributes**:
  - `hoursWorked` (double): Number of hours worked.
  - `hourlyWage` (double): Pay per hour.
- **Overrides**:
  - `calculateSalary()`: Returns `hoursWorked * hourlyWage * rate`.
  - `promote()`: Calls the base class `promote()` or adds specific logic if needed.
  - `displayDetails()`: Shows part-time-specific details.
- **Additional Logic**: Ensures `employmentType` is set to `PartTime`.

### EmployeeStatus.h and EmployeeStatus.cpp
- **Description**: Manages enums and provides helper functions for roles, statuses, and types.
- **Operator Overloading**: Overloads `++` for `Role` to handle promotions (e.g., `Intern` to `Junior`).
- **Helper Methods**:
  - `toString(Role role)`: Converts role to a string for display.
  - `toString(EmployeeStatus status)`: Converts status to a string for display.
  - `toString(EmploymentType type)`: Converts employment type to a string for display.
  - `getRateForRole(Role role)`: Returns the rate multiplier for a given role.

### Utility.h and Utility.cpp
- **Description**: Provides helper functions for the system.
- **Functions**:
  - `validateInput()`: Ensures valid user input.
  - `searchEmployeeByID()`: Searches for an employee by ID.
  - `searchEmployeeByName()`: Searches for an employee by name.
  - `formatDisplay()`: Formats employee details for output.

### main.cpp
- **Description**: The entry point for the program, providing a menu-driven interface for user interaction.
- **Functionality**:
  - Maintains a collection of employees (e.g., `vector<Employee*>`).
  - Handles user commands to add, display, promote, or update employees.

## Expected Output Examples
1. **Add a Full-Time Employee**
   ```
   Enter Employee ID: 101
   Enter Employee Name: Alice
   Enter Base Salary: 3000
   Enter Role (Intern/Junior/Middle/Senior): Junior
   Full-Time employee added successfully.
   ```

2. **Add a Part-Time Employee**
   ```
   Enter Employee ID: 102
   Enter Employee Name: Bob
   Enter Hours Worked: 50
   Enter Hourly Wage: 20
   Enter Role (Intern/Junior/Middle/Senior): Intern
   Part-Time employee added successfully.
   ```

3. **Display All Employees**
   ```
   Employee ID: 101, Name: Alice, Salary: 3600 (rate: 1.2), Role: Junior, Employment Type: Full-Time, Status: Active
   Employee ID: 102, Name: Bob, Salary: 1000 (rate: 1.0), Role: Intern, Employment Type: Part-Time, Status: Active
   ```

4. **Promote an Employee**
   ```
   Enter Employee ID to Promote: 102
   Promotion successful! Employee now has a Junior role and updated salary.
   ```

5. **Update Employee Status**
   ```
   Enter Employee ID to Update Status: 102
   Enter new Status (Active/OnLeave/Inactive/Retired): OnLeave
   Status updated successfully.
   ```

## Building and Running the Project
1. **Prerequisites**:
   - C++ compiler (e.g., `g++`).
   - `make` utility.
2. **Build the Project**:
   ```bash
   make
   ```
   This generates the executable (e.g., in a `bin/` directory or as specified in the `Makefile`).
