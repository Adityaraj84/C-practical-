# C-practical-
## Program 1.
### Write a program to compute the sum of the first n terms of the following serie= 1-1/2²+1/3²-1/4²+1/5² .....The number of terms n is to be taken from the user through the command line. If thecommand line argument is not found ### then prompt the user to enter the value of n.input

#include<iostream>
#include <cmath>
#include <cstdlib> // For atoi()
using namespace std;
int main(int argc, char *argv[]) {
    int n;

    // Check if command-line argument is provided
    if (argc > 1) {
        n = atoi(argv[1]); // Convert string to integer
    } else {
        // Prompt user for input
        cout << "Enter the number of terms (n): ";
        cin >> n;
    }

    if (n <= 0) {
        cout << "Please enter a positive integer." << endl;
        return 1;
    }

    double sum = 0.0;

    for (int i = 1; i <= n; i++) {
        double term = 1.0 / (i * i); // Compute 1/(i^2)
        if (i % 2 == 0) {
            sum -= term; // Subtract if even
        } else {
            sum += term; // Add if odd
        }
    }

    cout << "Sum of the first " << n << " terms of the series: " << sum << endl;
    return 0;
}
![Image](https://github.com/user-attachments/assets/7f740462-eebb-4dc4-a8ac-f047eda0ac65)

# program 2
## Write a program to remove the duplicates from an array.
#include <iostream>
#include <unordered_set>
#include <vector>

void removeDuplicates(int arr[], int &size) {
    std::unordered_set<int> seen;
    std::vector<int> uniqueArr;

    // Insert elements into the set (removes duplicates automatically)
    for (int i = 0; i < size; i++) {
        if (seen.find(arr[i]) == seen.end()) {
            seen.insert(arr[i]);
            uniqueArr.push_back(arr[i]);
        }
    }

    // Copy back to original array
    size = uniqueArr.size();
    for (int i = 0; i < size; i++) {
        arr[i] = uniqueArr[i];
    }
}

int main() {
    int arr[] = {4, 2, 2, 8, 3, 3, 1, 4, 5, 1};
    int size = sizeof(arr) / sizeof(arr[0]);

    std::cout << "Original Array: ";
    for (int i = 0; i < size; i++)
        std::cout << arr[i] << " ";
    
    removeDuplicates(arr, size);

    std::cout << "\nArray after removing duplicates: ";
    for (int i = 0; i < size; i++)
        std::cout << arr[i] << " ";

    return 0;
}
## Output 
![Image](https://github.com/user-attachments/assets/42daf852-7154-4aeb-9a14-4b341e811a59)

# Program 3
## Write a program that prints a table indicating the number of occurrences of eachalphabet in the text entered as command line arguments.

#include <iostream>
#include <cctype>

void countAlphabets(int argc, char* argv[]) {
    int frequency[26] = {0}; // Array to store frequency of each letter

    // Traverse each command-line argument
    for (int i = 1; i < argc; i++) {
        for (int j = 0; argv[i][j] != '\0'; j++) {
            char ch = std::tolower(argv[i][j]); // Convert to lowercase
            if (ch >= 'a' && ch <= 'z') { // Only count alphabets
                frequency[ch - 'a']++;
            }
        }
    }

    // Print the table
    std::cout << "Alphabet Frequency Table:\n";
    std::cout << "--------------------------\n";
    for (int i = 0; i < 26; i++) {
        if (frequency[i] > 0) { // Print only occurring alphabets
            std::cout << (char)('a' + i) << " : " << frequency[i] << std::endl;
        }
    }
}

int main(int argc, char* argv[]) {
    if (argc < 2) {
        std::cout << "Usage: " << argv[0] << " <text>\n";
        return 1;
    }

    countAlphabets(argc, argv);
    return 0;
}
![Image](https://github.com/user-attachments/assets/b42bc627-bd90-4d8e-9995-553dcb9d78df)

# Program 4
## Write a menu driven program to perform string manipulation (without using inbuiltstring functions):
## a. Show address of each character in string
![Image](https://github.com/user-attachments/assets/83258d6c-aa48-420b-951b-3e44317be151)
## b. Concatenate two strings
![Image](https://github.com/user-attachments/assets/857e1af8-6c37-4ff4-a208-783cc7299e9d)
## c. Compare two strings
![Image](https://github.com/user-attachments/assets/4fef2173-dfbe-4913-a916-72fffdabd479)

# Program 5 
## Write a program to merge two ordered arrays to get a single ordered array
#include <iostream>
using namespace std;

// Function to merge two sorted arrays into one sorted array
void mergeSortedArrays(int arr1[], int size1, int arr2[], int size2, int mergedArray[]) {
    int i = 0, j = 0, k = 0;

    // Merge arrays while both have elements
    while (i < size1 && j < size2) {
        if (arr1[i] < arr2[j])
            mergedArray[k++] = arr1[i++];
        else
            mergedArray[k++] = arr2[j++];
    }

    // Copy remaining elements of arr1
    while (i < size1)
        mergedArray[k++] = arr1[i++];

    // Copy remaining elements of arr2
    while (j < size2)
        mergedArray[k++] = arr2[j++];
}

int main() {
    int arr1[] = {1, 3, 5, 7};
    int arr2[] = {2, 4, 6, 8, 9};

    int size1 = sizeof(arr1) / sizeof(arr1[0]);
    int size2 = sizeof(arr2) / sizeof(arr2[0]);
    int mergedSize = size1 + size2;
    int mergedArray[mergedSize];

    // Merge the two sorted arrays
    mergeSortedArrays(arr1, size1, arr2, size2, mergedArray);

    // Print the merged sorted array
    cout << "Merged Sorted Array: ";
    for (int i = 0; i < mergedSize; i++)
        cout << mergedArray[i] << " ";

    return 0;
}
![Image](https://github.com/user-attachments/assets/d4ef3150-3a13-40ec-acb2-8bfb3ff37550)
![Image](https://github.com/user-attachments/assets/2bf3948f-7613-4f07-b83f-d27b3e03315b)
# 6. Write a program to search a given element in a set of N numbers using Binary search(i) with recursion (ii) without recursion.
#include <iostream>
using namespace std;

// Recursive Binary Search
int binarySearchRecursive(int arr[], int left, int right, int key) {
    if (left <= right) {
        int mid = left + (right - left) / 2;

        // If the element is present at the middle itself
        if (arr[mid] == key)
            return mid;

        // If the element is smaller than mid, it can only be in left subarray
        if (arr[mid] > key)
            return binarySearchRecursive(arr, left, mid - 1, key);

        // Else the element can only be in right subarray
        return binarySearchRecursive(arr, mid + 1, right, key);
    }
    return -1; // Element not found
}

// Iterative Binary Search
int binarySearchIterative(int arr[], int n, int key) {
    int left = 0, right = n - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == key)
            return mid;
        else if (arr[mid] > key)
            right = mid - 1;
        else
            left = mid + 1;
    }
    return -1; // Element not found
}

int main() {
    int n, key;
    cout << "Enter the number of elements: ";
    cin >> n;

    int arr[n];
    cout << "Enter " << n << " sorted elements: ";
    for (int i = 0; i < n; i++)
        cin >> arr[i];

    cout << "Enter the element to search: ";
    cin >> key;

    // Using Recursive Binary Search
    int resultRecursive = binarySearchRecursive(arr, 0, n - 1, key);
    if (resultRecursive != -1)
        cout << "Element found at index (Recursive): " << resultRecursive << endl;
    else
        cout << "Element not found (Recursive)" << endl;

    // Using Iterative Binary Search
    int resultIterative = binarySearchIterative(arr, n, key);
    if (resultIterative != -1)
        cout << "Element found at index (Iterative): " << resultIterative << endl;
    else
        cout << "Element not found (Iterative)" << endl;

    return 0}
    
 ![Image](https://github.com/user-attachments/assets/1263bf80-1fe7-414e-8d4e-7ffdf734c067)
![Image](https://github.com/user-attachments/assets/90b5beaa-c896-4245-a73a-73b86e02fd02)
# Program 7
# Write a program to calculate GCD of two numbers (i) with recursion (ii) without recursion.

![Image](https://github.com/user-attachments/assets/563abfe4-d353-4e7e-a902-d253853231c2)
![Image](https://github.com/user-attachments/assets/8732513b-d591-4eb2-a2c1-9e124c74ef3d)

# Program 8
# Create a Matrix class. Write a menu-driven program to perform following Matrixoperations (exceptions should be thrown by the functions if matrices passed to them are incompatible and handled by the main() function):a. Sum b. Productc. Transpose
![Image](https://github.com/user-attachments/assets/59d3f351-5d7e-4101-82f7-6c2ab3ad4ff0)
![Image](https://github.com/user-attachments/assets/c66977ca-52ec-4147-8a34-defe22a8ade1)
![Image](https://github.com/user-attachments/assets/0f3de777-c39a-46b5-92db-4fe3647fc1fb)
# Program 9
# Define a class Person having name as a data member. Inherit two classes Student and employee from Person. Student has additional attributes as course, marks and yearand Employee has department and salary. Write display() method in all the three classes to display the corresponding attributes. Provide the necessary methods to showruntime 
![Image](https://github.com/user-attachments/assets/3ab44989-ebb5-4282-bec6-e8c555257dbb)
![Image](https://github.com/user-attachments/assets/1b0cbd0e-04b7-4970-9d78-95f594142c91)
# program 10
## Create a Triangle class. Add exception handling statements to ensure the followingconditions: all sides are greater than 0 and sum of any two sides are greater than the third side. The class should also have overloaded functions for calculating the area of a right angled triangle as well as using Heron's formula to calculate the area of any type of triangle)
![Image](https://github.com/user-attachments/assets/71890b92-39d6-45ef-8d22-a927a3e3f056)
![Image](https://github.com/user-attachments/assets/5f9011ab-6ca2-4ee9-b8d7-b6c45ecf1d0d)
# Program 11
## Create a class Student containing fields for Roll No., Name, Class, Year and Total Marks. Write a program to store 5 objects of Student class in a file. Retrieve these records from the file and display them
#include <iostream>
#include <fstream>

using namespace std;

class Student {
private:
    int rollNo;
    char name[50];
    char studentClass[10];
    int year;
    float totalMarks;

public:
    void getData() {
        cout << "Enter Roll No.: ";
        cin >> rollNo;
        cin.ignore();
        cout << "Enter Name: ";
        cin.getline(name, 50);
        cout << "Enter Class: ";
        cin.getline(studentClass, 10);
        cout << "Enter Year: ";
        cin >> year;
        cout << "Enter Total Marks: ";
        cin >> totalMarks;
    }

    void showData() const {
        cout << "\nRoll No.: " << rollNo;
        cout << "\nName: " << name;
        cout << "\nClass: " << studentClass;
        cout << "\nYear: " << year;
        cout << "\nTotal Marks: " << totalMarks << endl;
    }

    void writeToFile() {
        ofstream outFile("students.dat", ios::binary | ios::app);
        outFile.write((char *)this, sizeof(*this));
        outFile.close();
    }

    void readFromFile() {
        ifstream inFile("students.dat", ios::binary);
        if (!inFile) {
            cout << "Error: Cannot open file!" << endl;
            return;
        }
        while (inFile.read((char *)this, sizeof(*this))) {
            showData();
        }
        inFile.close();
    }
};

int main() {
    Student s;
    int n = 5;

    // Writing data to file
    cout << "Enter details of 5 students:\n";
    for (int i = 0; i < n; i++) {
        s.getData();
        s.writeToFile();
    }

    // Reading data from file
    cout << "\nStudent records retrieved from file:\n";
    s.readFromFile();

    return 0;
}
![Image](https://github.com/user-attachments/assets/d277f4dd-68dc-43ad-9565-b8ba4a4d4fc9)
![Image](https://github.com/user-attachments/assets/b863b849-b52c-4e9e-850b-f013ea56c23d)
