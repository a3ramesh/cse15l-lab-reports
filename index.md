My name is Advait Ramesh, and this is a lab report for Week 2 of Spring 2023 CSE 15L with Joe Politz. The goal of this report is to describe the steps I took in order to log into a course-specific account on ieng6.

Step 1: Installing Visual Studios Code

I did not actually need to install VS Code this time because I had already installed it for CSE 8B. I did numerous PAs on it in that class. Here is a picture of my Visual Studios Code:
![Screenshot (8)](https://user-images.githubusercontent.com/130017333/230753068-7fe3e8c9-1d6c-41b1-8e97-77aacc439653.png)
This is an image of a programming assignment I did last quarter in CSE 8B using Visual Studios. This shows that I had Visual Studios installed before entering CSE 12.

Step 2: Remotely Connecting

In order to connect my terminal to a computer in the CSE basement, the first thing I did was install Git for Windows, since my computer is on Windows:
![Screenshot (9)](https://user-images.githubusercontent.com/130017333/230795102-eeba056a-e7c6-4daa-8e1b-f6f59f1e268d.png)
After I did this, my updated new terminal looked like this:
![Screenshot (10)](https://user-images.githubusercontent.com/130017333/230795186-8015891d-5106-44ff-a0a0-746aaee5c05f.png)
Before typing anything in this terminal, I first found out what my CSE 15L course-specific username is. To do this, I clicked on this url https://sdacs.ucsd.edu/~icc/index.php and wound up here:
![Screenshot (23)](https://user-images.githubusercontent.com/130017333/231033714-ad2a50bc-48aa-472e-8389-a06db80b1c1f.png)
When I was here, I clicked the 'submit' button and wound up on this page, where I found out my CSE 15L username:
![Screenshot (24)](https://user-images.githubusercontent.com/130017333/231034188-d3bf031e-5b45-4f40-b57f-622a4c8a3e10.png)
On this page, notice where it says 'Global Password Change Tool.' I clicked on this and reset my password. I was then ready to type into the terminal.
In this new terminal, I typed the ssh command (which is used to connect to remote servers), followed by my course-specific username cs15lsp23sf plus @ieng6.ucsd.edu:
![Screenshot (19)](https://user-images.githubusercontent.com/130017333/231026383-6fb8cae0-c868-4af2-b607-de420bbcbcf5.png)
It now asks for my password. After I type it in, the following appears:
![Screenshot (20)](https://user-images.githubusercontent.com/130017333/231026892-0953f961-a00b-49af-89d3-b4bc06bee791.png)
With this, my terminal is now connected to a computer in the CSE basement. 

Step 3: Trying Some Commands

I tried multiple commands with this terminal. I tried the the pwd command (stands for "print working directory" and prints the directory that my terminal is currently in) and the cat command (stands for "concatenate" and prints the contents of the file(s) given by the specified paths; in this case the "hello.txt" file):
![Screenshot (25)](https://user-images.githubusercontent.com/130017333/231041613-52a74507-8008-4a64-ac59-8d27c04c9ebc.png)
I also tried the cd command (this changes the directory that my terminal is currently in). After doing this, I used the pwd command again to check that the directory my terminal is in has changed:








