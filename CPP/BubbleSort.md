# BubbleSort


```cpp

#pragma once

#include "ISort.h"

namespace AESort {

    template <typename T>
    class BubbleSort : public ISort<T> {
    public:


        bool sort(T* arr, size_t begin, size_t end) override {
            if (arr == nullptr || end == 0) return false;

            for (size_t i = 0; i < end - 1; ++i) {
                for (size_t j = 0; j < end - i - 1; ++j) {
                    if (arr[j] > arr[j + 1]) {
                        std::swap(arr[j], arr[j + 1]);
                    }
                }
            }

            return true;
        }

    };

} // namespace AESort

```