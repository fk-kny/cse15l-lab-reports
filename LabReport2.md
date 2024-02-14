# CSE 15L Lab Report 2

Servers and SSH Keys

Flora Kang

## Part 1

**ChatServer code:**
```
import java.io.IOException;
import java.net.URI;
class Handler implements URLHandler {

    String message = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Welcome!");
        } else {
            if (url.getPath().equals("/add-message")) {
                String[] param = url.getQuery().split("&");
                String[] text = param[0].split("=");
                String[] user = param[1].split("=");
                if(user[0].equals("user")) {
                    message = message + user[1] + ": ";
                }
                if(text[0].equals("s")) {
                    message = message + text[1] + "\n";
                }
                return message;
            } else return "404 Not Found!";
        }
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
*assume that the s= parameter always comes before the user= parameter, and they are always separated by an &*

**Examples using `/add-message`**

1. /add-message?s=helloo&user=user1
   <img width="1167" alt="Screen Shot 2024-02-13 at 10 03 20 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/c61cc420-69c9-4254-ac4d-280688c41b0a">

* Which methods in your code are called?
    * The method `public String handleRequest(URI url)` is called, checking the path of the incoming URI
    * The method Server.start() is called
        * this creates a new instance of `Server` and calls the start method of that class, passing a port number and an instance of `Handler`, in which we have coded our behavior for this server
* What are the relevant arguments to those methods, and the values of any relevant fields of the class?
    * The method `public String handleRequest(URI url)` takes a new `URI` `url` as the argument.
    * The class `Handler` also has the field of type String called `message` that starts as an empty String "".
* How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
    * As our code runs, the query is split into a String array containing "s=helloo" and "user=user1". These are each split by "=", giving us two String arrays:
          `user[]`, containing "user" and "user1"
          `text[]`, containing "s" and "helloo"
      from `user[]`, we take "user1" and ": ", then add those two Strings to our field `message`
      from `text[]`, we take "helloo" and a new line ("\n"), then add those to our field `message`
      this gives us "user1: helloo"

2. /add-message?s=hi :) &user=user2
    <img width="1166" alt="Screen Shot 2024-02-13 at 10 03 44 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/3fa36ef7-ce68-435b-9eba-aaf96824b9ee">

* Which methods in your code are called?
    * The method `public String handleRequest(URI url)` is called, checking the path of the incoming URI
    * The method Server.start() is called
        * this creates a new instance of `Server` and calls the start method of that class, passing a port number and an instance of `Handler`, in which we have coded our behavior for this server
* What are the relevant arguments to those methods, and the values of any relevant fields of the class?
    * The method `public String handleRequest(URI url)` takes a new `URI` `url` as the argument.
    * The class `Handler` also has the field of type String called `message` that starts as an empty String "".
* How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
    * As our code runs, the query is split into a String array containing "s=helloo" and "user=user1". These are each split by "=", giving us two String arrays:
        * `user[]`, containing "user" and "user2"
        * `text[]`, containing "s" and "hi :) "
     
    * from `user[]`, we take "user2" and ": ", then add those two Strings to our field `message`
    * then, from `text[]`, we take "hi :) " and add it to our field `message`
      this gives us "user2: hi+:)+"

          Note: we get the "+" because some browsers show the space as %20 and a special character replacing the spaces (not important as of now)

## Part 2
Using the command line, show with ls and take screenshots of:

<img width="550" alt="Screen Shot 2024-02-13 at 11 06 52 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/a8ea66a3-520b-4590-a6aa-e7817eea38dc">
* The absolute path to the **private key** for your SSH key for logging into ieng6 (on your computer, an EdStem workspace, or on the home directory of the lab computer)

PATH: /Users/flora2.kang/.ssh/id_rsa

<img width="717" alt="Screen Shot 2024-01-25 at 1 32 00 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/2ac5b2d5-6022-4a1b-9ff6-a819fae8082e">
* The absolute path to the **public key** for your SSH key for logging into ieng6 (this is the one you copied to your account on ieng6, so it should be a path on ieng6's file system)

PATH: /Users/flora2.kang/.ssh/id_rsa.pub

<img width="744" alt="Screen Shot 2024-02-13 at 11 12 19 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/69bacead-3c8c-4367-9ca3-eda6fd8723ff">
* A terminal interaction where you log into your ieng6 account without being asked for a password.

## Part3

Before these two weeks, I did not know anything about web servers and coding a website, so all of the material and skills were brand new to me!
Previously, I only knew about coding within an application such as edStem workspaces, VSCode, Eclipse, etc, and had wanted to know how websites that everyday people use were created.
I learned what the parts of a URL mean and how I can navigate a site using those ideas.
