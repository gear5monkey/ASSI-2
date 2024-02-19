# ASSI-2
                               PROGRAMMING IN C ASSIGNMENT 2
1 Design a C program that utilizes an enumerated data type to represent the days of the week. Allow the user to input a day as an integer (1 for Sunday, 2 for Monday, etc.), and then output the corresponding day's name.

CODE
/*1 Design a C program that utilizes an enumerated data type to represent the days of the week. Allow the user to input a day as an integer (1 for Sunday, 2 for Monday, etc.), and then output the corresponding day's name. */
#include <stdio.h>
// Define an enum to represent days of the week
enum Days {
    SUNDAY = 1,
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY
};
int main() {
    int userInput;
    // Prompt the user to enter a number corresponding to a day
    printf("Enter a number (1-7) representing a day of the week: ");
    scanf("%d", &userInput);
    // Check if the user input is within the valid range
    if(userInput < SUNDAY || userInput > SATURDAY) {
        printf("Invalid input! Please enter a number between 1 and 7.\n");
        return 1; // Return with error
    }
    // Convert the input to the corresponding day
    enum Days userDay = (enum Days)userInput;
    // Print the name of the day based on the input
    switch (userDay) {
        case SUNDAY:
            printf("Sunday\n");
            break;
        case MONDAY:
            printf("Monday\n");
            break;
        case TUESDAY:
            printf("Tuesday\n");
            break;
        case WEDNESDAY:
            printf("Wednesday\n");
            break;
        case THURSDAY:
            printf("Thursday\n");
            break;
        case FRIDAY:
            printf("Friday\n");
            break;
        case SATURDAY:
            printf("Saturday\n");
            break;
        default:
            printf("Invalid day\n");
    }
 
    return 0;
}
OUTPUT

 







Algorithm for Q1 code: 

1.	Define an Enum to represent the days of the week. Each day will be assigned a unique integer value.
2.	Prompt the user to enter a number representing a day of the week.
3.	Read the user input as an integer.
4.	Validate the input to ensure it is within the valid range (1-7).
5.	Convert the integer input to the corresponding Enum value representing the day of the week.
6.	Use a switch statement to print the name of the day based on the Enum value.
7.	Handle cases where the input is out of range or invalid.

2 Write a C function named average that takes a variable number of arguments and calculates the average. The program should use this function to find the average of three different sets of numbers (e.g., 3, 5, 7 and 10, 20).

/* 2 Write a C function named average that takes a variable number of arguments and calculates the average.
 The program should use this function to find the average of three different sets of numbers (e.g., 3, 5, 7 and 10, 20). */


#include <stdio.h>
#include <stdarg.h>
// Function to calculate the average of a variable number of arguments
double average(int count, ...) {
    va_list args;
    int sum = 0;
    // Initialize the va_list
    va_start(args, count);
    // Loop through the arguments and calculate the sum
    for (int i = 0; i < count; ++i) {
        sum += va_arg(args, int);
    }
    // Clean up the va_list
    va_end(args);
    // Calculate and return the average
    return (double)sum / count;
}
int main() {
    // Calculate the average of three different sets of numbers
    double average1 = average(3, 3, 5, 7);
    double average2 = average(2, 10, 20);
    double average3 = average(5, 1, 2, 3, 4, 5);
    // Display the results
    printf("Average of (3, 5, 7): %.2f\n", average1);
    printf("Average of (10, 20): %.2f\n", average2);
    printf("Average of (1, 2, 3, 4, 5): %.2f\n", average3);
    return 0;
}
OUTPUT
 




Algorithm for Q2 code: 
1 Define a function named average that takes a variable number of arguments.
2 Inside the function:
•	Initialize a va_list object using va_start.
•	Iterate through the arguments using va_arg macro, calculating the sum of all arguments.
•	Count the number of arguments passed.
•	Clean up the va_list object using va_end.
•	Calculate the average by dividing the sum by the number of arguments.
•	Return the average value.
3 In the main function, call the average function three times with different sets of numbers and print the results.

3 Develop a C program that uses function pointers to create a calculator. Implement functions for addition, subtraction, multiplication, and division. Allow the user to choose an operation and perform calculations using function pointers.


/* 3 Develop a C program that uses function pointers to create a calculator.
 Implement functions for addition, subtraction, multiplication, and division. 
Allow the user to choose an operation and perform calculations using function pointers. *
#include <stdio.h>
// Function prototypes
double add(double a, double b);
double subtract(double a, double b);
double multiply(double a, double b);
double divide(double a, double b);
// Function pointer typedef for operation functions
typedef double (*OperationFunc)(double, double);
// Function to perform operation using function pointers
double performOperation(double a, double b, OperationFunc operation);
int main() {
    double num1, num2;
    char choice;
    do {
        // Display menu
        printf("\nCalculator Menu:\n");
        printf("1. Addition\n");
        printf("2. Subtraction\n");
        printf("3. Multiplication\n");
        printf("4. Division\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf(" %c", &choice);
        switch (choice) {
            case '1':
                printf("Enter two numbers: ");
                scanf("%lf %lf", &num1, &num2);
                printf("Result: %.2f\n", performOperation(num1, num2, add));
                break;
            case '2':
                printf("Enter two numbers: ");
                scanf("%lf %lf", &num1, &num2);
                printf("Result: %.2f\n", performOperation(num1, num2, subtract));
                break;
            case '3':
                printf("Enter two numbers: ");
                scanf("%lf %lf", &num1, &num2);
                printf("Result: %.2f\n", performOperation(num1, num2, multiply));
                break;
            case '4':
                printf("Enter two numbers: ");
                scanf("%lf %lf", &num1, &num2);
                printf("Result: %.2f\n", performOperation(num1, num2, divide));
                break;
            case '5':
                printf("Exiting calculator.\n");
                break;
            default:
                printf("Invalid choice. Please choose a valid operation.\n");
        }
    } while (choice != '5');
    return 0;
}
 
// Function to perform operation using function pointers
double performOperation(double a, double b, OperationFunc operation) {
    return operation(a, b);
}
// Addition function
double add(double a, double b) {
    return a + b;
}
// Subtraction function
double subtract(double a, double b) {
    return a - b;
}
// Multiplication function
double multiply(double a, double b) {
    return a * b;
}
// Division function
double divide(double a, double b) {
    if (b != 0) {
        return a / b;
    } else {
        printf("Error: Division by zero!\n");
        return 0;
    }
}

OUTPUT

 







Algorithm for Q3 code: 

1.	Define function prototypes for addition, subtraction, multiplication, and division.
2.	Implement functions for addition, subtraction, multiplication, and division.
3.	Define a function that takes two numbers and a function pointer as arguments and performs the corresponding operation.
4.	Inside the main function: 
•	Display a menu to the user with options for different operations (addition, subtraction, multiplication, division, and exit).
•	Prompt the user to choose an operation.
•	Based on the user's choice, call the corresponding function using function pointers.
•	Print the result of the operation.
•	Repeat the process until the user chooses to exit.

4 Create a C program that generates and prints the first N prime numbers using a function. Take N as input from the user and use a separate function to determine if a given number is prime.
/*4 Create a C program that generates and prints the first N prime numbers using a function.
Take N as input from the user and use a separate function to determine if a given number is prime. *
#include <stdio.h>
// Function to determine if a number is prime
int isPrime(int num) {
    if (num <= 1)
        return 0; // Not prime
    for (int i = 2; i * i <= num; i++) {
        if (num % i == 0)
            return 0; // Not prime
    }
    return 1; // Prime
}
// Function to generate and print the first N prime numbers
void generatePrimes(int N) {
    int count = 0;
    int num = 2; // Start checking from 2
 
    printf("First %d prime numbers:\n", N);
    while (count < N) {
        if (isPrime(num)) {
            printf("%d ", num);
            count++;
        }
        num++;
    }
    printf("\n");
}
int main() {
    int N;
    // Prompt the user to enter the value of N
    printf("Enter the value of N: ");
    scanf("%d", &N);
    // Generate and print the first N prime numbers
    generatePrimes(N);
    return 0;
}

OUTPUT

 




Algorithm for Q4 code:
 
1 Define a function is Prime that takes an integer as input and returns 1 if the number is prime, and 0 otherwise.
2 Define a function generate Primes that takes an integer N as input and prints the first N prime numbers.
3 Inside the generate Primes function:
Initialize a variable count to keep track of the number of prime numbers found.
Iterate through numbers starting from 2 until count reaches N:
Check if the current number is prime using the is Prime function.
If the number is prime, print it and increment count.
4 In the main function:
Prompt the user to enter the value of N.
Call the generate Primes function with the input value of N.

5 Implement a C function to check whether a given integer is a palindrome or not. In the main program, take user input, call the function, and print whether the entered number is a palindrome or not.
/* 5 Implement a C function to check whether a given integer is a palindrome or not. 
In the main program, take user input, call the function,
 and print whether the entered number is a palindrome or not.*
 #include <stdio.h>
#include <string.h>
// Function to check whether a given integer is a palindrome or not
int isPalindrome(int num) {
    char numStr[20]; // Assuming the maximum length of integer is 20 digits
    sprintf(numStr, "%d", num); // Convert integer to string
    int len = strlen(numStr);
    // Initialize two pointers
    int start = 0;
    int end = len - 1;
    // Compare characters from start and end
    while (start < end) {
        if (numStr[start] != numStr[end]) {
            return 0; // Not a palindrome
        }
        start++;
        end--;
    }
    return 1; // Palindrome
}
int main() {
    int num;
    // Prompt the user to enter an integer
    printf("Enter an integer: ");
    scanf("%d", &num);
    // Check if the entered number is a palindrome
    if (isPalindrome(num)) {
        printf("%d is a palindrome.\n", num);
    } else {
        printf("%d is not a palindrome.\n", num);
    }
    return 0;
}

OUTPUT 


 


Algorithm for Q5 code:

1 Define a function named is Palindrome that takes an integer as input and returns 1 if the number is a palindrome, and 0 otherwise.
2 Inside the is Palindrome function:
•	Convert the integer to a string or array of characters.
•	Initialize two pointers, one pointing to the beginning of the string and the other to the end.
•	Compare the characters at these pointers. If they match, move the pointers towards each other until they meet or cross each other.
•	If all character’s match, return 1 (indicating that the number is a palindrome); otherwise, return 0.
3 In the main function:
•	Prompt the user to enter an integer.
•	Call the is Palindrome function with the user input as an argument.
•	Print whether the entered number is a palindrome or not.

6 If a five-digit numbers input through the keyboard, write a program to print a new number by adding one to each of its digits. eg: input 12391 output 2350
/* 6 If a five digit numberis input through the keyboard,
write a program to print a new number by adding one to each of its digits.
 eg: input 12391 output 2350*/
#include <stdio.h>
int main() {
    int num;
    // Input a five-digit number from the user
    printf("Enter a five-digit number: ");
    scanf("%d", &num);
    // Add one to each digit and print the new number
    printf("New number: %d%d%d%d%d\n",
           (num / 10000 + 1) % 10,
           (num / 1000 + 1) % 10,
           (num / 100 + 1) % 10,
           (num / 10 + 1) % 10,
           (num % 10 + 1) % 10);
    return 0;
}

OUTPUT
 




Algorithm for Q6 code:
1 Start: Begin the program execution.
2.Input: Prompt the user to enter a five-digit number.
3.Read Input: Read the entered five-digit number from the user.
4.Calculate New Number: 
•     Extract each digit of the entered number and add one to it.
•     Handle the case where adding one results in a carry (i.e., when the digit becomes 10, it should wraparound to 0).
•     Calculate the new number by taking the remainder when dividing the updated digit by 10.
5.Print New Number: Print the new number obtained by combining the updated digits.
6.End: Terminate the program.
This algorithm outlines the steps involved in the C program for taking a five-digit number as input, adding one to each of its digits, and printing the resulting new number.

7 The distance between two cities (in km) is inputput throught the keyboard. Write a progrm to convert and print this distance in meters, feet, inches and centimeters.
/* 7 The distance between two cities (in km) is input put through the keyboard. 
Write a program to convert and print this distance in meters, feet, inches and centimeters. */
#include <stdio.h>
int main() {
    double distanceKm, distanceMeters, distanceFeet, distanceInches, distanceCentimeters;
 
    // Prompt the user to input the distance between two cities in kilometers
    printf("Enter the distance between two cities (in kilometers): ");
    scanf("%lf", &distanceKm);
    // Convert the distance to meters, feet, inches, and centimeters
    distanceMeters = distanceKm * 1000;
    distanceFeet = distanceKm * 3280.84;
    distanceInches = distanceKm * 39370.1;
    distanceCentimeters = distanceKm * 100000;
    // Print the converted distances
    printf("Distance in meters: %.2f\n", distanceMeters);
    printf("Distance in feet: %.2f\n", distanceFeet);
    printf("Distance in inches: %.2f\n", distanceInches);
    printf("Distance in centimeters: %.2f\n", distanceCentimeters);
    return 0;
}

OUTPUT

 



      Algorithm for Q7 code 

1.	Prompt the user to input the distance between two cities in kilometers.
2.	Read the input distance from the user.
3.	Convert the distance to meters by multiplying it by 1000.
4.	Convert the distance to feet by multiplying it by approximately 3280.84 (1 kilometer = 3280.84 feet).
5.	Convert the distance to inches by multiplying it by approximately 39370.1 (1 kilometer = 39370.1 inches).
6.	Convert the distance to centimeters by multiplying it by 100000.
7.	Print the converted distances in meters, feet, inches, and centimeters.

8 If the marks obtained by a student in five different subjects are input through the keyboard, find out the aggregate marks and percentage marks obtained by the student( maximum mark limit 100).
/*  
8 If the marks obtained by a student in five different subjects are input through the keyboard, 
find out the aggregate marks and percentage marks obtained by the student( maxium mark limit 100).
*/
#include <stdio.h>
int main() {
    int marks1, marks2, marks3, marks4, marks5;
    int totalMarks;
    float percentageMarks;
    // Prompt the user to input marks obtained in each subject
    printf("Enter marks obtained in five subjects (out of 100):\n");
    printf("Subject 1: ");
    scanf("%d", &marks1);
    printf("Subject 2: ");
    scanf("%d", &marks2);
    printf("Subject 3: ");
    scanf("%d", &marks3);
    printf("Subject 4: ");
    scanf("%d", &marks4);
    printf("Subject 5: ");
    scanf("%d", &marks5);
    // Check if any of the input marks exceed the maximum mark limit (100)
    if (marks1 > 100 || marks2 > 100 || marks3 > 100 || marks4 > 100 || marks5 > 100) {
        printf("Error: Marks should not exceed 100.\n");
        return 1;
    }
    // Calculate the total marks obtained
    total Marks = marks1 + marks2 + marks3 + marks4 + marks5;
    // Calculate the percentage marks obtained
    percentage Marks = (float)total Marks / (5 * 100) * 100;
    // Print the aggregate marks and percentage marks obtained
    printf("Aggregate Marks: %d\n", totalMarks);
    printf("Percentage Marks: %.2f%%\n", percentageMarks);
    return 0;
}


OUTPUT

 





Algorithm for Q8code:

1.	Define variables to store marks obtained in each subject and total marks.
2.	Prompt the user to input marks obtained in each of the five subjects.
3.	Read the input marks from the user.
4.	Check if any of the input marks exceed the maximum mark limit (100). If so, display an error message and exit the program.
5.	Calculate the total marks obtained by summing up the marks obtained in all five subjects.
6.	Calculate the percentage marks obtained by dividing the total marks obtained by the maximum possible marks (i.e., 100 marks per subject multiplied by 5 subjects) and multiplying by 100.
7.	Print the aggregate marks and percentage marks obtained by the student.

9 Write a C program to swap two numbers without using third variable.
/*9 Write a C program to swap two numbers without using third variable*/
#include <stdio.h>
int main() {
    int num1, num2;
    // Prompt the user to input two numbers
    printf("Enter two numbers: ");
    scanf("%d %d", &num1, &num2);
    // Swap the numbers using bitwise XOR operation
    num1 = num1 ^ num2.
    num2 = num1 ^ num2;
    num1 = num1 ^ num2;
    // Print the swapped numbers
    printf("After swapping:\n");
    printf("First number: %d\n", num1);
    printf("Second number: %d\n", num2);
    return 0;
}
OUTPUT



 




Algorithm for Q9 code:

1.	Prompt the user to input a five-digit number.
2.	Read the input number from the user.
3.	Extract the individual digits of the number.
4.	Reverse the order of the digits.
5.	Reconstruct the reversed number.
6.	Print the reversed number.

10 If a five-digit number is input through the keyboard, write a program to reverse the number.
/* 10 If a five-digit number is input through the keyboard, write a program to reverse the number*/
#include <stdio.h>
int main() {
    int number, reversedNumber = 0;
    // Prompt the user to input a five-digit number
    printf("Enter a five-digit number: ");
    scanf("%d", &number);
    // Check if the input number is a five-digit number
    if (number < 10000 || number > 99999) {
        printf("Error: Please enter a five-digit number.\n");
        return 1; // Exit the program with error
    }
    // Reverse the number
    while (number != 0) {
        int digit = number % 10; // Extract the last digit
        reversedNumber = reversedNumber * 10 + digit; // Append the digit to the reversed number
        number /= 10; // Remove the last digit from the original number
    }
    // Print the reversed number
    printf("Reversed number: %d\n", reversedNumber);
    return 0;
}

OUTPUT

 
Algorithm for Q10 code:

1.	Prompt the user to input a five-digit number.
2.	Read the input number from the user.
3.	Extract the individual digits of the number.
4.	Reverse the order of the digits.
5.	Reconstruct the reversed number.
6.	Print the reversed number.

