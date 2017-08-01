# Sorting

## Bubble Sort

Bubble sort is a **Comparison Sort** that repeatedly steps through the list to be sorted, compares each pair of adjacent items and swaps them if they are in the wrong order. The pass through the list is **repeated until no swaps are needed**, which indicates that the list is sorted.

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
