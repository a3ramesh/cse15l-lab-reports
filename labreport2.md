My name is Advait Ramesh, and this is a lab report for Week 4 of Spring 2023 CSE 15L with Joe Politz. This lab report has three parts: the first part is to create a working web server and describe its components; the second part is to showcase a buggy program and describe the steps to debugging it; and the last part is to simply list some things I've learned in the past two labs.

Part 1: Creating a Working Web Server
The way this webserver works is that the user is supposed to type in an input string after the URL, and this string should be displayed on the page. Each time the user types in a new input string after the URL, that string should be displayed underneath the already displayed strings. Here is the code for this program:

```
class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String text = "";

    public String handleRequest(URI url) {
        if(url.getPath().equals("/add-message"))
        {
            String query = url.getQuery();
            String input_text = query.substring(query.indexOf('=')+1);
            text = text + "\n" + input_text;
            System.out.println(text);
        }

        return text;
    }
}

public class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing query!");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

And this program works when run on the web:
![Screenshot (42)](https://user-images.githubusercontent.com/130017333/233879204-13ded621-fd59-48c8-aec5-cb673177d3cd.png)
Notice I typed "apple" at the end of the URL after "s=" and the word "apple" was displayed on the page. I tried it again, but typed "banana" after "s=":
![Screenshot (43)](https://user-images.githubusercontent.com/130017333/233879356-1d1767db-9740-44b0-9c4f-6a99f3e8625e.png)
Notice here that both the words "apple" and "banana" are displayed. 

Here is how the code works. Each time I type something into the URL and press enter, the main method in the StringServer class runs. If there *is* a URL in the bar, the method will go past the first if-statement and then go to where it says ```int port = Integer.parseInt(args[0])```. What this does is find the first integer in the URL, which will be the four-digit port number, convert that to an int, and then return that. The variable ```port``` is set equal to that ```int```. After this, what happens is the static method ```start``` within the ```Server``` class is called, with the first argument being the port number that was just found, and the second argument being a new Handler object. What the start method does essentially is start the activity of the server indicated by the given port number, and then link the new Handler object, which is of type URLHandler, to the information in this same server. This is how the methods within the Handler class, which we will get to, can access the information from this server. Here is the header and body of the ```start``` method within the ```Server``` class. 
```
public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
```
We don't have to know all the details, but this is mainly to get an idea of the purpose of this method.
Once the ```start``` method is called from the ```StringServer``` class, we go to the ```Handler``` class (due to the new ```Handler``` object being created). The first thing that happens in this class is the initialization of the ```text``` variable of type ```String```. It is initially empty. Then we go to the HandleRequest method. Here is the head and body of the HandleRequest method again:
```
public String handleRequest(URI url) {
        if(url.getPath().equals("/add-message"))
        {
            String query = url.getQuery();
            String input_text = query.substring(query.indexOf('=')+1);
            text = text + "\n" + input_text;
            System.out.println(text);
        }

        return text;
    }
```
It takes in as an argument the URL of the current server. The first if-statement then reads the URL's path with the ```getPath()``` method and checks if it is equal to the ```String``` "/add-message". If this String is not the path of the URL, the if-statement body does not run, and the method simply returns the ```text``` String without changing it. But if this String is the path of the URL, then we use the getQuery() method to get the query of the URL. We set this equal to the variable query. Using the substring() method, we find the relevant text that was typed into the URL after the = sign, and set this equal to equal the variable input_text. The next line of code is important: it takes the current value of the text String and then asks it to skip a line, and then it adds the value of the input_text String, which contains the text from the user input after the = sign in the URL. Basicallly, the ```text``` variable changes everytime this body of the if-statement runs. But it is never changed completely; it is only appended to. This is important because it ensures the previous text that was typed  is displayed as well. And lastly, we print out the text variable with System.out.println(), which is what allows it to be displayed on the page, and the ```text``` variable is returned.



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

```
sum += nums[i + 1];
```

If i is always even, then i+1 is always odd. What this means is that nums[i+1] is NOT accessing the even indices; it's actually accessing only the ODD indices. This is a major bug in the program because the program is not evenn adding the indices it is supposed to be, so it is bound to produce an incorrect output every time. The first way to fix this bug is by replacing i+1 with i; this will ensure that the nums array is accessing only its even indices rather than only its odd indices. Here's the updated method body:

```
static int sumEvenIndices(int[] nums) {
    int sum = 0;
    for(int i = 0; i < nums.length; i += 2) {
      sum += nums[i];
    }
    return sum;
  }
```

Let's test the program again with this bug eliminated. 
![Screenshot (41)](https://user-images.githubusercontent.com/130017333/233815654-fa83a172-a4e8-46a3-b077-799b8790b651.png)
And sure enough, all of the tests pass with JUnit! I even included one more test just to be safe.

Part 3: What I Learned in Lab

Something that I learned from lab in Week 2 was how to write a program that could take in a URL as an input and then output something on an online web page. I learned the existence of the getQuery() and getPath() methods to access the query and path, respectively, of an input URL, and I learned the importance of the port of a URL to indicate the specific web server the program runs on.


