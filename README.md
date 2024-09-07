# -EmployeeOperatorOverloading-
// Employee.cs
public class Employee
{
    public int Id { get; set; }           // Employee's ID
    public string FirstName { get; set; } // Employee's first name
    public string LastName { get; set; }  // Employee's last name

    // Overload the == operator to compare Employee objects based on their Id
    public static bool operator ==(Employee e1, Employee e2)
    {
        // If both objects are the same instance, they are equal
        if (ReferenceEquals(e1, e2))
        {
            return true;
        }

        // If one object is null and the other is not, they are not equal
        if (ReferenceEquals(e1, null) || ReferenceEquals(e2, null))
        {
            return false;
        }

        // Compare Ids to determine equality
        return e1.Id == e2.Id;
    }

    // Overload the != operator to compare Employee objects based on their Id
    public static bool operator !=(Employee e1, Employee e2)
    {
        // Use the == operator and negate the result to determine inequality
        return !(e1 == e2);
    }

    // Override Equals method to ensure consistency with == operator
    public override bool Equals(object obj)
    {
        // Check if the object is of type Employee
        if (obj is Employee employee)
        {
            return this == employee; // Use overloaded == operator
        }
        return false;
    }

    // Override GetHashCode method to ensure consistent hashing
    public override int GetHashCode()
    {
        return Id.GetHashCode(); // Use Id for hash code
    }
}
// Program.cs
using System;

class Program
{
    static void Main(string[] args)
    {
        // Create the first Employee object and set its properties
        Employee employee1 = new Employee
        {
            Id = 1,
            FirstName = "John",
            LastName = "Doe"
        };

        // Create the second Employee object and set its properties
        Employee employee2 = new Employee
        {
            Id = 1,
            FirstName = "Jane",
            LastName = "Smith"
        };

        // Compare the two Employee objects using the overloaded == operator
        bool areEqual = employee1 == employee2;

        // Display the result of the comparison
        Console.WriteLine($"Are the employees equal? {areEqual}"); // Outputs: Are the employees equal? True

        // Change the Id of the second employee
        employee2.Id = 2;

        // Compare the two Employee objects again using the overloaded != operator
        bool areNotEqual = employee1 != employee2;

        // Display the result of the comparison
        Console.WriteLine($"Are the employees not equal? {areNotEqual}"); // Outputs: Are the employees not equal? True
    }
}
