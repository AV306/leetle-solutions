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
