---
layout: post
title: Shell Sort Algorithm in Java
author: andre
categories: [ sort-algorithm ]
tags: [algorithm]
image: /assets/images/feature-images/feature-image-algorithms.png
description: This article gives provides an overview on Shell Sort together with an implementation in Java.
comments: true
---

- Table of Contents
{:toc .large-only}

Shell Sort is an in-place comparison sort algorithm. Shell Sort is a generalization of insertion sort that allows the exchange of items that are far apart. The algorithm perform  preliminary work by sorting pairs of elements far apart from each other. The algorithm progressively reduce the gap between elements to be compared as the goal is to reduce the amount of shifting of elements across the array. As the gap is reduced to 1, the algorithm becomes the same as the insertion sort algorithm.

## Algorithm Classification
The following table contains information about the analysis of the Shell Sort Sort algorithm. It defines the worst, average and best cases in terms of time complexity and also the worst case in space complexity.

| Attribute | Value | 
|-----------|-------|
| Class | Sorting Algorithm | 
| Classification | Internal, In-place, Unstable Algorithm  | 
| Data Structure | Array | 
| Time Complexity: Best | Ω(n log(n)) | 
| Time Complexity: Average | Θ(n log<sup>2</sup>n) | 
| Time Complexity: Worst | O(n<sup>2</sup>) | 
| Space Complexity: Worst | O(1) | 
{:.stretch-table}

Algorithm Classification: Shell Sort
{:.figcaption}

Please use the following [link][0] for an explanation on Big-O notation and what is good, fair and bad.

## Shell Sort In Java
The ShellSort class implements the Shell Sort algorithm for sorting an array of integers.

```java
public final class ShellSort {

    public void sort(int[] collection) {
        if (collection != null) {
            shellSort(collection);
        } else {
            throw new IllegalArgumentException("Input paramenter for array to sort is null.");
        }
    }
        
    private void shellSort(int[] collection) {
        int arrayLength = collection.length;
        
        for (int gap = arrayLength / 2; gap > 0; gap /= 2) {
            for (int i = gap; i < arrayLength; i++) {
                int newElement = collection[i];
                
                int j = i;
                while (j >= gap && collection[j - gap] > newElement) {
                    collection[j] = collection[j - gap];
                    j -= gap;
                }
                collection[j] = newElement;
            }
        }
    } 
}
```

## Sample Code (GitHub)
The code example can be downloaded from Github from the following [link][Code].

## Finally
The Shell Sort algorithm forms part of a larger group of sorting algorithms. Learning through experience is the reason I created this post about the implementation of the Shell Sort algorithm in Java. I have learned a lot about how others have solved the Shell Sort algorithm in other languages including different implementations in Java.

Learning how to solve difference problems and algorithms with certain techniques, one starts to develop certain pattern recognition abilities which will help you in future when similar problems arise.

[0]:http://www.bigocheatsheet.com/img/big-o-cheat-sheet-poster.png
[Code]:https://github.com/javanibble/java-algorithms/blob/master/sort/src/main/java/com/javanibble/algorithm/sort/ShellSort.java
