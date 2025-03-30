#include <iostream>
#include <vector>
#include <algorithm> // For std::sort

using namespace std;

// Function for Sequential Search
int sequentialSearch(const vector<int>& arr, int target, int& comparisons) {
    comparisons = 0; // Initialize comparisons count
    for (size_t i = 0; i < arr.size(); ++i) {
        comparisons++;
        if (arr[i] == target) {
            return i; // Return the index of the found item
        }
    }
    return -1; // Return -1 if not found
}

// Function for Binary Search
int binarySearch(const vector<int>& arr, int target, int& comparisons) {
    comparisons = 0; // Initialize comparisons count
    int left = 0;
    int right = arr.size() - 1;

    while (left <= right) {
        int mid = left + (right - left) / 2; // To prevent overflow
        comparisons++;

        if (arr[mid] == target) {
            return mid; // Return the index of the found item
        } else if (arr[mid] < target) {
            left = mid + 1; // Search in the right half
        } else {
            right = mid - 1; // Search in the left half
        }
    }
    return -1; // Return -1 if not found
}

// Function to display the array
void displayArray(const vector<int>& arr) {
    for (int num : arr) {
        cout << num << " ";
    }
    cout << endl;
}

// Main function
int main() {
    int n, target;

    // Accepting the number of elements
    cout << "Enter the number of elements: ";
    cin >> n;

    vector<int> data(n);
    cout << "Enter " << n << " integers: ";
    for (int i = 0; i < n; ++i) {
        cin >> data[i];
    }

    // Sorting the data for binary search
    sort(data.begin(), data.end());
    cout << "Sorted data: ";
    displayArray(data);

    // Accepting the target value for search
    cout << "Enter the number to search: ";
    cin >> target;

    // Perform Sequential Search
    int seqComparisons = 0;
    int seqIndex = sequentialSearch(data, target, seqComparisons);
    if (seqIndex != -1) {
        cout << "Sequential Search: " << target << " found at index " << seqIndex << " with " << seqComparisons << " comparisons." << endl;
    } else {
        cout << "Sequential Search: " << target << " not found after " << seqComparisons << " comparisons." << endl;
    }

    // Perform Binary Search
    int binComparisons = 0;
    int binIndex = binarySearch(data, target, binComparisons);
    if (binIndex != -1) {
        cout << "Binary Search: " << target << " found at index " << binIndex << " with " << binComparisons << " comparisons." << endl;
    } else {
        cout << "Binary Search: " << target << " not found after " << binComparisons << " comparisons." << endl;
    }

    // Determine which algorithm is more efficient
    if (seqComparisons < binComparisons) {
        cout << "Most efficient algorithm: Sequential Search" << endl;
    } else if (binComparisons < seqComparisons) {
        cout << "Most efficient algorithm: Binary Search" << endl;
    } else {
        cout << "Both algorithms made the same number of comparisons." << endl;
    }

    return 0;
}
