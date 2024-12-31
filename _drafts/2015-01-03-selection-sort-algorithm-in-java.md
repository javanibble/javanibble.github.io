---
layout: post
title: Selection Sort Algorithm in Java
author: andre
categories: [ sort-algorithm ]
tags: [algorithm]
image: /assets/images/feature-images/feature-image-algorithms.png
description: This article gives provides an overview on Selection Sort together with an implementation in Java.
comments: true
---

- Table of Contents
{:toc .large-only}

Selection sort is a sorting algorithm, specifically an in-place comparison sort and is used for sorting an array of integers. The algorithm divides the input list into two parts, sorted and unsorted. The algorithm looks for the largest element in the unsorted section and swap it with the last position in the unsorted partition.

## Algorithm Classification
The following table contains information about the analysis of the Selection Sort algorithm. It defines the worst, average and best cases in terms of time complexity and also the worst case in space complexity.

| Attribute | Value | 
|-----------|-------|
| Class | Sorting Algorithm | 
| Classification | Internal, In-place, Unstable Algorithm  | 
| Data Structure | Array | 
| Time Complexity: Best | Ω(n<sup>2</sup>) | 
| Time Complexity: Average | Θ(n<sup>2</sup>) | 
| Time Complexity: Worst | O(n<sup>2</sup>) | 
| Space Complexity: Worst | O(1) | 
{:.stretch-table}

Algorithm Classification: Selection Sort
{:.figcaption}

Please use the following [link][0] for an explanation on Big-O notation and what is good, fair and bad.

## Selection Sort In Java
The SelectionSort class implements the Selection Sort algorithm for sorting an array of integers.

```java
public final class SelectionSort {
    
    public void sort(int[] collection) {
        if (collection != null) {
            selectionSort(collection);
        } else {
            throw new IllegalArgumentException("Input paramenter for array to sort is null.");
        }
    }
    
    private void selectionSort(int[] collection) {
        int arrayLength = collection.length;
        
        for (int unsortIndex = arrayLength - 1; unsortIndex > 0; unsortIndex--) {
            int largest = 0;
            for (int i = 1; i <= unsortIndex; i++) {
                if (collection[i] > collection[largest]) {
                    largest = i;
                }
            }
            swap(collection, largest, unsortIndex);
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
The Selection Sort algorithm forms part of a larger group of sorting algorithms. Learning through experience is the reason I created this post about the implementation of the Selection Sort algorithm in Java. I have learned a lot about how others have solved the Selection Sort algorithm in other languages including different implementations in Java.

Learning how to solve difference problems and algorithms with certain techniques, one starts to develop certain pattern recognition abilities which will help you in future when similar problems arise.

[0]:http://www.bigocheatsheet.com/img/big-o-cheat-sheet-poster.png
[Code]:https://github.com/javanibble/java-algorithms/blob/master/sort/src/main/java/com/javanibble/algorithm/sort/SelectionSort.java




