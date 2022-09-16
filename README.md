# s-furlong.github.io
Blog Entries

Blog Post: 16 Sept 2022: HTTP SERVER


The intention of this blog was to map out and understand the thought process that went behind solving several challenges that went into composing the HTTP server.

Introduction
The  purpose of this project was to create a server that could take in a variety of requests from a client end And process proper  response to meet those client needs. These requests would allow for a client to access a server utilizing HTTP protocols. This would ultimately allow requests  and responses to be transported over the internet similar to a server found on a web browser. As a learning exercise,  this project gave me the opportunity to understand how information is sent to and from a server. It also provided the knowledge to understand how this server can deal with different unique requests from clients. My  goal for this project was to gain an understanding of the Java language, the development environment  to utilize Java, and  gain a comprehension of HTTP protocols by utilizing the server. 

Server Changes from Echo Server
The http server is  a further enhancement of the echo server that I had created in a previous project.  The overall  structure of the server was similar to that project with key differences. For reference,  the echo server was established with websockets in which a client socket communicates with a server socket. Once the client socket is established,  the server socket accepts that communication with the client socket and then is receptive to any communication that the client chooses to make. Once that communication is complete,  the sockets then closed for the client in the server can now take a new  connection from a new client. The limitation of the echo server was that it only allowed for the text the client submitted to the server to be a code back to them.  it did not accommodate any further requests or allow for submission of HTTP protocol. The key changes that need to be made involve shifting the functionality from simply echoing a message  to facilitating HTTP requests such as GET, HEAD, POST, etc.

Request
In order to properly facilitate these changes, one of  the most important aspects for my comprehension of the HTTP server was to understand how the client is sending their request. This request came in through a bufferedreader through the read line function. The request was then formed into a single string following the http protocol format. This format includes any HTTP methods, the  specific path,  the version of HTTP that we are using to communicate,  any headers that are necessary,  and a body if included. The body required a different method to extract the data which will be explained later. It was important to understand each component of this request and what it is doing in order to properly utilize each component for a response. Once I had this understanding,  I needed to parse  each individual component so my router would be able to appropriately handle the request.

“VERB PATH VERSION\r\nHEADERS\r\n\r\nBODY”

Verb
The HTTP method,  also known as a verb,  describes the action  that needs to be done to the request. Each request would require specific verbs and it was important to keep track of which verb was appropriate for what was being done. 
Path
The path was another important element.  This was a vital piece of information when composing my router. The router looks for specific paths in order to perform specific actions while establishing a response.
Version
This router only used HTTP/1.1 as the  version of communication protocols that would occur between the client and the server. This meant that I needed to have a good understanding of the HTTP/1.1 documentation.
Headers
Understanding the  purpose of headers was another important aspect of creating this server. Headers provide specific levels of detail about the request.  This helps to facilitate how to request  be utilized in the router  in order to create a valid response.  attention to the headers was more important in the responses  but I still needed to extract information from request headers.  An important example came from the content-length header.  This header determined how long the body would be and how many characters would need to be read in order for their server to return the whole body.
	Body
Extracting the body from the request was one of the more challenging aspects of completing this project. The readline method originally used stopped reading the request after the new line(\r\n\r\n) formed. I was able to resolve this problem by creating a new method to hand the body that reads each individual character of the body that would be able to run through my router.

Router
The router was used to take the parsed components of the request and handle those components to form a valid response.  This was done by utilizing an interface in Java that utilizes two methods.  The first method accessed the verb  or verbs that  were necessary  to facilitate a successful client response.  then the second method utilizes those verbs and attached appropriate headers in order to convert the request into a response. A big component to understand within the router was ensuring that the correct path names were accessed in order for the interface to extract the appropriate methods.

Response
	The response was another component that needed to be in specific format. The response from the server. The response had three elements that included a status code, any necessary headers,  and a body if given.

	“VERSION STATUS CODE\r\nHEADERS\r\n\r\nBODY”

The challenge that was presented in the response was taking the components that were extracted in the router and converting the data types to a string that matches the above format. Another challenge with the response included the fact that a response may take in all three parameters (status code, headers,  body) or it may only take a few of these parameters. This was solved by utilizing functionality within the Java programming language. I had multiple constructor  for the response. Java  knows  to override the Constructor if certain parameters were omitted or included. 
Status Code
The status code is probably the most important element in determining what to do with the request that was given.  A 200 response meant that everything was done properly and the client can now see what was requested. This Server included three other status codes to handle requests that may have been done in error.  404 was a catch-all status code that determined the  location for the request could not be found. This was determined primarily on the path name that was given and if it matched a path that was found in the router.  A 405 status code meant that the correct path was given but it could not process the HTTP verb that was provided. Finally, 301 mint at the location that changed in the path was then redirected to the correct location. 
Headers
Understanding which header was appropriate for the response was the key to creating a valid response. Within the context of this project, I needed to be able to add the allow header and the content length whenever the request required that from the response. These headers were taken in as key value pairs and then converted into strings. This string was then added to the response for the client.
Body
Once I was able to solve the challenge of extracting the body through the character builder in the request,  accessing that body for a response was much easier.  The body was accessed by obtaining the instance of that body in the request and then added to the response back to the client.

Challenges and Takeaways
This project proved to be challenging in many regards. One challenge included creating a stable development environment with Java utilizing the IntelliJ IDE. Learning how to create a walking skeleton in a new IDE utilizing Gradle Had several additional steps that required attention to detail and ensuring my local machine maintained inappropriate jdk and up to date versions of the latest software being utilized. Another challenge was comprehending how to take a client request in the form of a string and extract the information needed to tell the server what exactly the client is looking for. I was really able to gain an understanding of java as a language and the ability to take that string and parse it in order to get the appropriate information needed to form a response. Throughout the course of constructing HTTP server,  I gained a comprehensive understanding of websockets, HTTP protocol  format, correct use of data types in order to allow client information  to pass through the server and return the appropriate response. I was able to evolve my understanding of how a web server can take my request on a web page and return the appropriate information that I'm looking for. 


