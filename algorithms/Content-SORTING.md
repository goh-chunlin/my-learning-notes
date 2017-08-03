# Sorting

## Bubble Sort

> Worst-case Performance: O(n^2)    
> Best-case Performance: O(n)    
> Average-case Performance: O(n^2)    
> Worst-case Space Complexity: O(1) of additional memory space    

Bubble Sort is a **Comparison Sort** that repeatedly steps through the list to be sorted, compares each pair of adjacent items and swaps them if they are in the wrong order. The pass through the list is **repeated until no swaps are needed**, which indicates that the list is sorted.

```
private static int[] Sort(int[] source)
{
    bool isAllElementsSorted = true;

    do
    {
        isAllElementsSorted = true;

        for (int i = 0; i < source.Length; i++)
        {
            if (i == source.Length - 1) break;

            if (source[i] > source[i + 1])
            {
                isAllElementsSorted = false;

                int temp = source[i];

                source[i] = source[i + 1];
                source[i + 1] = temp;
            }
        }
    } while (!isAllElementsSorted);

    return source;
}
```

The bubble sort algorithm can be easily optimized by observing that the n-th pass finds the n-th largest element and puts it into its final place. So, the inner loop can avoid looking at the last n − 1 items when running for the n-th time.

```
private static int[] Sort(int[] source)
{
    bool isAllElementsSorted = true;
    
    int count = 0;

    do
    {
        isAllElementsSorted = true;

        for (int i = 0; i < source.Length; i++)
        {
            if (i == source.Length - (count + 1)) break;

            if (source[i] > source[i + 1])
            {
                isAllElementsSorted = false;

                int temp = source[i];

                source[i] = source[i + 1];
                source[i + 1] = temp;
            }
        }

        count++;
    } while (!isAllElementsSorted);

    return source;
}
```

## Insertion Sort

> Worst-case Performance: O(n^2)    
> Best-case Performance: O(n)    
> Average-case Performance: O(n^2)    
> Worst-case Space Complexity: O(1) of additional memory space    

Insertion Sort iterates up the array and grows the sorted list in front of each array-position. It checks the value there against the largest value in the sorted list. If larger, it leaves the element in place and moves to the next. If smaller, it finds the correct position within the sorted list, shifts all the larger values up to make a space, and inserts into that correct position.

```
private static int[] Sort(int[] source)
{
    for (int i = 1; i < source.Length; i++)
    {
        for (int j = i; j > 0; j--)
        {
            if (source[j - 1] <= source[j])
            {
                break;
            }
            else
            {
                int temp = source[j];

                source[j] = source[j - 1];
                source[j - 1] = temp;
            }
        }
    }

    return source;
}
```

## Selection Sort

> Worst-case Performance: O(n^2)    
> Best-case Performance: O(n^2)    
> Average-case Performance: O(n^2)    
> Worst-case Space Complexity: O(1) of additional memory space    

Selection Sort scans through the unsorted data looking for the smallest remaining element, then swap it into the position immediately following the sorted data. Repeat until finished.

The logic for both Insertion Sort and Selection Sort is quite similar. They both have a partially sorted sub-array in the beginning of the array. The only difference is how they search for the next element to be put in the sorted array.

 - Insertion Sort: Inserts the next element at the correct position;
 - Selection sort: Selects the smallest element and exchange it with the current item.

```
private static int[] Sort(int[] source)
{
    int indexOfSmallestElementInUnsortedSubArray = 1;

    for (int round = 0; round < source.Length; round++)
    {
        int temp = source[round];

        for (int i = (round + 1); i < source.Length; i++)
        {
            if (source[i] < source[indexOfSmallestElementInUnsortedSubArray])
            {
                indexOfSmallestElementInUnsortedSubArray = i;
            }
        }

        source[round] = source[indexOfSmallestElementInUnsortedSubArray];
        source[indexOfSmallestElementInUnsortedSubArray] = temp;
    }

    return source;
}
```

## Merge Sort

> Worst-case Performance: O(n logn)    
> Best-case Performance: O(n logn)    
> Average-case Performance: O(n logn)    
> Worst-case Space Complexity: O(n) of additional memory space    

A merge sort works as follows:
1. Divide the unsorted list into n sublists, each containing 1 element (a list of 1 element is considered sorted);
2. Repeatedly merge sublists to produce new sorted sublists until there is only 1 sublist remaining. This will be the sorted list.

```
private static int[] Sort(int[] source)
{
    MainSort(source, 0, source.Count() - 1);

    return source;
}

private static void MainSort(int[] source, int startIndex, int endIndex)
{
    if (startIndex < endIndex)
    {
        int middleIndex = (startIndex + endIndex) / 2;

        MainSort(source, startIndex, middleIndex);
        MainSort(source, middleIndex + 1, endIndex);

        Merge(source, startIndex, middleIndex, endIndex);
    }
}

private static void Merge(int[] source, int startIndex, int middleIndex, int endIndex)
{
    int[] temp = new int[endIndex - startIndex + 1];

    int leftSubArrayIndex = startIndex;
    int rightSubArrayIndex = middleIndex + 1;

    for (int i = 0; i < temp.Count(); i++)
    {
        if (leftSubArrayIndex > middleIndex)
        {
            temp[i] = source[rightSubArrayIndex];

            rightSubArrayIndex++;
        }
        else if (rightSubArrayIndex > endIndex)
        {
            temp[i] = source[leftSubArrayIndex];

            leftSubArrayIndex++;
        }
        else if (source[leftSubArrayIndex] >= source[rightSubArrayIndex])
        {
            temp[i] = source[rightSubArrayIndex];

            rightSubArrayIndex++;
        }
        else
        {
            temp[i] = source[leftSubArrayIndex];

            leftSubArrayIndex++;
        }
    }

    for (int i = 0; i < temp.Count(); i++)
    {
        source[startIndex + i] = temp[i];
    }
}
```

## Quick Sort

## Heap Sort
