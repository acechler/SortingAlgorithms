# MergeSort

```cpp
#pragma once
#include "ISort.h"
#include <vector>
#include <iostream>

namespace AESort {

    template <typename T>
    class MergeSort : public ISort<T> {
    public:
        bool sort(T* arr, size_t begin, size_t end) override {
            // Basic validation
            if (arr == nullptr) {
                std::cerr << "Error: Null array passed to MergeSort.\n";
                return false;
            }
            if (begin >= end) return true; // Already sorted if only one element or invalid range

            // Recursive merge sort call
            size_t mid = begin + (end - begin) / 2;
            sort(arr, begin, mid);
            sort(arr, mid + 1, end);
            merge(arr, begin, mid, end);

            return true;
        }

        bool sort(std::vector<T>& arr, size_t begin, size_t end) override {
            // Basic validation
            if (begin >= end) return true; // Already sorted if only one element or invalid range

            // Recursive merge sort call
            size_t mid = begin + (end - begin) / 2;
            sort(arr, begin, mid);
            sort(arr, mid + 1, end);
            merge(arr, begin, mid, end);

            return true;
        }

    private:
        void merge(T* arr, size_t begin, size_t mid, size_t end) {
            size_t n1 = mid - begin + 1;
            size_t n2 = end - mid;

            // Create temporary arrays
            T* left = new T[n1];
            T* right = new T[n2];

            // Copy data to temporary arrays
            for (size_t i = 0; i < n1; i++)
                left[i] = arr[begin + i];
            for (size_t j = 0; j < n2; j++)
                right[j] = arr[mid + 1 + j];

            // Merge the temporary arrays back into arr[begin..end]
            size_t i = 0, j = 0, k = begin;
            while (i < n1 && j < n2) {
                if (left[i] <= right[j]) {
                    arr[k] = left[i];
                    i++;
                }
                else {
                    arr[k] = right[j];
                    j++;
                }
                k++;
            }

            // Copy the remaining elements of left[], if any
            while (i < n1) {
                arr[k] = left[i];
                i++;
                k++;
            }

            // Copy the remaining elements of right[], if any
            while (j < n2) {
                arr[k] = right[j];
                j++;
                k++;
            }

            // Clean up
            delete[] left;
            delete[] right;
        }

        void merge(std::vector<T>& arr, size_t begin, size_t mid, size_t end) {
            size_t n1 = mid - begin + 1;
            size_t n2 = end - mid;

            // Create temporary arrays
            std::vector<T> left(n1);
            std::vector<T> right(n2);

            // Copy data to temporary arrays
            for (size_t i = 0; i < n1; i++)
                left[i] = arr[begin + i];
            for (size_t j = 0; j < n2; j++)
                right[j] = arr[mid + 1 + j];

            // Merge the temporary arrays back into arr[begin..end]
            size_t i = 0, j = 0, k = begin;
            while (i < n1 && j < n2) {
                if (left[i] <= right[j]) {
                    arr[k] = left[i];
                    i++;
                }
                else {
                    arr[k] = right[j];
                    j++;
                }
                k++;
            }

            // Copy the remaining elements of left[], if any
            while (i < n1) {
                arr[k] = left[i];
                i++;
                k++;
            }

            // Copy the remaining elements of right[], if any
            while (j < n2) {
                arr[k] = right[j];
                j++;
                k++;
            }
        }
    };

} // namespace AESort


```