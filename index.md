## StringServer.java Code

<details>
  <summary>Click to view code!</summary>
<br/>

```java
import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String str = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) 
        {
            return "No messages to add";
        } 
        else if (url.getPath().equals("/add-message"))
        {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s"))
                str += parameters[1] + "\n";
                return String.format("%s", str);
        }
        return "Error 404 not found";
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
```

</details>

<details>
  <summary>Screenshots</summary>
![Image](Hello.png)	
![Image](World!.png)	
</details>


