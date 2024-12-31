---
layout: post
title: Counting Sort Algorithm in Java
author: andre
categories: [ sort-algorithm ]
tags: [algorithm]
image: /assets/images/feature-images/feature-image-algorithms.png
description: This article gives provides an overview on Counting Sort together with an implementation in Java.
comments: true
---

- Table of Contents
{:toc .large-only}


Counting Sort is an integer sorting algorithm. Counting Sort are unlike other sorting algorithms in that it makes certain assumptions about the data. It counts the number of objects with a distinct key value, and use arithmetic to determine the position of each key. This algorithm does not make use of comparisons to sort the values. In simplistic terms, the algorithm counts the number of occurrences of each value in order to sort it.

The initial phase of the algorithm is to start counting the number of occurrences of the values within the array and increment the value associated with the counting key. The second phase is to write out the new sorted array making use of the number of occurrences of each of the counting keys.

## Algorithm Classification
The following table contains information about the analysis of the Counting Sort algorithm. It defines the worst, average and best cases in terms of time complexity and also the worst case in space complexity.

| Attribute | Value | 
|-----------|-------|
| Class | Sorting Algorithm | 
| Classification | Internal, Not In-place Algorithm  | 
| Data Structure | Array | 
| Time Complexity: Best | Ω(n+k) | 
| Time Complexity: Average | Θ(n+k) | 
| Time Complexity: Worst | O(n+k) | 
| Space Complexity: Worst | O(k) | 
{:.stretch-table}

Algorithm Classification: Counting Sort
{:.figcaption}

Please use the following [link][0] for an explanation on Big-O notation and what is good, fair and bad.

## Counting Sort In Java
The CountingSort class implements the Counting Sort algorithm for sorting an array of integers.

```java
public final class CountingSort {
    
    public void sort(int[] collection) {
        if (collection != null) {
            int maxValue = findMaxValue(collection);
            countingSort(collection, maxValue);
        } else {
            throw new IllegalArgumentException("Input paramenter for array to sort is null.");
        }
    }
    
    private void countingSort(int[] collection, int maxValue) {
        int[] countArray = countOccurrences(collection, maxValue);
        reconstructArray(collection, countArray, maxValue);
    }
    
    private int findMaxValue(int[] collection) {
        int highest = collection[0];
        for (int index = 1; index < collection.length; index ++) {
            if (collection[index] > highest) {
                highest = collection [index];
            }
        }
        return highest;
    }
    
    private int[] countOccurrences(int[] collection, int maxValue) {
        int[] tempArray = new int[maxValue + 1];
        for (int i = 0; i < collection.length; i++) {
            int key = collection[i];
            tempArray[key]++;
        }    
        return tempArray;
    }
    
    private void reconstructArray(int[] collection, int[] countArray, int maxValue) {
        int j = 0;
        for (int i = 0; i <= maxValue; i++) {
            while (countArray[i] > 0) {
                collection[j++] = i;
                countArray[i]--;
            }
        }
    }
}
```

## Sample Code (GitHub)
The code example can be downloaded from Github from the following [link][Code].

## Finally
The Counting Sort algorithm forms part of a larger group of sorting algorithms. Learning through experience is the reason I created this post about the implementation of the Counting Sort algorithm in Java. I have learned a lot about how others have solved the Counting Sort algorithm in other languages including different implementations in Java.

Learning how to solve difference problems and algorithms with certain techniques, one starts to develop certain pattern recognition abilities which will help you in future when similar problems arise.

[0]:http://www.bigocheatsheet.com/img/big-o-cheat-sheet-poster.png
[Code]:https://github.com/javanibble/java-algorithms/blob/master/sort/src/main/java/com/javanibble/algorithm/sort/BubbleSort.java