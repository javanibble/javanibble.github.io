---
layout: post
title: Quick Sort Algorithm in Java
author: andre
categories: [ sort-algorithm ]
tags: [algorithm]
image: /assets/images/feature-images/feature-image-algorithms.png
description: This article gives provides an overview on Quick Sort together with an implementation in Java.
comments: true
---

- Table of Contents
{:toc .large-only}

Quick Sort, also known as partition-exchange sort, is an efficient divide and conquer sorting algorithm. The algorithm can be implemented making use of loops or recursions. The algorithm performs the sorting in-place. Quick Sort is a comparison sort, meaning that it can sort items of any type for which a "less-than" relation is defined.

The algorithm divides the array into two smaller sub-arrays. To divide the algorithm into two array, an pivot or element within the array is chosen. The partition phase consist of reordering the array so that all elements with values less than the pivot come before the pivot, while all elements with values greater than the pivot come after it. After the partition phase, the pivot is in its final position. The pivot logically splits the original array into two sub-arrays. The Quick Sort algorithm then recursively sort the sub-arrays by selecting a new pivot and move the values accordingly. Every element will be selected as the pivot and will be placed in the correct position.

## Algorithm Classification
The following table contains information about the analysis of the Quick Sort algorithm. It defines the worst, average and best cases in terms of time complexity and also the worst case in space complexity.

| Attribute | Value | 
|-----------|-------|
| Class | Sorting Algorithm | 
| Classification | Internal, In-place, Unstable Algorithm  | 
| Data Structure | Array | 
| Time Complexity: Best | Ω(n log(n)) | 
| Time Complexity: Average | Θ(n log(n)) | 
| Time Complexity: Worst | O(n<sup>2</sup>) | 
| Space Complexity: Worst | O(n log(n)) | 
{:.stretch-table}

Algorithm Classification: Quick Sort
{:.figcaption}

Please use the following [link][0] for an explanation on Big-O notation and what is good, fair and bad.

## Quick Sort In Java
The QuickSort class implements the Quick Sort algorithm for sorting an array of integers.

```java
public final class QuickSort {
    
    public void sort(int[] collection) {
        if (collection != null) {
            quickSort(collection, 0, collection.length-1);
        } else {
            throw new IllegalArgumentException("Input paramenter for array to sort is null.");
        }
    } 

    private void quickSort(int[] collection, int firstPosition, int lastPosition) {
        if (firstPosition >= lastPosition) {
            return;
        } else {            
            int pivotIndex = partition(collection, firstPosition, lastPosition);
            quickSort(collection, firstPosition, pivotIndex-1);
            quickSort(collection, pivotIndex+1, lastPosition);
        }         
    } 

    private int partition(int[] collection, int firstPosition, int lastPosition) {    
        int pivotIndex = selectPivot(firstPosition, lastPosition);
        swap (collection, pivotIndex, lastPosition);
        int store = firstPosition;
        pivotIndex = lastPosition;
        for (int i = firstPosition; i <= lastPosition-1 ; i++) {
            if (collection[i] <= collection[pivotIndex]) {
                swap (collection, i, store);
                store++;
            }
        }
        swap (collection, store, pivotIndex);
        pivotIndex = store;
        return pivotIndex;
    }     
    
    private void swap(int[] collection, int x, int y) {
        int temp = collection[x];
        collection[x] = collection[y];
        collection[y] = temp;
    } 

    private int selectPivot(int first, int last) {
        return (first+last)/2;
    } 

}
```

## Sample Code (GitHub)
The code example can be downloaded from Github from the following [link][Code].

## Finally
The Quick Sort algorithm forms part of a larger group of sorting algorithms. Learning through experience is the reason I created this post about the implementation of the Quick Sort algorithm in Java. I have learned a lot about how others have solved the Quick Sort algorithm in other languages including different implementations in Java.

Learning how to solve difference problems and algorithms with certain techniques, one starts to develop certain pattern recognition abilities which will help you in future when similar problems arise.

[0]:http://www.bigocheatsheet.com/img/big-o-cheat-sheet-poster.png
[Code]:https://github.com/javanibble/java-algorithms/blob/master/sort/src/main/java/com/javanibble/algorithm/sort/QuickSort.java