# InsertionSort

```cpp
#pragma once

#include "ISort.h"

namespace AESort {

	template <typename T>
	class InsertionSort : public ISort<T> {
	public:



		bool sort(T* arr, size_t begin, size_t end) override {
			if (arr == nullptr || begin >= end) return false;

			for (size_t i = begin + 1; i < end; i++) {
				T next = arr[i];
				size_t position = i;
				while ((position > begin) && arr[position - 1] > next) {
					arr[position] = arr[position - 1];
					position--;
				}
				arr[position] = next;
			}

			return true;
		}


		bool sort(std::vector<T>& arr, size_t begin, size_t end) override {
			if (begin >= end) return false;

			for (size_t i = begin + 1; i < end; i++) {
				T next = arr[i];
				size_t position = i;
				while ((position > begin) && arr[position - 1] > next) {
					arr[position] = arr[position - 1];
					position--;
				}
				arr[position] = next;
			}

			return true;
		}

	};

}

// namespace AESort

```