# SelectionSort

```cpp
#pragma once

#include "ISort.h"
#include <vector>
#include <algorithm> // for std::swap

namespace AESort {

    template <typename T>
    class SelectionSort : public ISort<T> {
    public:
        bool sort(T* arr, size_t begin, size_t end) override {
            if (arr == nullptr || end == 0) return false;
            for (size_t last = end - 1; last > begin; last--) {
                size_t largest = findIndexOfLargest(arr, last + 1);
                std::swap(arr[largest], arr[last]);
            }
            return true; // Ensure the function returns true after sorting
        }

        bool sort(std::vector<T>& arr, size_t begin, size_t end) override {
            if (begin >= end) return false;
            for (size_t last = end - 1; last > begin; last--) {
                size_t largest = findIndexOfLargest(arr, last + 1);
                std::swap(arr[largest], arr[last]);
            }
            return true; // Ensure the function returns true after sorting
        }

    private:
        size_t findIndexOfLargest(const T* arr, size_t size) {
            size_t highestIndex = 0;
            for (size_t i = 1; i < size; i++) {
                if (arr[i] > arr[highestIndex]) {
                    highestIndex = i;
                }
            }
            return highestIndex;
        }

        size_t findIndexOfLargest(const std::vector<T>& arr, size_t size) {
            size_t highestIndex = 0;
            for (size_t i = 1; i < size; i++) {
                if (arr[i] > arr[highestIndex]) {
                    highestIndex = i;
                }
            }
            return highestIndex;
        }
    };

} // namespace AESort



```