---
layout: post
title: Insertion Sort Algorithm in Java
author: andre
categories: [ sort-algorithm ]
tags: [algorithm]
image: /assets/images/feature-images/feature-image-algorithms.png
description: This article gives provides an overview on Insertion Sort together with an implementation in Java.
comments: true
---

- Table of Contents
{:toc .large-only}

Insertion sort is a sorting algorithm that builds the final sorted array (or list) one item at a time. The algorithm iterates over the list and removes the current element, finds the location within the sorted part of the list, and inserts it there.  This process is repeated until the whole list is sorted.

## Algorithm Classification
The following table contains information about the analysis of the Insertion Sort algorithm. It defines the worst, average and best cases in terms of time complexity and also the worst case in space complexity.

| Attribute | Value | 
|-----------|-------|
| Class | Sorting Algorithm | 
| Classification | Internal, In-place, Stable Algorithm  | 
| Data Structure | Array | 
| Time Complexity: Best  | Ω(n) | 
| Time Complexity: Average  | Θ(n<sup>2</sup>) | 
| Time Complexity: Worst  | O(n<sup>2</sup>) | 
| Space Complexity: Worst  | O(1) | 
{:.stretch-table}

Algorithm Classification: Insertion Sort
{:.figcaption}

Please use the following [link][0] for an explanation on Big-O notation and what is good, fair and bad.

## Insertion Sort In Java
The InsertionSort class implements the Insertion Sort algorithm for sorting an array of integers.

```java
public final class InsertionSort {
    
    public void sort(int[] collection) {
        if (collection != null) {
            insertionSort(collection);
        } else {
            throw new IllegalArgumentException("Input parameter for array to sort is null.");
        }
    } 
    
  
    private void insertionSort(int[] collection) {
        int arrayLength = collection.length;
        
        for (int unsortIndex = 1; unsortIndex < arrayLength;  unsortIndex++) {
            int newElement = collection[unsortIndex];
            int iterator = 0;

            for (iterator = unsortIndex; iterator > 0 && collection[iterator - 1] > newElement; iterator--) {
                collection[iterator] = collection[iterator - 1];
            }
            collection[iterator] = newElement;
        }
    }
}
```

## Sample Code (GitHub)
The code example can be downloaded from Github from the following [link][Code].

## Finally
The Insertion Sort algorithm forms part of a larger group of sorting algorithms. Learning through experience is the reason I created this post about the implementation of the Insertion Sort algorithm in Java. I have learned a lot about how others have solved the Insertion Sort algorithm in other languages including different implementations in Java.

Learning how to solve difference problems and algorithms with certain techniques, one starts to develop certain pattern recognition abilities which will help you in future when similar problems arise.

[0]:http://www.bigocheatsheet.com/img/big-o-cheat-sheet-poster.png
[Code]:https://github.com/javanibble/java-algorithms/blob/master/sort/src/main/java/com/javanibble/algorithm/sort/InsertionSort.java
