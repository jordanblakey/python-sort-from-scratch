# python-sort-from-scratch
## Recreating Python sorting algorithms to benchmark and understand them better.

```python
import random
import time

def random_items(n=5000):
    return [random.randint(-50, 100) for c in range(n)]


# BUBBLE SORT ALGORITHM
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items)-1-i):
            if items[j] > items[j+i]:
                items[j], items[j+i] = items[j+1], items[j] #Swap!

# Testing Bubble Sort
print 'Bubble Sorting 5000 integers... '#, random_items
start = time.time() * 1000
bubble_sort(random_items())
end = time.time() * 1000
print 'Sorted! (Milliseconds elapsed:', end - start, ') ' #, random_items


# INSERTION SORT
def insertion_sort(items):
    for i in range(1, len(items)):
        j = i
        while j > 0 and items[j] < items[j-1]:
            items[j], items[j-1] = items[j-1], items[j]
            j -= 1

# Testing Insertion Sort
print 'Insertion Sorting 5000 integers...'
start = time.time() * 1000
insertion_sort(random_items())
end = time.time() * 1000
print 'Sorted! (Milliseconds elapsed:', end - start, ')'


# MERGE SORT
def merge_sort(x):
    result = []
    if len(x) < 20:
        return sorted(x)
    mid = int(len(x) / 2)
    y = merge_sort(x[:mid])
    z = merge_sort(x[mid:])
    i = 0
    j = 0
    while i < len(y) and j < len(z):
        if y[i] > z[j]:
            result.append(z[j])
            j += 1
        else:
            result.append(y[i])
            i += 1
    result += y[i:]
    result += z[j:]
    return result

# Testing Merge Sort
print 'Merge Sorting 5000 integers...'
start = time.time() * 1000
merge_sort(random_items())
end = time.time() * 1000
print 'Sorted! (Milliseconds elapsed:', end - start, ')'


# QUICK SORT
def quick_sort(items):
    if len(items) > 1:
        pivot_index = len(items) / 2
        smaller_items = []
        larger_items = []

        for i, val in enumerate(items):
            if i != pivot_index:
                if val < items[pivot_index]:
                    smaller_items.append(val)
                else:
                    larger_items.append(val)

        quick_sort(smaller_items)
        quick_sort(larger_items)
        items[:] = smaller_items + [items[pivot_index]] + larger_items

# Testing Quick Sort
print 'Quick Sorting 5000 integers...'
start = time.time() * 1000
quick_sort(random_items())
end = time.time() * 1000
print 'Sorted! (Milliseconds elapsed:', end - start, ')'


# Testing Built-in .sorted Method
print '.sorted Sorting 5000 integers...'
start = time.time() * 1000
sorted(random_items())
end = time.time() * 1000
print 'Sorted! (Milliseconds elapsed:', end - start, ')'
```
