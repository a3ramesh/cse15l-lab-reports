My name is Advait Ramesh, and this is a lab report for Week 10 of Spring 2023 CSE 15L with Joe Politz. The goals of this lab report are to 1) showcase a program with a bug and thoroughly explain the steps to debug the program, and 2) reflect on something interesting I learned in the second half of CSE 15L.

Goal 1: Showcasing a Buggy Program

To do this, we're going to simulate a post on EdStem in which a student posts a picture of a symptom of their buggy program and takes a guess at the bug in their program. Then a TA will suggest a step to finding the bug in the program. Then the student will try the suggestion, after which it is clear what the bug is. Here it is:

Student: The arrayInsertFirstMethod() isn't working for me. There is a main method in the Sample.java class that takes in a set of arguments; all of the arguments except the last one are supposed to make up an array, and the final argument is supposed to be the value that is inserted at the beginning of the array, pushing all of the other elements forward by one index. This new array is supposed to be printed out as the output. But this is not what happens. Instead, the last few elements of the array are repeated for some reason.
Here is my Sample.java file:
![Screenshot (73)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/e8d7020a-4276-4f09-b07d-99156fe2d431)
Here is the sample.sh file:
![image](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/4dd045e3-8a5a-43bc-87e1-3695096c5144)
And here is my command line:
![Screenshot (75)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/adc7a65c-35ed-41e5-9e69-71b92983b43a)
I don't know why it says my insert method isn't working correctly. My failure inducing input was of course typing 'bash sample.sh' at the command line, but I don't know what other input to try at the command line. I'm pretty sure all of my code in the Sample.java file is written correctly, so I feel that something is wrong with the sample.sh file. I'm not entirely sure how bash works, but I think the error might have something to do with "result = `java Sample 1 2 3 4 9`". I think there's a problem with setting a variable equal to the entire output of running a program. However, I'm not sure how to fix this .sh file so that it more accurately assesses my code. Could someone help me please?

TA: How sure are you that the code in your Sample.java file is written correctly? I suggest that you try some other inputs to get a good idea of what the error is. Also, I assure you that there is nothing wrong with doing "result = `java Sample 1 2 3 4 9`" and a bash script is perfectly capable of setting a variable equal to the output of running a program. So that this is clear, I want you to not run the bash script and instead just run the commands directly with the command line. Notice where it says in the bash script
```
javac Sample.java
result=`java Sample 1 2 3 4 9`
```
Try running these commands directly in the terminal without running the bash script. The same result should appear. Then after this, I want you to use these same commands to try a different input, and then observe the output for that. 

Student: Okay, I did what you said. And yes, the result of running that input with just the terminal is the same as what the bash script said:
![Screenshot (77)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/1cb6f379-bdac-40a6-bbfc-0803b46c8e9f)
I also tried this with a different input, and the error was similar to the one before.
![Screenshot (78)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/f28c4ca7-80f0-443a-9789-75f90b7619c5)
And to check that this was the same output that the bash script would give me, I changed the code on the bash script as well. And it gave me the same result like you said.
![Screenshot (79)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/f3b0371d-4477-46b2-8bf6-88dcc9e9ab03)
So I now see that there's nothing wrong with the bash script; it simply mirrors what you type directly at the command line. So then the problem must be in my Sample.java file. But I don't know how to fix it.

TA: Okay. So now you want to find out the cause of the symptom. Go to the Sample.java file. Right now, when you run the program you can only see the input array and the output array, but you can't see anything in between. What is something you can add to your code to observe how each element in the output array is being set gradually, rather than just the end result? Try to see if you can find a way to view the value of each element in the array before and after EACH iteration of the for loop. Tell me what you can take away from that.

Student: Okay, I did what you said, and the way I decided to do it is print out the value at each index with System.out.println() both before and after each iteration of the for loop (as well as once before the for loop begins). Here was the result using the original input 1 2 3 4 9:
![Screenshot (80)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/9c624c35-b760-4ccb-9e6a-bb541aa88251)
What I take away from this is that, before each iteration is simply each of the command line arguments, but after each iteration is 1. Every time. arr[1] is 2 at first then becomes 1, arr[2] is 3 at first and then becomes 1, arr[3] is 4 at first and then becomes 1, etc. Each element is actively being set to 1. And the operation that's doing that must be ```arr[i]=arr[i-1]```, which means that arr[i-1] is always equal to 1. But I'm not sure why though.

TA: You're on the right track. In your code, arr[i-1] is always equal to 1. What is the starting value of arr[i-1]? 

Student: Well, the starting value of arr[i-1] is 1 when i=1. This means arr[i] is arr[1], which is also set to 1. Then when i=2, arr[i-1] is arr[1], and the value of this is just 1 from the previous iteration, so then arr[i] is arr[2], which is also set to 1. Ohhhhhhh, I see it now! The initial value of arr[i-1] is just 1, and in each iteration, arr[i] is being set to the same value as arr[i-1]. But the key is that arr[i] in this iteration becomes arr[i-1] in the next iteration, and then arr[i] in the next iteration is set to arr[i-1], which is 1. So every element in the array is going to eventually be set equal to 1! It makes sense now. 

TA: Yes, that's absolutely correct! But how do you fix this so that this doesn't happen?

Student: Well, one thing I could try is instead of iterating through the array from the beginning forwards, I could iterate from the end backwards.
And when I did this, the method passed with the bash script!
![Screenshot (82)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/42191c39-f0fa-49c9-941a-4728d53e26eb)
![Screenshot (81)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/3d0e1ab2-d112-45b0-8b26-3f8d138d39fa)

_______________________________________________________________________________________________________________________________________________________________________

This scenario is a good example of how to know which file your code is problematic, and how to use some modification tactics to your code to pinpoint the error. 

Some key points of this particular scenario:
1.) I used a java file called Sample.java and a shell file called sample.sh. Both of these files were in the same directory.
2.) The shell file contained some very simple bash code with essentially one test case to check if a particular method functioned as it should have. The java file contains the code for this method, which is a method to insert an element at the beginning of an array, shifting the other elements over by one space as necessary. The original code for this method had a bug in it that ensured that all of the elements apart from the first one are the same. In addition to this method was a main method that took command line arguments and converted all of them except for the last one into an array, and passed this array as an argument for the insert method; the other argument for the insert method, the value to be inserted, is the final command line argument for the main method. The output of the main method is simply the modified array with the insertion.
3.) Running ```bash sample.sh``` was enough to trigger the bug. This triggered the bug in that it displayed a message saying that the insert method did not work as it should have. This was because inside of the sample.sh file was an actual instance of running the main method, with ```javac Sample.java``` and ```java Sample 1 2 3 4 9```. The latter triggered the bug in that it did not output what it was supposed to. After deducing that the bug was in the code for the insert method itself, I added some System.out.println methods to print the contents of the array as it was being iterated through. I then ran the main method with the command line again using ```java Sample 1 2 3 4 9```, after which it was more clear what was going on: namely that before each iteration the element was one of the command line arguments, but after each iteration the element was set equal to 1.
4.) Instead of iterating forward through the array to shift the elements one forward after insertion, we iterated backward through the array. This fixed the bug, and when the command ```bash sample.sh``` was run, a message that insert method worked as it should have was displayed.

Goal 2: Reflection

I learned so many cool things in CSE 15L! One cool thing I learned was how to write a bash script. I learned important aspects of the syntax of bash, including for loops and if statements (enhanced for loops, do and done; if, then, else, and fi), and the idea that variables can be initialized to be the output of certain commands, which I find to be the coolest part. I also greatly enjoyed the content of Lab Report 3, in which I took the wc command and explored variations on it; it was very fun to experiment with these variations on the wc command and test them out on actual files, as well as analyze how these commands made coding more efficient. It was also a lot of fun to learn about vim, a powerful text editor with some odd yet fascinating choices for keystrokes to initiate certain commands (such as h, j, k,and l for left, down, up, and right, and wq! to save and quit, and  /<query> to search for words, etc.). All in all, CSE 15L has been an interesting and insightful class that is different from any computer science course I've taken thus far, and I look forward to the ways in which I will take the kwoledge from thsi class and use them in my coding assignments for future endeavors. Thank you, and this concludes my lab report.





