




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
![Screenshot (39)](https://user-images.githubusercontent.com/130017333/233815739-c535bbba-d07a-4ee0-b14b-0c349b24b808.png)


Let's look back at the method body provided earlier:
```
static int sumEvenIndices(int[] nums) {
    int sum = 0;
    for(int i = 0; i < nums.length; i += 2) {
      sum += nums[i + 1];
    }
    return sum;
  }
```
Observe the for-loop header. It appears from this that the variable i will always be an even number; it starts at 0 and increases by 2 after each iteraion, so it can only be even. Now take a look at the for-loop body:

``
sum += nums[i + 1];
``

If i is always even, then i+1 is always odd. What this means is that nums[i+1] is NOT accessing the even indices; it's actually accessing only the ODD indices. This is a major bug in the program because the program is not evenn adding the indices it is supposed to be, so it is bound to produce an incorrect output every time. The first way to fix this bug is by replacing i+1 with i; this will ensure that the nums array is accessing only its even indices rather than only its odd indices. Here's the updated method body:
``

static int sumEvenIndices(int[] nums) {
    int sum = 0;
    for(int i = 0; i < nums.length; i += 2) {
      sum += nums[i];
    }
    return sum;
  }
``

Let's test the program again with this bug eliminated. 
![Screenshot (41)](https://user-images.githubusercontent.com/130017333/233815654-fa83a172-a4e8-46a3-b077-799b8790b651.png)
And sure enough, all of the tests pass with JUnit! I even included one more test just to be safe.


