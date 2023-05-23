My name is Advait Ramesh, and this is a lab report for Week 8 of Spring 2023 CSE 15L with Joe Politz. The goal of this lab report is to complete set of steps with the terminal and record the amount of keystrokes each step takes me.

Step 1: Log into ieng6
![Screenshot (54)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/433fb6c7-bdc1-4c29-85be-0c3384e7221d)
For this step, I went to the terminal and typed:
ssh cs15lsp23sf@ieng6.ucsd.edu <enter> <password> and that's all
  
Step 2: Cloning a fork of the repository from my Github account
In order to clone the directory, I simply type ```git clone https://github.com/ucsd-cse15l-s23/lab7``` However, when I do this, it says the following:
![Screenshot (55)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/23248b2b-c297-48d2-866e-ab664ef016e1)
What it says is that the lab7 file already exists in my downloaded files. For the purposes of this assignment, I am going to remove this file so that I can start over again. The way to do this is with the ```rm -rf command```. After executing this command, I should be able to successfully clone a fork of this repository:
![Screenshot (56)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/581bb64f-7692-4cb2-a082-24b375f07800)
Note that I "typed" the git clone command again by using the up arrow a couple of times, since I had just recently typed it. And when I did so, the operation was successful. 
  
Step 3: Running the tests and demonstrating that they fail
First I change directories to the lab7 directory as follows:
![Screenshot (57)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/e1dbd6e1-14f7-4f14-a757-1c8b75ae31bc)
Now when I use the ls command, I can see the test.sh folder. This is what I will use to run my tests. The command to run the tests is ```bash test.sh```. When I run this, it should show that there is a failure:
![Screenshot (58)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/d8982d1e-90fc-46e5-ab17-1c208c8eb7f2)
And indeed, it shows that one of the tests has failed.

Step 4: Editing the code file to fix the failing test
To fix the test that failed, I need to enter the file that contains the code for the test. This file is the ListExamples.java file, shown in the ls command below:
![Screenshot (59)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/ccfe84f7-fa15-4d51-8c0c-bcc5babc0cca)
A good way to fix the code in this file is by going into vim mode. To do this, I simply type the command ```vim ListExamples.java```, and then the file will be in vim mode:
![Screenshot (60)](https://github.com/a3ramesh/cse15l-lab-reports/assets/130017333/3128805a-16e4-497a-93a1-34785c77b684)
This is the result after typing ```vim ListExamples.java```. 









 
  
  
  
