# Day 22 - Merging Sorted Arrays

Since the arrays are already sorted, we just need to "interleave" them together.

```
list1 = [1, 3, 4, 7]
list2 = [2, 5, 6, 9]

list1: [1]     [3] [4]         [7]
list2:     [2]         [5] [6]         [9]

answer = [1, 2, 3, 4, 5, 6, 7, 9]
```

```python
def solve(list1, list2):
  newList = [];
  # The indexes for each list
  i = 0;
  j = 0;

  while i < len( list1 ) or j < len( list2 ):
    # Out-of-range for list 1; keep adding list 2
    # Could use slices or something but this worked
    if i >= len( list1 ):
      newList.append( list2[j] );
      j += 1;
      continue;

    # OOR on list 2; keep adding list 1
    if j >= len( list2 ):
      newList.append( list1[i] );
      i += 1;
      continue;

    # Compare the two values on each list we're looking at
    if list1[i] < list2[j]:
      # Append the list1 value and shift to the next list1 value
      newList.append( list1[i] );
      i += 1;
    else:
      # Append the list2 value and shift to the next list2 value
      newList.append( list2[j] );
      j += 1;
    
  return newList;
```

`i` and `j` will show a pattern like (0, 0), (1, 0), (1, 1)... as we compare each `list1` element with indices "next to" (difference ≤ 1) the index of the current `list2` element to determine the order in which we interleave them.

It's like sorting two (sorted) stacks of numbered pages into one new stack - you look at the two topmost pages, put the smaller-numbered (or bigger, whichever direction you're sorting) page onto the new stack, then compare the two new topmost pages and repeat.


# Day 24 - Minimum Rotated Sorted Array

A much easier version of the LeetCode problem. Given a sorted array that has been shifted in a circular manner (with wrapping) by some amount in either direction, find the smallest element.

Observe that the array will have two sections, each sorted and separated by a "drop" - e.g. [4, 5, 6, 1, 2, 3] (the first section can have length 0, i.e. the array was not shifted.

The smallest element will be the one just after the "drop". We can identify the drop by comparing each element with the one before it, starting from the second element.

```python
def solve( nums ):
  if len( nums ) == 1:
    return nums[0];

  # Starting from 1 works for Leetle, but it won't
  # work for the case where the array has not been rotated.
  # Since python supports negative indices, starting from 0
  # works here, but may jot work in other languages.
  for i in range( 0, len( nums ) ):
    if nums[i] > nums[i-1]:
      # Still in the ascending section
      continue;

    return nums[i];
```

# Day 31 - Length of Last Word

The catch here is that test-case 2 has an extra space at the end (or something to that effect), so if you simply `s.split( " " )[-1]` you'll get a string of length 0 instead of the last word.

```python
def solve(s):
  last = s.strip().split( " " )[-1];
  return len( last );
```
