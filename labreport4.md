My name is Advait Ramesh, and this is a lab report for Week 8 of Spring 2023 CSE 15L with Joe Politz. The goal of this lab report is to complete a set of steps with the terminal and record the amount of keystrokes each step takes me.

Step 4: Log into ieng6

![Screenshot (54)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/433fb6c7-bdc1-4c29-85be-0c3384e7221d)
For this step, I went to the terminal and typed:
```ssh cs15lsp23sf@ieng6.ucsd.edu <enter> <password> <enter>``` and that's all
  
Step 5:  Clone your fork of the repository from your Github account

In order to clone the directory, I simply type ```git clone https://github.com/ucsd-cse15l-s23/lab7 <enter>```. However, when I do this, it says the following:
![Screenshot (55)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/23248b2b-c297-48d2-866e-ab664ef016e1)
What it says is that the lab7 directory already exists in my downloaded files. For the purposes of this assignment, I am going to remove this directory so that I can start over again. The way to do this is with the ```rm -rf``` command. After typing ```rm -rf lab7 <enter>```, I will successfully remove the lab7 directory.
![image](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/15bb5033-7223-4788-ad8c-d365db566e29)
As you can see, after I typed ```rm -rf lab7 <enter>```and typed ``ls <enter>`` to view the subdirectories in the current working directory, lab7 is no longer there. So the directory was successfully removed. 
Now I can type ```git clone https://github.com/ucsd-cse15l-s23/lab7``` again to clone the repository.
![Screenshot (56)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/581bb64f-7692-4cb2-a082-24b375f07800)
Note that I "typed" the git clone command again by using the up arrow a couple of times, since I had just recently typed it. And when I did so, the operation was successful. 
  
Step 6: Run the tests, demonstrating that they fail

First I change directories to the lab7 directory by typing ```cd lab7``` and then enter:
![Screenshot (57)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/e1dbd6e1-14f7-4f14-a757-1c8b75ae31bc)
Now when I use the ls command, I can see that the test.sh file is inside of the lab7 directory. This file is what I will use to run my tests. The command to run the tests is ```bash test.sh```. When I run this, it should show that there is a failure:
![Screenshot (58)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/d8982d1e-90fc-46e5-ab17-1c208c8eb7f2)
And indeed, it shows that one of the tests has failed.

Step 7: Edit the code file to fix the failing test

  To fix the test that failed, I need to enter the file that contains the code for the test. This file is the ListExamples.java file, shown in the ls command below:
![Screenshot (59)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/ccfe84f7-fa15-4d51-8c0c-bcc5babc0cca)
A good way to fix the code in this file is by going into vim mode. To do this, I simply type the command ```vim ListExamples.java <enter>```, and then the file will be in vim mode:
![Screenshot (60)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/3128805a-16e4-497a-93a1-34785c77b684)
This is the result after typing ```vim ListExamples.java <enter>```. 
The error in this code is that in the last while loop, index1 is written when index2 should be written:
![Screenshot (61)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/48eb3da9-57f8-49dd-b97e-3717c2a195f0)
There's a way I can get to this line without using the cursor. If I type ```/index <enter>```, this only focuses on the lines that have the word "index" in them. Then, I can use the ```n``` key to jump to each line with the word "index" in it. 
![Screenshot (62)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/9b788cdf-42a9-4f44-a9d7-2ced5c814ee0)
Notice that when I typed "/index" it highlighted the first appearance of the word "index" in the top line. Now I can press ```n``` about 16 times to navigate to the bottom line with the word "index", which is where the error is:
![Screenshot (63)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/687bb386-3661-4e5a-9cb7-c3c04c335f21)
Now I can scroll to the right until my cursor is on the number 1:
![Screenshot (64)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/69188af3-efd6-4805-bfcf-f5c6066b882f)
From this point, what I can do is press ```r``` and then 2. This will have successfully replaced the 1 with a 2 to make index2.
![Screenshot (65)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/70eade64-50c3-4817-8ac4-631520b8015c)
Now to run the tests again, I can save my progress and exit vim mode by pressing ```:wq!<enter>```:
![Screenshot (66)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/ae445326-a81a-4684-ac38-e6c6ff9901f2)
![Screenshot (67)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/3f57d98f-09ae-4bcd-b7c1-35da7e7f43a5)
Now I am out of vim mode.
  
Step 8: Run the tests, demonstrating that they now succeed
  
Now we should type ```bash test.sh <enter>``` once again and run it.
![Screenshot (69)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/4f54c0b9-e570-4b13-943e-7a70acb55e98)
As demonstrated, my tests have now passed.

Step 9: Commit and push the resulting change to your Github account
  
  
The way to do this is simply to type ```git push``` and then ```git commit``` successively




  










 
  
  
  
