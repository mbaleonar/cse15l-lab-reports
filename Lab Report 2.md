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

*Test 1*

![image](https://user-images.githubusercontent.com/122484639/215359935-aad0828f-078b-4de3-9d15-843254a26bd2.png)
![image](https://user-images.githubusercontent.com/122484639/215359952-5ce1e7ce-48bf-4e85-ac5a-1cfe57ffcdee.png)


