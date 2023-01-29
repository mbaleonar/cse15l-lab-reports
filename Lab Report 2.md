## CSE 15L Week 3
# Servers and Bugs
---

## Part 1: String Server
Below is the code for my `StringServer` web server that creates a local webserver and adds and outputs strings aafter a `=` argument:

    import java.io.IOException;
    import java.net.URI;
    class Handler implements URLHandler {
        // The one bit of state on the server: a number that will be manipulated by
        // various requests.
        String returnString = "";
        public String handleRequest(URI url) {
            if (url.getPath().equals("/")) {
                return returnString;
            }
            else {
                System.out.println("Path: " + url.getPath());
                if (url.getPath().contains("/add-message")) {
                    System.out.println(url.getQuery());
                    String[] parameters = url.getQuery().split("=");
                    if (parameters[0].equals("s")) {
                        for (int i = 1; i < parameters.length; i ++){
                            returnString += parameters[i] +"\n";
                        }
                        return returnString;
                    }
                    return (returnString);
                }
            }
            return "404 Not Found!";
        }
    }

    class StringServer {
        public static void main(String[] args) throws IOException {
            if(args.length == 0){
                System.out.println("Missing port number! Try any number between 1024 to 49151");
                return;
            }
            int port = Integer.parseInt(args[0]);
            Server.start(port, new Handler());
        }
    }

And to run the server, you would input this into VSC's terminal:

    javac Server.java StringServer.java
    java Main [port]
    //e.g: java Main 8080
This is also implied that there is a blackbox `Server.java` file that handles the URL.

Here are two instances of using `/add-message`,  with both the VSC and the web-browser each:

># *Test 1*
>
>![image](https://user-images.githubusercontent.com/122484639/215359935-aad0828f-078b-4de3-9d15-843254a26bd2.png)
>![image](https://user-images.githubusercontent.com/122484639/215359952-5ce1e7ce-48bf-4e85-ac5a-1cfe57ffcdee.png)
>
>The methods of my code are called handleRequest, which solely handles a url request created at the specified port number (4567 in this case).
>
>The relevant argument of this method is scanning the url path and see if it contains `/add-message`, which subsequently scans everything past
>the command `s=` and concatenates it into a `String returnString` value with a `\n` value at the end to make way for subsequent `/add-message` commands.
>
>The only value changed is `returnString` in each passthrough.

># *Test 2*
>![image](https://user-images.githubusercontent.com/122484639/215361029-f06fc5a9-60f3-4278-bee8-45637615315e.png)
>![image](https://user-images.githubusercontent.com/122484639/215361056-e7e7a12d-997f-471f-bf07-c181a4e3483e.png)
>
>The methods haven't changed, although I changed the port to (4512) and tested single word add values, strings with multiple spaces and strings with numbers.
>
>Another test I tried was also to add another `s=` to see what would happen, and it seems like it simply adds another `\n` into the `returnString` value.
---
## Part 2: Array Method Bugs

From the lab, I went ahead and chose the `ArrayExamples` file to debug. 

The failure-inducing input for `testReverseInPlac`e was any `int[]` array that wasn’t a palindrome, such as in this code:

    @Test
    public void testReverseInPlace() {
        int[] input1 = { 3,27,99,740,100,6,15};
        ArrayExamples.reverseInPlace(input1);
        assertArrayEquals(new int[]{ 15,6,100,740,99,27,3 }, input1);
    }
  
 with the output as:
 
    arrays first differed at element [4]; expected:[99] but was:[100]
    at ArrayTests.testReverseInPlaceTwo(ArrayTests.java:16)
    Caused by: java.lang.AssertionError: expected:[99] but was:[100]
    ... 31 more

The failure-inducing input for `testReversed` was any array that wasn’t entirely made up of zeroes.

    @Test
    public void testReversed() {
        int[] input1 = {3,27,99,740,100,6,15};
        assertArrayEquals(new int[]{15,6,100,740,99,27,3}, 
        ArrayExamples.reversed(input1));
    }
which outputs:

    arrays first differed at element [0]; expected:[15] but was:[0]
    at ArrayTests.testReversedTwo(ArrayTests.java:29)
    Caused by: java.lang.AssertionError: expected:[15] but was:[0]
    ... 31 more

For `testReverseInPlace`, placing a palindrome as the input does not induce a failure.

    @Test 
    public void testReverseInPlaceTwo() {
        int[] input1 = {3,27,100,27,3};
        ArrayExamples.reverseInPlace(input1);
        assertArrayEquals(new int[]{3,27,100,27,3}, input1);
    }
    
and here is the JUnit test result:
![image](https://user-images.githubusercontent.com/122484639/215362291-98491978-9363-4aa1-b74c-9efb80314022.png)

For `testReversed`, the non-failure-inducing input is any length array with only zeroes as the values.

    @Test
    public void testReversedTwo() {
        int[] input1 = {0,0,0,0,0};
        assertArrayEquals(new int[]{0,0,0,0,0}, ArrayExamples.reversed(input1));
    }

and here is the JUnit test result:

![image](https://user-images.githubusercontent.com/122484639/215362386-76f30322-3c7a-4033-aec7-ec815f13417e.png)

The symptom for ReverseInPlace was an error message saying the element past the halfway point was expected to be the next reversed array item, but was instead the item two indices prior.  
The symptom for Reversed was an error message claiming the first element was expected to be the first reversed item but was instead “zero”.

The code after the fixes are as such:

    @Test 
    public void testReverseInPlaceTwo() {
        int[] input1 = {3,27,99,740,100,6,15,5,12};
        ArrayExamples.reverseInPlace(input1);
        assertArrayEquals(new int[]{12,5,15,6,100,740,99,27,3}, input1);
    }
    
and

    @Test
    public void testReversedTwo() {
        int[] input1 = {3,27,99,740,100,6,15};
        assertArrayEquals(new int[]{15,6,100,740,99,27,3}, ArrayExamples.reversed(input1));
    }




