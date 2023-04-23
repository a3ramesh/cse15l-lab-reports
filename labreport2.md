




Part 2: Debugging
In this part, we will take a look at a buggy program and try to debug. The first step to fixing a buggy program is to first test if it is even buggy. We will look at a method that takes in an array and that is supposed to return sum of the elements in the even indices of the array. Below is the method body for the method, called sumEvenIndices:
```
static int sumEvenIndices(int[] nums) {
    int sum = 0;
    for(int i = 0; i < nums.length; i += 2) {
      sum += nums[i + 1];
    }
    return sum;
  }
```

This method does produce the correct output for a particular type of input value. And that is an empty array. In this case, it should simply return 0.

```
public void testSumEvensLength4() {
    int[] input1 = {};
    assertEquals(EvensExample.sumEvenIndices(input1), 0);
  }
```
I tested this input with JUnit, and the test passed.

However, every other input appears to be a failure-inducing input. When this method takes in an array with one element, it should simply return that element. Here was the test:
```
public void testSumEvenLength5() {
    int[] input1 = { 12};
    assertEquals(EvensExample.sumEvenIndices(input1), 12);
  }
```
However, when I ran this through JUnit, it led to an IndexOutOfBounds exception. This is called a symptom: when a program outputs what it is not supposed to.
![Screenshot (38)](https://user-images.githubusercontent.com/130017333/233814906-a8171d3b-08b9-40b0-8a12-0dcb9115e629.png)

For another input, I tested an array with four elements.
```
public void testSumEvenLength6() {
    int[] input1 = { 12, 13, 7, 8};
    assertEquals(EvensExample.sumEvenIndices(input1), 19);
  }
```
When I ran this through JUnit, it did not lead to an exception. It simply returned an integer that it was not supposed to return. So this is a different symptom.
![Uploading Screenshot (39).png…]()



