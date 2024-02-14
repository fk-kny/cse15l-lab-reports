# CSE 15L Lab Report 2
## Serveers and SSH Keys
### Flora Kang

**Part 1**
ChatServer code:
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

Examples using `/add-message`

1. <img width="1167" alt="Screen Shot 2024-02-13 at 10 03 20 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/c61cc420-69c9-4254-ac4d-280688c41b0a">

* Which methods in your code are called?
* What are the relevant arguments to those methods, and the values of any relevant fields of the class?
* How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
2. <img width="1166" alt="Screen Shot 2024-02-13 at 10 03 44 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/3fa36ef7-ce68-435b-9eba-aaf96824b9ee">

* Which methods in your code are called?
* What are the relevant arguments to those methods, and the values of any relevant fields of the class?
* How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

**Part 2**
![]()
* The absolute path to the private key for your SSH key for logging into ieng6 (on your computer, an EdStem workspace, or on the home directory of the lab computer)
![]()
* The absolute path to the public key for your SSH key for logging into ieng6 (this is the one you copied to your account on ieng6, so it should be a path on ieng6's file system)
![]()
* A terminal interaction where you log into your ieng6 account without being asked for a password.

**Part3**
In a couple of sentences, describe something you learned from lab in week 2 or 3 that you didn't know before:
Before these two weeks, I did not know anything about web servers and coding a website, so all of the material and skills were brand new to me!
Previously, I only knew about coding within an application such as edStem workspaces, VSCode, Eclipse, etc, and had wanted to know how websites that everyday people use were created.
I learned what the parts of a URL mean and how I can navigate a site using those ideas.
