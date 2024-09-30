# Sort Interface

```cpp
#pragma once

namespace AESort {

    template <typename T>
    class ISort {
    public:
        virtual ~ISort() = default; // Virtual destructor for proper cleanup of derived classes
        virtual bool sort(T* arr, size_t begin, size_t end) = 0;
    };

} // namespace AESort


```