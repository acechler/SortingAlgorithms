# Main

```cpp

#include <iostream>
#include "BubbleSort.hpp"
#include "InsertionSort.hpp"
#include "SelectionSort.hpp"
#include "QuickSort.hpp"
int main() {
    int arr[] = { 5, 3, 8, 4, 2 };
    // int arr[] = { 1,2,3,4,5,6,7,8 };
    size_t size = sizeof(arr) / sizeof(arr[0]);

    AESort::InsertionSort<int> sorter;
    if (sorter.sort(arr, 0, size)) {
        std::cout << "Sorted array: ";
        for (size_t i = 0; i < size; ++i) {
            std::cout << arr[i] << " ";
        }
        std::cout << std::endl;
    }
    else {
        std::cout << "Sorting failed." << std::endl;
    }

    return 0;
}

```