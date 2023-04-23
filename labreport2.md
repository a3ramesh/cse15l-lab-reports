




Part 2: Debugging
In this part, we will take a look at a buggy program and try to debug. The first step to fixing a buggy program is to first test if it is even buggy. We will look at a method that takes in an array and that is supposed to return sum of the elements in the even indices of the array. Below is the method body for the method, called sumEvenIndices:
![Screenshot (35)](https://user-images.githubusercontent.com/130017333/233813978-7f1ef095-d88d-4ab6-b3e6-df0c95e2de89.png)

This method does produce the correct output for a particular type of input value. And that is an empty array.

```
public void testSumEvensLength4() {
    int[] input1 = {};
    assertEquals(EvensExample.sumEvenIndices(input1), 0);
  }
```


