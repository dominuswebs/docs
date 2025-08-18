Things to know / be aware

Unified Modelling Language (UML) - https://www.smartdraw.com/uml-diagram

Compiled vs Interpreted

The difference between an interpreted and a compiled language lies in the result of the process of interpreting or compiling. An interpreter produces a result from a program, while a compiler produces a program written in assembly language. 

The assembler of architecture then turns the resulting program into binary code. Assembly language varies for each individual computer, depending upon its architecture. Consequently, compiled programs can only run on computers that have the same architecture as the computer on which they were compiled.


Nomenclature

A CALLER passes ARGUMENTS. A METHOD takes PARAMETERS.


OOP

Encapsulation

Mark instance variables PRIVATE

Mark getters and setters PUBLIC

This allows us to change the logic in the setters and getters later without breaking code.

Inheritance - IS A

One class inherits properties and behavior from another class i.e., "is-a" relationship. This can be useful for code reuse, as a subclass can reuse the code of its superclass and add new functionality as needed. 

However, inheritance can also lead to tight coupling between classes, as changes to the superclass can have unintended consequences for the subclass. This can make the code difficult to maintain, modify, or extend.

Delegation

Involves creating a new class that contains an instance of the existing class and delegates some of its responsibilities to it. This allows for greater flexibility and modularity in the design, as well as better control over the interactions between classes. Aggregation and composition are two ways to achieve delegation.

Aggregation - HAS A

Is a relationship between two classes where one class is a "has-a" relationship to the other class. This means that the first class contains an instance of the second class, but the second class can still exist independently of the first class. For example, a car has an engine, but the engine can exist independently of the car.

Advantages of Aggregation:

Code Reusability: Aggregation allows for code reusability by allowing multiple classes to share a single object.

Flexibility: Since the second class can exist independently of the first class, aggregation provides flexibility in the design of the system.
		
Reduced Coupling: Aggregation reduces coupling between classes, making the system easier to maintain and modify.
				
Disadvantages of Aggregation:

Memory Management: The first class is responsible for managing the lifetime of the second class, which can lead to memory leaks if not properly handled.

Complexity: Aggregation can add complexity to the system design, especially if there are multiple levels of aggregation.

Suitable Scenarios for Aggregation:

A Book and Author relationship: A Book can have many Authors and an Author can write many Books.

A University and Student relationship: A University can have many Students, but each Student can also attend multiple Universities.

Composition - PART OF

Is a stronger form of aggregation where the second class is owned by the first class. This means that the second class cannot exist independently of the first class. In other words, the two classes have a "part-of" relationship, where the first class "has" an instance of the second class and controls its lifetime.For example, a house is composed of many rooms, but each room is exclusively part of one house.

Advantages of Composition:

Strong Relationship: Composition provides a strong relationship between classes, ensuring that the second class cannot exist independently of the first.

Memory Management: Since the second class is owned by the first class, memory management is easier and less error-prone.

Simplicity: Composition provides a simpler and more straightforward design, as the relationship between the classes is clear.

Disadvantages of Composition:

Code Reusability: Composition does not allow for code reusability at the run time, as the second class cannot be shared among multiple instances of the first class.

Rigidity: Composition provides less flexibility in the design of the system, as the second class is exclusively owned by the first class.

Suitable Scenarios for Composition:

A House and Room relationship: A House is made up of many Rooms, but each Room is exclusively part of one House.

A Car and Engine relationship: A Car owns an Engine, and the Engine cannot exist independently of the Car.

Differences between Aggregation and Composition:

Ownership: In Aggregation, the second class can exist independently of the first class, whereas in Composition, the second class is owned by the first class.

Lifetime: In Aggregation, the first class does not control the lifetime of the second class, whereas in Composition, the first class controls the lifetime of the second class.

Reusability: Aggregation allows for code reusability, whereas Composition does not at the run time.

Flexibility: Aggregation provides more flexibility in the design of the system, whereas Composition provides a stronger relationship between classes.

In aggregation, the first class holds a pointer or reference to the second class, whereas in composition, the first class owns an instance of the second class.

Polymorphism

Polymorphism describes the concept of using different classes with the same interface. Each of these classes can provide its implementation of the interface.

Java supports two kinds of polymorphism. You can overload a method with different sets of parameters. The compiler statically binds the method call to a specific method, which we know as static polymorphism.

Within an inheritance hierarchy, a subclass can override a method of its superclass. The JVM will always call the overridden method if you instantiate the subclass. Even if you cast the subclass to its superclass, the result will be the same. That is dynamic polymorphism.

Network

A socket is a fundamental concept in network programming that serves as an endpoint for sending and receiving data across a network. It provides the necessary infrastructure to allow communication between two devices (e.g., computers) over a network, whether it's on the same machine or across the internet.

Key Concepts of Sockets
Endpoints of Communication:

A socket is essentially one end of a two-way communication link between two programs running on a network. A pair of sockets, one on each end of the communication, facilitates data exchange.
Combination of IP Address and Port:

Each socket is associated with an IP address and a port number. The IP address identifies the machine on the network, and the port number identifies the specific application or service on that machine.
Socket Types:

Stream Sockets (TCP):
Provides reliable, connection-oriented communication. The Transmission Control Protocol (TCP) is typically used with stream sockets.
Example: Web browsers use TCP sockets to connect to web servers.
Datagram Sockets (UDP):
Provides connectionless, unreliable communication. The User Datagram Protocol (UDP) is typically used with datagram sockets.
Example: Video streaming or gaming applications that can tolerate some data loss use UDP sockets.
How Sockets Work
Server and Client:

Typically, network communication using sockets involves a server and one or more clients.
The server listens on a specific port, waiting for clients to connect.
The client initiates the connection by specifying the server's IP address and port number.
Establishing a Connection (TCP):

Server Side:
The server creates a ServerSocket object, binds it to a specific port, and listens for incoming connection requests.
When a client attempts to connect, the server accepts the connection, creating a new Socket object for the communication.
Client Side:
The client creates a Socket object and attempts to connect to the server using the server's IP address and port number.
Once the connection is established, the client and server can send and receive data.
Data Transmission:

After a connection is established, both the server and client can send data to each other using input and output streams associated with the socket.
For TCP sockets, data transmission is reliable and ensures that data is delivered in the correct order.
For UDP sockets, data is sent as individual packets, with no guarantee of delivery or order.

How HTTP Works with Sockets
TCP as the Transport Layer:

HTTP relies on TCP (Transmission Control Protocol) for the underlying communication. TCP provides a reliable, connection-oriented service, which means that data is guaranteed to be delivered in the same order it was sent, without duplication or loss.
When you access a website using a browser, the browser establishes a TCP connection to the server hosting the website using a TCP socket.
Establishing the Connection:

Client Side (Browser):
The browser initiates a TCP connection to the server by creating a socket that connects to the server's IP address and port number (typically port 80 for HTTP or port 443 for HTTPS).
Server Side (Web Server):
The server listens on a specific port (usually 80 for HTTP or 443 for HTTPS). When a TCP connection request is received, the server accepts the connection and establishes a socket to communicate with the client.
HTTP Communication:

Once the TCP connection is established, the client (browser) sends an HTTP request over this connection, such as a GET request to retrieve a webpage.
The server processes the request and sends back an HTTP response over the same TCP connection. The response might include the requested HTML page, images, or other resources.
After the data is exchanged, the TCP connection can be closed, though in many cases, the connection might be kept alive for a period to handle additional requests.
Example of the Flow
Client (Browser):

Establishes a TCP connection to www.example.com on port 80 (for HTTP).
Sends an HTTP request: GET /index.html HTTP/1.1.
Server (Web Server):

Accepts the TCP connection on port 80.
Receives the HTTP request and processes it.
Sends an HTTP response: HTTP/1.1 200 OK, followed by the content of index.html.
HTTP vs. TCP
TCP (Transport Layer):

Handles the low-level details of data transmission, ensuring that data packets are delivered reliably and in order between two endpoints (client and server).
HTTP (Application Layer):

Defines the rules for requesting and transferring resources (like HTML pages, images, etc.) between a client (like a web browser) and a server. It specifies methods like GET, POST, PUT, etc., and handles headers, status codes, and message bodies.
In summary, HTTP is an application-level protocol that leverages the reliable transport services provided by TCP sockets to facilitate communication between web clients and servers.


WebSockets
HTTP Handshake:

Initial Connection: A WebSocket connection begins with an HTTP request. The client (often a web browser) sends an HTTP request to the server with an "Upgrade" header, asking to switch from the HTTP protocol to the WebSocket protocol.
Upgrade to WebSocket: If the server supports WebSockets, it responds with an HTTP 101 status code, agreeing to the protocol upgrade. After this, the connection is no longer an HTTP connection but a WebSocket connection.
Full-Duplex Communication:

Once the WebSocket connection is established, it allows for full-duplex (two-way) communication. Both the client and server can send and receive messages independently of each other, without the need for repeated HTTP requests.
Uses TCP:

WebSockets operate over a TCP connection, meaning they inherit the reliable, connection-oriented nature of TCP. However, WebSockets are a higher-level protocol, designed specifically for web-based real-time communication.
Applications:

WebSockets are commonly used for applications like live chats, real-time notifications, multiplayer online games, and live data feeds.
Traditional TCP Sockets
Direct TCP Connection:

Traditional TCP sockets are used for low-level network communication. There’s no HTTP involved; you directly create a socket, connect to a remote host and port, and start sending and receiving data.
This is the most basic form of network communication, often used in custom protocols, non-web-based communication, or services where HTTP or WebSocket overhead is unnecessary.
Full Control:

With TCP sockets, you have full control over the communication process. You define how the data is structured, how connections are managed, and how data is sent and received.
Uses TCP:

Like WebSockets, traditional TCP sockets also use TCP for reliable, ordered communication. However, they don’t involve any higher-level protocol like HTTP or WebSocket.
Applications:

TCP sockets are used in a wide range of applications, including server-client systems, custom protocols, peer-to-peer networks, and any situation requiring efficient, low-level communication.

Key Differences
Establishment:

WebSockets: Start with an HTTP handshake, then upgrade to a WebSocket connection.
TCP Sockets: Directly create and manage a TCP connection without involving HTTP.
Purpose:

WebSockets: Specifically designed for web applications requiring real-time, interactive communication between a client (typically a browser) and a server.
TCP Sockets: General-purpose, low-level network communication for any type of data exchange.
Overhead:

WebSockets: Have some initial HTTP overhead during the handshake phase, but then offer efficient, persistent communication.
TCP Sockets: Minimal overhead since they don’t involve HTTP, making them suitable for custom, high-performance applications.


Deployment CI/CD

Git

