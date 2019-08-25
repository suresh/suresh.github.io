
title: "Binary Search Algorithm"
description: "Portland in shoreditch Vice, labore typewriter pariatur hoodie fap sartorial Austin. Pinterest literally occupy Schlitz forage."
category: articles
tags: [sample post, readability, test]
---
Want to learn more? Check out [Data Structures and Algorithms in Python](http://amzn.to/2kjkqWQ)

## Create Sorted List

We need a sorted list for binary search algorithm. This can be created using these two lines:

```python
sorted_list = list(range(20))

sorted_list
```

[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]

## Create A Binary Search Algorithm

```python
# Define a function that takes a sorted list and the value we want to find,
def binary_search(sorted_list, target):

    # Set the initial search area to be the whole list
    search_area = sorted_list

    # While the search area has at least 1 element,
    while len(search_area) >= 1:

        # Print the current search area:
        print('Search area:', search_area)

        # Create the index of the last element
        end = len(search_area) - 1

        # Create the index of the first element
        middle = int((0 + end)/2)

        # If target is smaller than the middle value of the search area
        if target < search_area[middle]:
            # Make the new search area the first half of the current search area
            search_area = search_area[:middle]

        # If target is greater than the middle value of the search area
        elif target > search_area[middle]:
            # Make the new search area the second half of the current search area
            search_area = search_area[middle:]

        # If the target is equal to the middle value of the search area:
        else:
            # Print success!
            return print('Found it!', str(search_area[middle]))
    # If the list area has 0 elements, print that search failed
    else:
        return print('Not in list!')

# Run function
binary_search(sorted_list, 7)
```

Search area: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
Search area: [0, 1, 2, 3, 4, 5, 6, 7, 8]
Search area: [4, 5, 6, 7, 8]
Search area: [6, 7, 8]
Found it! 7
