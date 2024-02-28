# CSE 15L Lab Report 3

Bugs and Commands

Flora Kang

## Part 1
### Failure-inducing input:

`ArrayExamples.java`

```java
// Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```

Additional Tests Written in `ArrayTests.java`

```java
@Test 
  public void testReverseInPlaceMoreElem() {
    int[] input1 = { 1, 2, 3, 4 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 4, 3, 2, 1 }, input1);
  }

  @Test 
  public void testReverseInPlaceEmptyArray() {
    int[] input1 = {};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{}, input1);
  }

  @Test
  public void testReversedMoreElem() {
    int[] input1 = { 1, 2, 3, 4 };
    assertArrayEquals(new int[]{ 4, 3, 2, 1 }, ArrayExamples.reversed(input1));
  }

  @Test
  public void testReversedOneElem() {
    int[] input1 = { 1 };
    assertArrayEquals(new int[]{ 1 }, ArrayExamples.reversed(input1));
  }
```

**Symptom (Terminal):**

```bash
There were 3 failures:
1) testReversedOneElem(ArrayTests)
arrays first differed at element [0]; expected:<1> but was:<0>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReversedOneElem(ArrayTests.java:46)
        ... 30 trimmed
Caused by: java.lang.AssertionError: expected:<1> but was:<0>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 36 more
2) testReverseInPlaceMoreElem(ArrayTests)
arrays first differed at element [2]; expected:<2> but was:<3>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReverseInPlaceMoreElem(ArrayTests.java:25)
        ... 30 trimmed
Caused by: java.lang.AssertionError: expected:<2> but was:<3>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 36 more
3) testReversedMoreElem(ArrayTests)
arrays first differed at element [0]; expected:<4> but was:<0>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReversedMoreElem(ArrayTests.java:40)
        ... 30 trimmed
Caused by: java.lang.AssertionError: expected:<4> but was:<0>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 36 more

FAILURES!!!
Tests run: 6,  Failures: 3

```

**Explanation:**

Purpose: The method reverseInPlace() should change the given array to be in reversed order

Explanation of bug: The method iterates through the input array using a for loop, starting at i = 0, increasing by 1 until i is not less than the length of the array. However, within the loop, the program assigns the element at index i the value of the element at index (arr.length - i - 1), causing a bug because once the loop has replaced half the array, the second half of the input array has been overwritten and the original elements lost.

**Method: reversed()**

Purpose: The method reversed() should return a new array with the elements of the given array in reversed order.

Explanation of bug: The method creates a new array `newArray` with the same length as the input array and iterates through using a loop like in reverseInPlace(), but incorrectly assigns the values of `newArray`, which is empty, to the input array and returns the emptied input array instead of assigning the elements of the input array to `newArray` and returning `newArray` with the assigned values.

### Non failure-inducing Input:

`ArrayExamples.java`

```java
// Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = temp;
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i++) {
        newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```

**Tests Written in `[ArrayTests.java](http://ArrayTests.java)` remained the same**

**Symptom (Terminal):**

```java
flora2.kang@MacBook-Air-5 lab3 % javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java

flora2.kang@MacBook-Air-5 lab3 % java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ArrayTests

JUnit version 4.13.2
......
Time: 0.004

OK (6 tests)

flora2.kang@MacBook-Air-5 lab3 % 
```

(all tests passed after these changes)

**Explanation:**

**Method: reverseInPlace()**

To fix the bug, I created a variable temp, which would hold onto the value of the original element at index `i` during each iteration of the loop while the element at `i` would be overwritten by the value at index (arr.length - i - 1). Then, I reassigned temp to index (arr.length - i - 1), basically flipping the two elements in one iteration, which is why we only iterated through half of the array.

**Method: reversed()**

To fix the bug, I had to edit the body of the for loop so that instead of assigning the values of the new array to the input array, we add the values of the input array to the new array.

`arr[i] = newArray[arr.length - i - 1]` to `newArray[i] = arr[arr.length - i - 1]`

Then, I made sure to return `newArray` , not the input array.

## Part 2 - Researching Commands

Command: `grep`

4 Command-line Options:

1. grep -r “pettern” <directory> : recursively searches all files under current directory
    1. grep -r 1468
    2. grep -r Introduction (screenshot cropped for length)
    
    ![Screen Shot 2024-02-27 at 10.32.47 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2d8cd9a-00a8-478f-94bd-3418ffefafff/849bb07b-99eb-4292-83d0-13cecdfac2ed/Screen_Shot_2024-02-27_at_10.32.47_PM.png)
    
2. grep -c “pattern” <file>: display count of lines that match te pattern
    1. grep -c For technical/911report/chapter-1.txt
    2. grep -c for technical/911report/chapter-1.txt
        
        ![Screen Shot 2024-02-27 at 10.41.37 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2d8cd9a-00a8-478f-94bd-3418ffefafff/4d074889-13c6-4bd7-8bec-b041b0afc1d6/Screen_Shot_2024-02-27_at_10.41.37_PM.png)
        
3. grep -i “pattern” <file>: find the pattern within the file ignoring cases
    1. grep -i 'WE HAVE SOME PLANES' 911report/chapter-1.txt
    2. grep -i 'we have some planes' 911report/chapter-1.txt (to check cases)
        
        ![Screen Shot 2024-02-27 at 10.51.19 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2d8cd9a-00a8-478f-94bd-3418ffefafff/f77ef78f-dc3a-4b4e-aff2-2dbe2a46e511/Screen_Shot_2024-02-27_at_10.51.19_PM.png)
        
        ![Screen Shot 2024-02-27 at 10.51.37 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2d8cd9a-00a8-478f-94bd-3418ffefafff/547e7d9c-7739-4361-b5f6-d268b18624cd/Screen_Shot_2024-02-27_at_10.51.37_PM.png)
        
4. grep -n : display matched lines and line numbers
    1. grep -n "WE HAVE SOME PLANES" technical/911report/chapter-1.txt
    2. grep -n "we have some planes" technical/911report/chapter-1.txt
    
    ![Screen Shot 2024-02-27 at 10.45.54 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/b2d8cd9a-00a8-478f-94bd-3418ffefafff/56b27f3a-92d1-4718-979f-58ecea7e9046/Screen_Shot_2024-02-27_at_10.45.54_PM.png)
    

Citations:

https://linuxcommand.org/lc3_man_pages/grep1.html

https://www.geeksforgeeks.org/grep-command-in-unixlinux/
