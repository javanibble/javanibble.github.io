---
layout: post
title: Merge Sort Algorithm in Java
author: andre
categories: [ sort-algorithm ]
tags: [algorithm]
image: /assets/images/feature-images/feature-image-algorithms.png
description: This article gives provides an overview on Merge Sort together with an implementation in Java.
comments: true
---

- Table of Contents
{:toc .large-only}

Merge Sort is a divide and conquer algorithm as the algorithm splits the original array into smaller logical sections. The algorithm can be implemented making use of loops or recursions. The two distinct phases are a splitting phase and secondly a merging phase.

*Splitting Phase*: Divide the array into two unsorted arrays. Each of the split arrays are continuously split into smaller arrays until only multiple single element arrays exist. Single element arrays are sorted as they only have one element in them.

*Merging Phase*: Each of the single element arrays are now merged back into a larger array. During the merge phase the two arrays are merged so that the elements are sorted within the new larger sorted array. This process is repeated until a single sorted array is left. This is not an in-place algorithm as temporary arrays are used.

## Algorithm Classification
The following table contains information about the analysis of the Merge Sort algorithm. It defines the worst, average and best cases in terms of time complexity and also the worst case in space complexity.

| Attribute | Value | 
|-----------|-------|
| Class | Sorting Algorithm | 
| Classification | Internal, Not In-place, Stable Algorithm  | 
| Data Structure | Array | 
| Time Complexity: Best | Ω(n log(n)) | 
| Time Complexity: Average | Θ(n log(n)) | 
| Time Complexity: Worst | O(n log(n)) | 
| Space Complexity: Worst | O(n) | 
{:.stretch-table}

Algorithm Classification: Merge Sort
{:.figcaption}

Please use the following [link][0] for an explanation on Big-O notation and what is good, fair and bad.

## Merge Sort In Java
The MergeSort class implements the Merge Sort algorithm for sorting an array of integers.

```java
public final class MergeSort {

    public void sort(int[] collection) {
        if (collection != null) {
            mergeSort(collection, 0 , collection.length);
        } else {
            throw new IllegalArgumentException("Input paramenter for array to sort is null.");
        }
    }
    
    public  void mergeSort(int[] collection, int minIndex, int maxIndex) {
        if (maxIndex - minIndex < 2) {
            return;
        }
        
        int centre = (minIndex + maxIndex) / 2;
        mergeSort(collection, minIndex, centre);
        mergeSort(collection, centre, maxIndex);
        mergeBack(collection, minIndex, centre, maxIndex);       
    }
    
    public void mergeBack(int[] collection, int minIndex, int centre, int maxIndex) {
        if (collection[centre - 1] <= collection[centre]) {
            return;
        }
        int tempMinIndex = minIndex;
        int tempCentre = centre;
        
        int tempIndex = 0;
        int[] tempArray = new int[maxIndex - minIndex];
        
        while ((tempMinIndex < centre) && (tempCentre < maxIndex)) {
            if(collection[tempMinIndex] <= collection[tempCentre]) {
                tempArray[tempIndex++] = collection[tempMinIndex++];    
            } else {
                tempArray[tempIndex++] = collection[tempCentre++];
            }
        }

        System.arraycopy(collection, tempMinIndex, collection, minIndex + tempIndex, centre - tempMinIndex);
        System.arraycopy(tempArray, 0, collection, minIndex, tempIndex);
    }   
}
```

## Sample Code (GitHub)
The code example can be downloaded from Github from the following [link][Code].

## Finally
The Merge Sort algorithm forms part of a larger group of sorting algorithms. Learning through experience is the reason I created this post about the implementation of the Merge Sort algorithm in Java. I have learned a lot about how others have solved the Merge Sort algorithm in other languages including different implementations in Java.

Learning how to solve difference problems and algorithms with certain techniques, one starts to develop certain pattern recognition abilities which will help you in future when similar problems arise.

[0]:http://www.bigocheatsheet.com/img/big-o-cheat-sheet-poster.png
[Code]:https://github.com/javanibble/java-algorithms/blob/master/sort/src/main/java/com/javanibble/algorithm/sort/MergeSort.java