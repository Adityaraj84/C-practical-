# C-practical-
## Program 1.
### Write a program to compute the sum of the first n terms of the following serie= 1-1/2²+1/3²-1/4²+1/5² .....
### The number of terms n is to be taken from the user through the command line. If thecommand line argument is not found ### then prompt the user to enter the value of n.
# input

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

# programm 2
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

# Programm 3
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

# Programm 4
## Write a menu driven program to perform string manipulation (without using inbuiltstring functions):
## a. Show address of each character in string
![Image](https://github.com/user-attachments/assets/83258d6c-aa48-420b-951b-3e44317be151)
## b. Concatenate two strings
![Image](https://github.com/user-attachments/assets/857e1af8-6c37-4ff4-a208-783cc7299e9d)
## c. Compare two strings
![Image](https://github.com/user-attachments/assets/4fef2173-dfbe-4913-a916-72fffdabd479)

# Programm 5 
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
# Programm 7
# Write a program to calculate GCD of two numbers (i) with recursion (ii) without recursion.


