# Sorting

## Sorting

time           | best        | worst
---------------|-------------|-------
bubble sort    | O(n)        | O(n^2)
selection sort | O(n^2)      | O(n^2)
insertion sort | O(n)        | O(n^2)
merge sort     | O(nlog n)   | O(nlog n)
quick sort     | O(nlog n)   | O(n^2)
bucket sort    | O(n + k)    | O(n^2)

--             | time | space
---------------|------|------
counting sort  | O(n) | O(k)

space          | best        | worst
---------------|-------------|----------
merge sort     | O(n)        | O(n)
quick sort     | O(log n)    | O(n)

### Bubble Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/bubble-sort-complexity.png)

--          | best  | worst
------------|-------|-------
bubble sort | O(n)  | O(n^2)

* **Ascending Order**

        public void sort(T[] array) {
            for(int i=0;i<array.length;i++) {
                for (int j = 1; j < array.length - i; j++) {
                    if (array[j].compareTo(array[j - 1]) < 0) {
                        swap(array, j, j - 1);
                    }
                }
            }
        }

* **Optimized**

        public void sortOptimized(T[] array) {
            for(int i=0;i<array.length;i++) {
                boolean isSorted = true;
                for (int j = 1; j < array.length - i; j++) {
                    if (array[j].compareTo(array[j - 1]) < 0) {
                        swap(array, j, j - 1);
                        isSorted = false;
                    }
                }

                if(isSorted)
                    return;
            }
        }

### Selection Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/selection-sort-complexity.png)

--             | best   | worst
---------------|--------|-------
selection sort | O(n^2) | O(n^2)

* **steps**
    * pick the minimum element and swap with the first element.
    * do that again for the (n-1) elements.

* **Ascending Order**

        public void sort(T[] array) {
            for(int i=0;i<array.length;i++) {
                swap(array, minIndex(array, i), i);
            }
        }

        private int minIndex(T[] array, int startIndex) {
            int minIndex = startIndex;
            for(int j=startIndex;j<array.length;j++) {
                if(array[j].compareTo(array[minIndex]) < 0) {
                    minIndex = j;
                }
            }
            return minIndex;
        }

### Insertion Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/insertion-sort-complexity.png)

--             | best   | worst
---------------|--------|-------
insertion sort | O(n)   | O(n^2)

* **steps**
    * start with the first element and start to insert second element to it.
    * as in cards sort elment while inserting it.
    * do the same till the end of the array.

* **Ascending Order**

        public void sort(T[] array) {
            for(int i=1;i<array.length;i++) {
                T current = array[i];
                int j = i - 1;
                while(j>=0 && array[j].compareTo(current) > 0) {
                    array[j + 1] = array[j];
                    j--;
                }
                array[j + 1] = current;
            }
        }

### Merge Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/merge-sort-complexity.png)

time           | best        | worst
---------------|-------------|----------
merge sort     | O(nlog n)   | O(nlog n)

space          | best        | worst
---------------|-------------|----------
merge sort     | O(n)        | O(n)

* **Ascending Order**

        public void sort(T[] array) {
            if(array.length < 2)
                return;

            int middle = array.length / 2;
            T[] left = (T[]) new Number[middle];
            T[] right = (T[]) new Number[array.length - middle];
            for(int i=0;i<array.length;i++) {
                if(i < middle)
                    left[i] = array[i];
                else
                    right[i-middle] = array[i];
            }

            sort(left);
            sort(right);

            merge(left, right, array);
        }

        private void merge(T[] left, T[] right, T[] result) {
            int i = 0, j = 0, k = 0;
            while(i < left.length && j < right.length) {
                if(left[i].compareTo(right[j]) <= 0)
                    result[k++] = left[i++];
                else
                    result[k++] = right[j++];
            }

            //remaining items
            while(i < left.length)
                result[k++] = left[i++];

            while(j<right.length)
                result[k++] = right[j++];
        }

* **In place implementation**

### Quick Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/quick-sort-complexity.png)

time           | best        | worst
---------------|-------------|----------
quick sort     | O(nlog n)   | O(n^2)

* **space because of stack calls**

space          | best        | worst
---------------|-------------|----------
quick sort     | O(log n)    | O(n)

* **steps**
    * choose an element as a pivot. (last element)
    * rearrange array so all smaller elements are to the left of pivot and greater elements to the right.
    * now this pivot in the right place.
    * repeat for all elements

* **Ascending Order**

        public void sort(T[] array) {
            sort(array, 0, array.length - 1);
        }

        private void sort(T[] array, int start, int end) {
            if(start >= end)
                return;

            //index of the pivot
            int boundary = partitioning(array, start, end);

            sort(array, start, boundary - 1);
            sort(array, boundary + 1, end);
        }

        private int partitioning(T[] array, int start, int end) {
            T pivot = array[end];
            int boundary = start - 1;  //left partition ref.

            for(int i=start;i<=end;i++)
                if(array[i].compareTo(pivot) <= 0)
                    swap(array, i, ++boundary);

            return boundary;
        }

### Counting Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/counting-sort.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/counting-sort-complexity.png)

--             | time | space
---------------|------|------
counting sort  | O(n) | O(k)

* **steps**
    * generate array of size k to count elements.
    * loop throw counts and generate ordered array.

* **Ascending Order**

        public void sort(int[] array, int max) {
            int[] counts = new int[max + 1];
            for(int item : array) {
                counts[item]++;
            }

            int index = 0;
            for(int i=0;i<counts.length;i++) {
                for(int j=0;j<counts[i]; j++) {
                    array[index++] = i;
                }
            }
        }

### Bucket Sort
![](https://github.com/shamy1st/algorithms/blob/main/images/bucket-sort.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/bucket-sort-complexity.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/bucket-sort-graph.png)

--             | best     | worst
---------------|----------|-------
bucket sort    | O(n + k) | O(n^2)

* **steps**
    * distribute elements to buckets.
    * sort each bucket using any sorting technique.
    * iterate throw buckets and generate ordered array.

* **Ascending Order**

        public void sort(T[] array, int numOfBuckets) {
            List<List<T>> buckets = new ArrayList<>();
            for(int i=0;i<numOfBuckets;i++)
                buckets.add(new ArrayList<>());

            for(T item : array)
                buckets.get((Integer)item / numOfBuckets).add(item);

            int index = 0;
            for(var bucket : buckets) {
                Collections.sort(bucket);
                for(var item : bucket)
                    array[index++] = item;
            }
        }
        
