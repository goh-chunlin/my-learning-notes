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
