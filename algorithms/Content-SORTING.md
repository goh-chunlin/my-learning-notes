# Sorting

## Bubble Sort

> Worst-case Performance: O(n^2)
> Best-case Performance: O(n)
> Average-case Performance: O(n^2)
> Worst-case Space Complexity: O(1)

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
