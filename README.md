## Implementation of Bubble Sort in Javascript

## Overview

This document details the step-by-step internal mechanics of the `bubbleSort` function. The algorithm accepts an unsorted array and returns it fully sorted by bubbling the highest values to the top during each pass-through.

## Algorithm Walkthrough

### 1. Initialization

Before beginning the sort, the function establishes two key variables to manage the state of the array.

- Tracking the Unsorted Range: The variable `unsortedUntilIndex` tracks the rightmost index of the array that has not yet been sorted. Initially, the entire array is unsorted, so it points to the final index.

```
let unsortedUntilIndex = array.length - 1;
```

Tracking Sort Status: The `sorted` variable acts as a flag. It is initialized to false to trigger the main execution loop.

```
let sorted = false;
```

### 2. The Main Execution Loop

The algorithm uses a `while` loop that continues to run as long as the array is not fully sorted (`!sorted`). Each iteration of this loop represents one full "pass-through" of the array.

```
while (!sorted) {
    sorted = true;
```

- Optimistic Assumption: At the start of each pass, we preliminarily set sorted to true. We assume the array is sorted until we encounter a swap. If a pass completes without swaps, sorted remains true, and the loop terminates.

### 3. Iteration and Swapping

Inside the main loop, a `for` loop iterates through the array using pointer `i`. It runs from the beginning up to the `unsortedUntilIndex`.

```
for (let i = 0; i < unsortedUntilIndex; i += 1) {
```

Within this loop, adjacent pairs are compared:

- Comparison: We check if `array[i]` is greater than `array[i + 1]`.

- The Swap: If they are out of order, we swap their positions.

- Flag Update: Because a swap occurred, we set `sorted` to `false` to ensure another pass-through occurs.

```
  if (array[i] > array[i + 1]) {
      [array[i], array[i + 1]] = [array[i + 1], array[i]];
      sorted = false;
  }
}
```

### 4. Optimization and Completion

At the end of each pass-through, the highest value in the unsorted range has "bubbled" up to its correct position at the right.

- Narrowing the Scope: We decrement `unsortedUntilIndex` by 1. We no longer need to inspect this index in future passes.

```
unsortedUntilIndex -= 1;
```

Return: Once the `while` loop finishes (meaning a pass occurred with zero swaps), the array is fully sorted and returned.

```
return array;
```