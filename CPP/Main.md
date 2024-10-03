# Main

```cpp

#include <iostream>
#include "BubbleSort.hpp"
#include "InsertionSort.hpp"
#include "SelectionSort.hpp"
#include "QuickSort.hpp"
int main() {
   const int MAX = 1000;
   Bag<int> rngBag = BagUtility::generateRandomBag(MAX, 0, 100);
   std::vector<int> bagVec = rngBag.toVector(); // Convert to vector for linear traversal
   size_t vsize = bagVec.size(); // For the vector size
   int arr[MAX]; // initialize the raw array
   for (size_t i = 0; i < MAX; i++) {
       arr[i] = bagVec.at(i);
   }
   size_t size = sizeof(arr) / sizeof(arr[0]); // for raw array size

   AESort::RadixSort<int> sorter;

   // Start timing
   auto start = std::chrono::high_resolution_clock::now();

   if (sorter.sort(arr, 0, size)) { // Pass size - 1 to avoid out-of-bounds, this goes for quicksort
       // End timing
       auto end = std::chrono::high_resolution_clock::now();
       std::chrono::duration<double> duration = end - start;

       std::cout << "Sorted array: ";
       for (size_t i = 0; i < size; ++i) {
           std::cout << arr[i] << " ";
       }
       std::cout << std::endl;

       // Set precision to 3 decimal places
       std::cout << std::fixed << std::setprecision(10);
       std::cout << "Sorting took " << duration.count() << " seconds." << std::endl;
   }
   else {
       std::cout << "Sorting failed." << std::endl;
   }
}

```