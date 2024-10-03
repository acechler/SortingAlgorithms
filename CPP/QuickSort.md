# QuickSort

```cpp

#pragma once
#include "ISort.h"
#include <iostream>
#include <algorithm> // for std::swap

namespace AESort {

    template <typename T>
    class QuickSort : public ISort<T> {
    public:
        bool sort(T* arr, size_t begin, size_t end) override {
            // Basic validation
            if (arr == nullptr) {
                std::cerr << "Error: Null array passed to QuickSort.\n";
                return false;
            }
            if (begin >= end) return true; // Already sorted if only one element or invalid range

            // Recursive quicksort call
            size_t pivotIndex = this->partition(arr, begin, end);
            if (pivotIndex > 0) this->sort(arr, begin, pivotIndex - 1); // Prevent underflow
            this->sort(arr, pivotIndex + 1, end);

            return true;
        }

        bool sort(std::vector<T>& arr, size_t begin, size_t end) override {
            // Basic validation
            if (begin >= end) return true; // Already sorted if only one element or invalid range

            // Recursive quicksort call
            size_t pivotIndex = this->partition(arr, begin, end);
            if (pivotIndex > 0) this->sort(arr, begin, pivotIndex - 1); // Prevent underflow
            this->sort(arr, pivotIndex + 1, end);

            return true;
        }

    private:
        size_t partition(T* arr, size_t start, size_t end) {
            T pivot = arr[start];
            size_t count = 0;

            // Count elements less than or equal to pivot
            for (size_t i = start + 1; i <= end; i++) {
                if (arr[i] <= pivot)
                    count++;
            }

            // Place pivot at its correct position
            size_t pivotIndex = start + count;
            std::swap(arr[pivotIndex], arr[start]);

            // Partition the array into two halves
            size_t i = start, j = end;
            while (i < pivotIndex && j > pivotIndex) {
                while (arr[i] <= pivot && i < pivotIndex) {
                    i++;
                }
                while (arr[j] > pivot && j > pivotIndex) {
                    j--;
                }
                if (i < pivotIndex && j > pivotIndex) {
                    std::swap(arr[i++], arr[j--]);
                }
            }

            return pivotIndex;
        }

        size_t partition(std::vector<T>& arr, size_t start, size_t end) {
            T pivot = arr[start];
            size_t count = 0;

            // Count elements less than or equal to pivot
            for (size_t i = start + 1; i <= end; i++) {
                if (arr[i] <= pivot)
                    count++;
            }

            // Place pivot at its correct position
            size_t pivotIndex = start + count;
            std::swap(arr[pivotIndex], arr[start]);

            // Partition the array into two halves
            size_t i = start, j = end;
            while (i < pivotIndex && j > pivotIndex) {
                while (arr[i] <= pivot && i < pivotIndex) {
                    i++;
                }
                while (arr[j] > pivot && j > pivotIndex) {
                    j--;
                }
                if (i < pivotIndex && j > pivotIndex) {
                    std::swap(arr[i++], arr[j--]);
                }
            }

            return pivotIndex;
        }
    };

} // namespace AESort


```