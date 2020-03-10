*Lectures 3, 4, 5 & 6*
# Application Layer
#### Objectives:
1. conceptual, implementation aspects of network application protocols.
	- transport-layer service models.
	- client-server paradigm.
	- peer-to-peer paradigm.
1. learn about protocols by examining popular application-level protocols.
	- HTTP.
	- SMTP / POP3 / IMAP.
	- DNS
1. creating network applications.
	- socket API.
--------------------------------------------------
#### Client-Server Architecture
- Servers
	- always on-host.
	- static IP address.
- Clients
	- communicate with the server.
	- dynamic IP addresses.
	- DO NOT directly communicate with eachother.

#### Peer-To-Peer Architecture
- *No* 'always-on' server.
- End systems communicate **directly**.
- **Self Scalabaility** - new peers bring new service capacity, as well as new service demands.
- ISP friendly!
- Bluetooth for example, but bluetooth happens at a much lower layer.

##### Problems :
1. Security.
1. Incentives.
--------------------------------------------------
#### Processes Communicating
A process is a program running within a host. Within the same host, two processes communicate using **inter-process communication**.

Processes are identified by both their *IP address* and their *Port Numbers*.

#### Sockets
Processes send/receive messages to/from its **socket**.

--------------------------------------------------
### Application Layer Protocols
1. Types of messages exchanged.
1. Message Syntax.
1. Message Semantics.
1. Rules for when and how send & respond to messages.

#### Transport Services for Apps
1. Data Integrity :
	- some apps require 100% reliable data transfer (file transfer, web transaction).
	- other apps can tolerate some loss (audio).
1. Timing :
	- some apps require low delay to be effective (internet telephony, interactive games).
1. Throughput :
	- some apps require minimum amount of throughput to be effective (multimedia e.g. Netflix).
	- other apps make use of what they get (elastic apps).
1. Security :
	- encryption, data integrity...
--------------------------------------------------
#### Internet Transport Protocols
| TCP  | UDP |
|---|---|
| **Reliable Transport**  | **Unreliable Data Transfer**  |
| **Flow Control** | **No** flow control |
| **Congestion Control** | **No** congestion control |
| **Connection-Oriented** | **No** connection setup |
| **No** timing, throughput guarantee or security | **No** timing, throughput guarantee or security

Why does UDP still exist?
- When you drop a few packets with UDP, you get a bit of static. But if you were to lose TCP packets, the entire voice stream stops completely until the missing packets could be re-sent, and then continues on.
--------------------------------------------------
#### Electronic Mail
Three Major Components :
1. user agents.
	- composing, editing, reading email messages.
1. mail servers.
	- mailbox - incoming message for user.
	- message queue - of outgoing mail messages.
1. Simple Mail Transfer Protocol : SMTP.
	- sending email messages between mail servers.
	- uses TCP to reliably transfer email messages - port 25.
	- Three phases of Transfer :
		1. handshaking
		1. transfer of messages
		1. closure
	- **messages must be in 7-bit ASCII**.
--------------------------------------------------
#### Mail Access Protocols
- SMTP : deliver TO server.
- Retrieve FROM server :
	- **POP**: Post Office Protocol
		- authorisation phase, download phase.
	- **IMAP**: Internet Mail Access Protocol
		- keeps all messages on one server.
		- allows user to organise messages (at server).
		- more features + manipulation of stored messages on server.
	- **HTTP**: gmail, Hotmail, Yahoo! Mail, etc...
		- server-to-server communication
		- sending/pushing an email to the user's SMTP server is also done through HTTP.
		- MIME (Multipurpose Internet Mail Extensions) is used widely in HTTP. Extends the email formatting standards.

| Internet Mail Access Protocol (IMAP) | Multipurpose Internet Mail Extensions (MIME) |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| - keeps all messages in one place : **at server**. | - uses email to support: text in other character sets; non-text  attachments : audio, video, images etc; message bodies with multiple  parts. |
| - allows users to organise messages in folders. | - all human-written internet email is transmitted via SMTP in MIME format. |
| - keeps user state across sessions. | - MIME designed for SMTP but extensively used in HTTP. |
| - users can get *parts* of a multi-part message. <br> | - *Content Type* : text/plain, image/jpeg, audio/mp3, video/mp4, application/msword. |
### HTTP
--------------------------------------------------
HTTP uses TCP. <br>
**RTT** : time for small packet to travel from client to server and back.
#### HTTP - TCP Connections
**Non-Persistent HTTP** :
- at most one object sent over TCP, connection is then closed. Costs : 
	- requires 2 RTTs per object.
	- this has latency implications = 2RTT + file transmission time.
- downloading several objectives requires several connections.

**Persistent HTTP** :
- several objects can be sent over a single TCP connection. Costs :
	- server leaves connection open.
	- client sends request as soon as it encounters a referenced object.

#### HTTP Method Types:
**HTTP/1.0** :
- GET.
- POST.
- HEAD.
	- asks server to leave requested object out of response.

**HTTP/1.1** :
- GET.
- POST.
- HEAD.
- PUT.
	- uploads file in entity body to path specified in URL field.
- DELETE.
	- deletes file specified in URL field.

#### Uploading Form Input
- **POST** Method
	- web page includes form input, which is uploaded to server in entity body.
- **URL**
	- uses **GET** method, input is uploaded in URL field of request.

#### HTTP Response Status Codes Examples :
- **200** OK.
- **301** Moved Permanently.
- **400** Bad Request.
- **404** Not Found.
- **505** HTTP Version Not Supported.

#### HTTP v2.0
Main aim : decrease latency to improve page load speed in web browsers.
- data compression of HTTP headers.
- HTTP/2 Server Push.
- fixing the head-of-line blocking problem in HTTP 1.x
- multiplexing multiple requests ver a single TCP connection.

### Cookies
--------------------------------------------------
4 Components of Cookies : 
1. cookie header line of HTTP response message.
1. cookie header line in next HTTP request message.
1. cookie file kept on user's host, managed by user's browser.
1. band-end 'database' at website.

#### Use of Cookies
1. authorisation.
1. shopping carts.
1. recommendations.
1. user state sessions.
	- state maintained through protocol endpoints : sending/receiving over multiple transactions.

#### Cookies & Privacy
- Cookies permit sites to learn a lot about you.
- You may supply your name and email to sites.

### Web Caches
--------------------------------------------------
*Goal* : satisfy client request without involving origin server.

- User sets browser : Web accessess via cache.
- Browser sends all HTTP requests to cache.

Cache acts as both client and server, server for original requesting client and client to the origin server. Typically, cache is installed by ISP (university, company, residential ISP)
.
#### Why we use Web Caching
1. reduce response time for client request.
1. reduce traffic on an access link.
1. enables content providers to effectively deliver content.


...

...

...

...

...

...

...

...

...

...

...


### Content Delivery Networks
--------------------------------------------------
- Overlay networks across the world.
- Efficiently manage popular content on behalf of content providers.
- DNS Redirection

### Socket Programming
--------------------------------------------------
<center> <b>Socket</b>

A <i>host-local</i>, <i>application-created</i>, <i>OS-controlled</i> interface into which an application process can <b>both send and receive</b> messages to/from another application process.

</center>

#### Socket Programming using TCP
TCP Service : reliable transfer of bytes from one proces to another.

**Client must contact the server** :
- server process must first be running.
- server must have created a socket that welcomes client's contact.

**Client contacts the server by** :
- creating a client-local TCP socket.
- specifying IP address, port number of server address.


<center>

### Example : Java Client (TCP)

</center>
```
import java.io.*;
import java.net.*;

public class TCPClient {

    public static void main(String argv[]) throws Exception { 
        String sentence; 
        String modifiedSentence;

        BufferedReader inFromUser = new BufferedReader(new InputStreamReader(System.in)); 
        Socket clientSocket = new Socket("hostname", 6789); 
        DataOutputStream outToServer = new DataOutputStream(clientSocket.getOutputStream());

	    BufferedReader inFromServer = new BufferedReader(new InputStreamReader(clientSocket.getInputStream())); 
        sentence = inFromUser.readLine(); 
        outToServer.writeBytes(sentence + '\n');
        modifiedSentence = inFromServer.readLine(); 
        System.out.println("FROM SERVER: " + modifiedSentence);
  
	clientSocket.close(); 
	}
}
```

<center>

### Example : Java Server (TCP)

</center>

```
import java.io.*; 
import java.net.*;

public class TCPServer {

  public static void main(String argv[]) throws Exception {
 
      String clientSentence; 
      String capitalizedSentence; 

      ServerSocket welcomeSocket = new ServerSocket(6789); 

      while(true) { 

           Socket connectionSocket = welcomeSocket.accept(); // create a new thread after this.
           BufferedReader inFromClient = new BufferedReader(new InputStreamReader(connectionSocket.getInputStream()));

           DataOutputStream outToClient = new DataOutputStream(connectionSocket.getOutputStream());
           clientSentence = inFromClient.readLine(); 
           capitalizedSentence = clientSentence.toUpperCase() + '\n'; 
           outToClient.writeBytes(capitalizedSentence); 
        } 
    } 
}
```

#### Socket Programming using UDP
UDP : no *connection* between client & server. <br>
UDP : transmitted data may be received out of order, or lost. 

UDP provides an unreliable transfer of groups of bytes (*datagrams*) between the client & server.
- no handshaking.
- server must extract IP address, port of sender from received packet.

<center>

### Example : Java Client (UDP)

</center>

```
import java.io.*; 
import java.net.*;

public class UDPClient {

    public static void main(String args[]) throws Exception {
 
      BufferedReader inFromUser = new BufferedReader(new InputStreamReader(System.in)); 
      DatagramSocket clientSocket = new DatagramSocket(); 
      InetAddress IPAddress = InetAddress.getByName("hostname"); 

      byte[] sendData = new byte[1024]; 
      byte[] receiveData = new byte[1024]; 

      String sentence = inFromUser.readLine(); 
      sendData = sentence.getBytes();

      DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, IPAddress, 9876); 
      clientSocket.send(sendPacket); 
      
	  DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length); 
      clientSocket.receive(receivePacket); 
      String modifiedSentence = new String(receivePacket.getData()); 
      System.out.println("FROM SERVER:" + modifiedSentence); 
      
	  clientSocket.close(); 
      } 
}
```

<center>

### Example : Java Server (UDP)

</center>

```
import java.io.*; 
import java.net.*; 

public class UDPServer {
 
  public static void main(String args[]) throws Exception {
 
      DatagramSocket serverSocket = new DatagramSocket(9876); 
      byte[] receiveData = new byte[1024]; 
      byte[] sendData  = new byte[1024]; 
      
	  while(true) { 
           DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length); 
           serverSocket.receive(receivePacket);

		  String sentence = new String(receivePacket.getData()); 
          InetAddress IPAddress = receivePacket.getAddress(); 
          int port = receivePacket.getPort();

          String capitalizedSentence = sentence.toUpperCase(); 
          sendData = capitalizedSentence.getBytes(); 
          DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, IPAddress, port); 
          serverSocket.send(sendPacket); 
        } 
    } 
}
```
