RadixSort

```cpp

#pragma once

#include <cstddef>     // For size_t
#include <type_traits> // For std::is_integral, std::make_unsigned
#include <cstring>     // For std::memset
#include <vector>


//TODO Allow Radix Sort to sort strings
namespace AESort {

	template <typename T>
	class RadixSort : public ISort<T> {
	public:
		// Ensure that T is an integral type
		static_assert(std::is_integral<T>::value, "RadixSort requires an integral type T");

		virtual ~RadixSort() = default;

		virtual bool sort(T* arr, size_t begin, size_t end) override {
			if (arr == nullptr || begin >= end) {
				return false;
			}

			// Number of elements to sort
			size_t n = end - begin;

			// Create a temporary array for output
			T* output = new (std::nothrow) T[n];
			if (!output) {
				return false; // Allocation failed
			}

			// Using UnsignedT for bit manipulation
			using UnsignedT = typename std::make_unsigned<T>::type;

			// Determine number of bits in T
			const size_t bitSize = sizeof(T) * 8;

			// Number of bits per digit (base 256)
			const size_t bitsPerDigit = 8;

			// Number of possible values per digit
			const size_t radix = 1 << bitsPerDigit; // 256

			// Number of digits to process
			const size_t numDigits = (bitSize + bitsPerDigit - 1) / bitsPerDigit;

			// Allocate count array
			size_t count[radix];

			// Perform radix sort
			for (size_t d = 0; d < numDigits-1; ++d) {
				// Initialize count array
				std::memset(count, 0, sizeof(count));

				// Count occurrences of each digit value
				for (size_t i = 0; i < n; ++i) {
					UnsignedT val = static_cast<UnsignedT>(arr[begin + i]);
					size_t digit = (val >> (d * bitsPerDigit)) & (radix - 1);
					++count[digit];
				}

				if (d < numDigits - 1) {
					// Accumulate counts for digits (standard counting sort)
					for (size_t i = 1; i < radix; ++i) {
						count[i] += count[i - 1];
					}
				}
				else {
					// Adjust counts for the most significant digit to handle negative numbers
					size_t cumulativeCount = 0;

					// Process negative numbers (sign bit = 1)
					for (size_t i = radix / 2; i < radix; ++i) {
						size_t temp = count[i];
						count[i] = cumulativeCount;
						cumulativeCount += temp;
					}

					// Process positive numbers (sign bit = 0)
					for (size_t i = 0; i < radix / 2; ++i) {
						size_t temp = count[i];
						count[i] = cumulativeCount;
						cumulativeCount += temp;
					}
				}

				// Build the output array using the counts
				for (std::ptrdiff_t i = n - 1; i >= 0; --i) {
					UnsignedT val = static_cast<UnsignedT>(arr[begin + i]);
					size_t digit = (val >> (d * bitsPerDigit)) & (radix - 1);
					--count[digit];
					output[count[digit]] = arr[begin + i];
				}


				// Copy the output array back to the original array
				for (size_t i = 0; i < n; ++i) {
					arr[begin + i] = output[i];
				}
			}

			delete[] output;

			return true;
		}

		virtual bool sort(std::vector<T>& arr, size_t begin, size_t end) {
			if (begin >= end) {
				return false;
			}

			// Number of elements to sort
			size_t n = end - begin;

			// Create a temporary array for output
			std::vector<T> output(n);

			// Using UnsignedT for bit manipulation
			using UnsignedT = typename std::make_unsigned<T>::type;

			// Determine number of bits in T
			const size_t bitSize = sizeof(T) * 8;

			// Number of bits per digit (base 256)
			const size_t bitsPerDigit = 8;

			// Number of possible values per digit
			const size_t radix = 1 << bitsPerDigit; // 256

			// Number of digits to process
			const size_t numDigits = (bitSize + bitsPerDigit - 1) / bitsPerDigit;

			// Allocate count array
			size_t count[radix];

			// Perform radix sort
			for (size_t d = 0; d < numDigits-1; ++d) {
				// Initialize count array
				std::memset(count, 0, sizeof(count));

				// Count occurrences of each digit value
				for (size_t i = 0; i < n; ++i) {
					UnsignedT val = static_cast<UnsignedT>(arr[begin + i]);
					size_t digit = (val >> (d * bitsPerDigit)) & (radix - 1);
					++count[digit];
				}

				if (d < numDigits - 1) {
					// Accumulate counts for digits (standard counting sort)
					for (size_t i = 1; i < radix; ++i) {
						count[i] += count[i - 1];
					}
				}
				else {
					// Adjust counts for the most significant digit to handle negative numbers
					size_t cumulativeCount = 0;

					// Process negative numbers (sign bit = 1)
					for (size_t i = radix / 2; i < radix; ++i) {
						size_t temp = count[i];
						count[i] = cumulativeCount;
						cumulativeCount += temp;
					}

					// Process positive numbers (sign bit = 0)
					for (size_t i = 0; i < radix / 2; ++i) {
						size_t temp = count[i];
						count[i] = cumulativeCount;
						cumulativeCount += temp;
					}
				}

				// Build the output array using the counts
				for (std::ptrdiff_t i = n - 1; i >= 0; --i) {
					UnsignedT val = static_cast<UnsignedT>(arr[begin + i]);
					size_t digit = (val >> (d * bitsPerDigit)) & (radix - 1);
					--count[digit];
					output[count[digit]] = arr[begin + i];
				}

				// Copy the output array back to the original array
				for (size_t i = 0; i < n; ++i) {
					arr[begin + i] = output[i];
				}
			}

			return true;
		}
	};

};

// namespace AESort



```