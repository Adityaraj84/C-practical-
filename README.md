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

