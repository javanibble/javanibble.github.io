---
layout: post
title: Bubble Sort Algorithm in Java
author: andre
categories: [ sort-algorithm ]
tags: [algorithm]
image: /assets/images/feature-images/feature-image-algorithms.png
description: This article gives provides an overview on Bubble Sort together with an implementation in Java.
comments: true
---

- Table of Contents
{:toc .large-only}

Bubble sort is sometimes referred to as sinking sort. The bubble sort algorithm repeatedly steps through the list and compare each adjacent item. The pair of values gets swapped if they are in the wrong order. The algorithm gets its name from the way smaller or larger elements “bubble” to the top of the list.

## Algorithm Classification
The following table contains information about the analysis of the BubbleSort algorithm. It defines the worst, average and best cases in terms of time complexity and also the worst case in space complexity.

| Attribute | Value | 
|-----------|-------|
| Class | Sorting Algorithm |
| Classification | Internal, In-place, Stable Algorithm  |
| Data Structure | Array |
| Time Complexity: Worst | O(n<sup>2</sup>) |
| Time Complexity: Average | O(n<sup>2</sup>) |
| Time Complexity: Best | O(n) |
| Space Complexity: Worst | O(1) |
{:.stretch-table}

Algorithm Classification: Bubble Sort
{:.figcaption}

Please use the following [link][0] for an explanation on Big-O notation and what is good, fair and bad.

## Pseudo-Code
This algorithm works by repeatedly iterating through the list of items and comparing adjacent elements. If an element is found to be larger than its neighbor, it is swapped with that element. This process is repeated until the list is sorted in ascending order.

```
procedure bubbleSort(list)
    n = length of list
    for i = 0 to n-1
        for j = 0 to n-i-1
            if list[j] > list[j+1]
                swap(list[j], list[j+1])
```

The outer loop (the one with the variable i) is used to track the number of passes that have been made over the list. The inner loop (the one with the variable j) is used to compare the adjacent elements and perform the swap, if necessary.

The pseudo-code above uses a simple implementation of the bubble sort algorithm. There are several ways to optimize this algorithm, such as adding a flag to track whether any swaps were made during a pass, or using a more efficient sorting algorithm for lists that are already partially sorted.


## BubbleSort In Java
The BubbleSort class implements the BubbleSort algorithm for sorting an array of integers.

```java
public final class BubbleSort {

    public void sort(int[] collection) {
        if (collection != null) {
            bubbleSort(collection);
        } else {
            throw new IllegalArgumentException("Input parameter for array to sort is null.");
        }
    }

    private void bubbleSort(int[] collection) {
        int n = collection.length;
        for (int i = 0; i < n-1; i++) {
            for (int j = 0; j < n-i-1; j++) {
                if (collection[j] > collection[j+1]) {
                    swap(collection, j, j+1);
                }
            }
        }
    }

    private void swap(int[] collection, int x, int y) {
        int temp = collection[x];
        collection[x] = collection[y];
        collection[y] = temp;
    }

}
```

## Sample Code (GitHub)
The code example can be downloaded from Github from the following [link][Code].

## Finally
The BubbleSort algorithm forms part of a larger group of sorting algorithms. Learning through experience is the reason I created this post about the implementation of the BubbleSort algorithm in Java. I have learned a lot about how others have solved the BubbleSort algorithm in other languages including different implementations in Java.

Learning how to solve difference problems and algorithms with certain techniques, one starts to develop certain pattern recognition abilities which will help you in future when similar problems arise.

[0]:http://www.bigocheatsheet.com/img/big-o-cheat-sheet-poster.png
[Code]:https://github.com/javanibble/java-algorithms/blob/master/sort/src/main/java/com/javanibble/algorithm/sort/BubbleSort.java