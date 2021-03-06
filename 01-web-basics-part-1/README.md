# Introduction


[Session 01 slides](https://docs.google.com/presentation/d/19ntegcXmtk2DGBfr-FMBvEVTitvqaxaOROKlDUnNhEM/edit?usp=sharing)    
***

As the World Wide Web's high-level topology consists mainly of personal computing devices (e.g. desktops, laptops, mobile devices) making HTTP requests to web servers, the general field of web security consists of three main sub-fields: client-side security (i.e. browser security), communications security and server-side security, or web application security. This lab and the following will focus on the first sub-field, although they might provide some general information on the former two.

The design of web applications, and their security in particular is influenced by the following characteristics:

* **Statelessness:** by default HTTP is a simple request-response protocol maintaining no state between successive communications. This shortcoming led to the design of cookies, which are small pieces of information exchanged between the client and the web application. The type of information exchanged using cookies needs to be carefully chosen, as a malicious client could possibly attempt to send back a malformed or forged cookie; additionally, cookies most often (but not always) represent confidential data, which means that they should only be transferred over a secure channel (i.e. HTTPS).
* **Message format:** HTTP requests have a specific format, namely they comprise plain-text header and data (although newer improvements also implement a binary protocol). The header contains various information about the client or the server (e.g. a user-agent, page caching information, text encoding information), while the payload is very often (but not always) a HTML page.

* **Addressing:** resources on the web are located using the URI/URL addressing scheme. Possible vulnerabilities here include a misconfigured web server that allows viewing application-specific files, or worse, that allow accessing other files on the host machine. While this information leakage is not very dangerous by itself, it may be used as an intermediary stage for other attacks

* **Request methods:** HTTP communication is most often done using the GET and POST methods. Both methods allow clients to define variables and transfer them as arguments to the server. The fundamental difference between the two is that GET encodes variables in the URL, while POST encodes them in the message body. w3schools gives a brief explanation of how each of them is used.

While POST hides variables from the URL, it does not provide any communication security. HTTPS is still required to send confidential data (e.g. passwords) to the server.

While the client is provided with HTML, JavaScript, CSS pages, modern web applications are implemented using general-purpose scripting or programming languages, e.g. PHP, Java, Python, Ruby, etc. and centralize their data using database systems such as MySQL. Faulty back-end code can in itself provide a more dangerous attack surface to potentially malicious clients.

![Client - Server](https://drive.google.com/uc?export=view&id=1X004Kae-Z-h4H8XyKiF-WDPJF3Agk2e2)

# Web Applications Today

Dynamic websites provide tailored user experience based on information known or given by the user. The user usually has to authenticate to access the website and is authorized to use services it provides. In this case, the dynamic website contains information about the user, and there is therefore a great deal more for the attacker to steal. The fundamental difference to static web pages is that a dynamic webpage/website contains functionality that can be compromised. Breaching the security of the server itself is no longer necessary. It is sufficient to discover the security hole in the dynamic website functionality. We therefore need to look at the security of a web application itself. A dynamic website can be considered to be a web application.

Web applications introduce a new range of threats, or a new security perimeter, to put it another way. Depending on the setup, web applications are commonly located in an internal network or in the demilitarized zone, which therefore renders network level defenses ineffective. Network, services and operating system level defenses may have been perfectly set in place, but the system would still be vulnerable to a break-in. Web applications commonly interact with internal systems, such as database servers. The network level firewall could be blocking all traffic, but for web applications it will have to allow HTTP and HTTPS traffic. An attacker might therefore be able to bypass all network level defenses

# Types of Vulnerabilities 

These days, web applications are very complex being composed of multiple libraries, frameworks and using multiple external services. Each component can have vulnerabilities.
Types of vulnerabilities:
* System vulnerabilities - applications or services that run inside an Operating System or an Operating System vulnerability
* Runtime vulnerabilities - when one of the components (frameworks such as PHP, Java, Python, WordPress, etc.) of the web application is vulnerable lead to a risk.
* Browser vulnerabilities - occasionally attackers will discover a vulnerability in the browser itself that allows execution of arbitrary binary code when a user simply visits a compromised site. Browsers are complex pieces of machinery with many subsystems (HTML rendering, JavaScript engine, CSS parser, image parsers, etc.), and a small coding mistake in any of these systems could offer malicious code just enough of a foothold to get running
* Vulnerabilities in web application implementation - here we can talk about OWASP Top Ten vulnerabilities

In this Practical Software Exploitation we will focus mainly on the web applications implementation vulnerabilities.

# HTTP (Hypertext Transfer Protocol)

## HTTP Request / Response

Communication between clients and servers is done by requests and responses:

* A client (a browser) sends an HTTP request to the web
* An web server receives the request
* The server runs an application to process the request
* The server returns an HTTP response (output) to the browser
* The client (the browser) receives the response

![HTTP - Request](https://drive.google.com/uc?export=view&id=1g62ylxoatBomcgcKNqm1EwiiF_KPBCqI)

![HTTP - Response](https://drive.google.com/uc?export=view&id=1YR9TqYFtgaVBDrTyHFRS2CTA01fKyNT4)

### Basic format of the request:

VERB /resource/locator HTTP/1.1  
Header1: Value1  
Header2: Value2  
…  
  
<Body of the request>  
  
Header is separated from the body by 2 CRLF sequences  


### Request Headers:

* **Host:** Indicates the desired host handling the request
* **Accept:** Indicates what MIME type(s) are accepted by the client; often used to specify JSON or XML output for web-services
* **Cookie:** Passes cookie data to the server
* **Referer:** Page leading to this request (note: this is not passed to other servers when using HTTPS on the origin)
* **Authorization:** Used for ‘basic auth’ pages (mainly). Takes the form “Basic <base64’d username:password>”


### HTTP Request Circle

A typical HTTP request / response circle:

The browser requests an HTML page. The server returns an HTML file.
The browser requests a style sheet. The server returns a CSS file.
The browser requests a JPEG image. The server returns a JPG file.
The browser requests JavaScript code. The server returns a JS file
The browser requests data. The server returns data (in XML or JSON).

### XHR - XML Http Request

All browsers have a built-in XMLHttpRequest Object (XHR).

XHR is a JavaScript object that is used to transfer data between a web browser and a web server.

XHR is often used to request and receive data for the purpose of modifying a web page.

Despite the XML and Http in the name, XHR is used with other protocols than HTTP, and the data can be of many different types like HTML, CSS, XML, JSON, and plain text.

The XHR Object is a Web Developers Dream, because you can:

Update a web page without reloading the page
Request data from a server - after the page has loaded
Receive data from a server - after the page has loaded
Send data to a server - in the background
The XHR Object is the underlying concept of AJAX and JSON:

![XMLHttpRequest](https://drive.google.com/uc?export=view&id=12-9YOQSo48wVitih4r6wQqlQoRssEj7V)

### HTTP Response Codes

* 1xx -> Informational responses
* 2xx -> Successful responses
* 3xx -> Redirects
* 4xx -> Client errors
* 5xx -> Server errors

xx = [00, 01 … 99]

### URL (Uniform Resource Locator)

With Hypertext and HTTP, URL is one of the key concepts of the Web. It is the mechanism used by browsers to retrieve any published resource on the web.

URL stands for Uniform Resource Locator. A URL is nothing more than the address of a given unique resource on the Web. In theory, each valid URL points to a unique resource. Such resources can be an HTML page, a CSS document, an image, etc. In practice, there are some exceptions, the most common being a URL pointing to a resource that no longer exists or that has moved. As the resource represented by the URL and the URL itself are handled by the Web server, it is up to the owner of the web server to carefully manage that resource and its associated URL.

A URL incorporates the domain name, along with other detailed information, to create a complete address (or “web address”) to direct a browser to a specific page online called a web page. In essence, it’s a set of directions and every web page has a unique one.

![URL](https://drive.google.com/uc?export=view&id=1ZrRZywT2lVitOI4Nq3Jx6cwlW-tPiTCU)

Special characters are encoded as hex:
* **%0A** = newline
* **%20** or + = space, **%2B** = + (special exception)

## Browser

A web browser (commonly referred to as a browser) is a software application for accessing information on the World Wide Web. When a user requests a web page from a particular website, the web browser retrieves the necessary content from a web server and then displays the page on the screen.

A list of Web Browsers: Google Chrome, Mozilla Firefox, Edge, Internet Explorer, Safari, Opera, Netscape, etc.

### Browser execution model
Each browser windows or frame:
* Loads content
* Renders it
    * Processes HTML and scripts to display page
    * May involve images, subframes, etc.
* Responds to events such as:
    * User actions: OnClick, OnMouseover
    * Rendering: OnLoad, OnBeforeUnload
    * Timing: setTimeout(), clearTimeout()

![browser-analogy](https://drive.google.com/uc?export=view&id=1BKTl3hD1MAWFfIVCBkfFbsu2RGnVar94)


Examples of browser vulnerabilities:
* Google Chrome
    * CVE-2019-5795 https://nvd.nist.gov/vuln/detail/CVE-2019-5795
* Mozilla Firefox 
    * CVE-2019-11716 https://nvd.nist.gov/vuln/detail/CVE-2019-11716


## DOM (Document Object Model)

The Document Object Model connects web pages to scripts or programming languages by representing the structure of a document—such as the HTML representing a web page—in memory. Usually, that means JavaScript, although modeling HTML, SVG, or XML documents as objects are not part of the core JavaScript language, as such.

Object-oriented interface used to read and write docs
* Web page in HTML in structured data
* DOM provides representation of this hierarchy

The DOM represents a document with a logical tree. Each branch of the tree ends in a node, and each node contains objects. DOM methods allow programmatic access to the tree. With them, you can change the document's structure, style, or content.

Nodes can also have event handlers attached to them. Once an event is triggered, the event handlers get executed. DOM (Document Object Model) - is an ‘application programming interface’. Use the DOM when we interact with web pages.
* Add content to a HTML document
* Delete content from a HTML document
* Change Content on a HTML document

Every element within your document is an object: <head> tag, <body> tag, etc. are objects etc.  Javascript - we can call methods on objects, we can call properties on objects in order to change the objects.

![DOM](https://drive.google.com/uc?export=view&id=1vXTZt-mJEM5rDUYjNLUflKWBZMCBOi9Y)

We can introduce nodes - all objects are nodes. We can change the nodes, we can interact with them, create Animations, validations, etc.

The Document interface represents any web page loaded in the browser and serves as an entry point into the web page's content, which is the DOM tree. The DOM tree includes elements such as <body> and <table>, among many others. It provides functionality globally to the document, like how to obtain the page's URL and create new elements in the document.

**DOM**
* Object-oriented interface used to read and write docs
* Web page in HTML is structured data
* DOM provides representation of this hierarchy

**Examples**
* Properties: document.alinkColor, document.URL, document.forms[ ], document.links[], document.anchors[ ]
* Methods: document.write(document.referrer)

**Includes Browser Object Model (BOM)**
* window, document, frames[], history, location, navigator (type
and version of browser)

## MIME (Multipurpose Internet Mail Extensions)

MIME is a specification for the format of non-text e-mail attachments that allows the attachment to be sent over the Internet. MIME allows your mail client or Web browser to send and receive things like spreadsheets and audio, video and graphics files via Internet mail.  By default, many web servers are configured to report a MIME type of text/plain or application/octet-stream for unknown content types. As new content types are invented or added to web servers, web administrators may fail to add the new MIME types to their web server's configuration. This is a major source of problems for users of Gecko-based browsers, which respect the MIME types as reported by web servers and web applications.

**MIME Sniffing** - The browser will often not just look at the Content-Type header that the server is passing, but also the contents of the page. If it looks enough like HTML, it’ll be parsed as HTML. => This led to IE 6/7-era bugs where image and text files containing HTML tags would execute as HTML (not so common anymore) - history

**Encoding Sniffing** - the encoding used on a document will be sniffed by browsers. If you don’t specify an encoding for an HTML document, the browser will apply heuristics to determine it. If you are able to control the way the browser decodes text, you may be able to alter the parsing.

## Security Mechanism

![BrowserSecurityMechanism](https://drive.google.com/uc?export=view&id=1R-Q0SmpiS0ulbkcT7V3cq4dOR47EkjnZ)

![ComponentsBrowserSecurityPolicy](https://drive.google.com/uc?export=view&id=1L6qROHKPMnUay-TfhDev5jFUIMUTQBiv)

**Same-Origin Policy **
* backbone of web security today
* is how the browser restricts a number of security-critical features:
    * What domains you can contact via XMLHttpRequest
    * Access to the DOM across separate frames/windows

## Isolation - Frames, HTML Sandboxing

### Frame and iFrame
Windows may contain frames from different sources
* Frame: rigid division as part of frameset
* iFrame: floating inline frame

iFrame example:

```
<iframe src="simple_iframe.html" width=450 height=100>
if you can see this, you browser doesn't understand IFRAME.
</iframe>
```

Why use frames?
* Delegate screen area to content from another source
* Browser provides isolation based on frames
* Parent may work even if frame is broken

In order to play a little bit with iframes follow the next instructions: 
1. `user@hostname~$: sudo apt install nginx`
2. Change `index.html` file content with the above code
3. `user@hostname~$: sudo service nginx start`
4. Access the browser as http://localhost
5. Solve the problem in order to see the iframe 

### HTML Sandboxing

The sandbox attribute enables an extra set of restrictions for the content in the iframe.

When the sandbox attribute is present, and it will:

* treat the content as being from a unique origin
* block form submission
* block script execution
* disable APIs
* prevent links from targeting other browsing contexts
* prevent content from using plugins (through <embed>, <object>, <applet>, or other)
* prevent the content to navigate its top-level browsing context
* block automatically triggered features (such as automatically playing a video or automatically focusing a form control)

Add the below HTML code in the same index.html as above:

```
<iframe src="sandbox_iframe.html" sandbox width=450 height=100>
if you can see this, you browser doesn't understand SANDBOX IFRAME.
</iframe>
```

Access the page via browser http://localhost.

The value of the sandbox attribute can either be just sandbox (then all restrictions are applied), or a space-separated list of pre-defined values that will REMOVE the particular restrictions


### Talking to web sites

Let's go through the basics of how HTTP requests are made, using telnet to form requests. First, let's connect to the vulnerable web server:

```
user@hostname~#: telnet 141.85.224.157 80
```

Now let's issue a simple GET. The request is composed of:

* GET <path> <http-version>
* followed by other header contents
* followed by an additional newline, indicating the end of the request.

_Please note the above bullet points and the fact that you need to provide an additional newline to indicate the end of the request._

GET / HTTP/1.0

HEAD / HTTP/1.0

POST / HTTP/1.0

The server's response contains:

* A status code (200 OK in our case)
* Date information and information about the server
* Encoding and other info about the data, i.e. it's MIME-type
* The length of the data
* The actual data

# Exercises

**[1]** The below image represents a snippet with DevTools containing information about a web application. What can you discover in the next image ? Is there any useful information from a security point of view ? Write the answer to the instructor.

![inspect-element](https://drive.google.com/uc?export=view&id=17xxCWiNyMQtCec5tRYU-lNOk4vwr9EUV)

https://imgur.com/a/47j3r5Y

**[2]** [Cockroach](https://sss-ctf.security.cs.pub.ro/challenges?category=web-sessions)  
**[3]** [Gimme](https://sss-ctf.security.cs.pub.ro/challenges?category=web-sessions)  
**[4]** [Surprise](https://sss-ctf.security.cs.pub.ro/challenges?category=web-sessions)  
**[5]** [My Special Name](https://sss-ctf.security.cs.pub.ro/challenges?category=web-sessions)  
**[6]** [Lame Login](https://sss-ctf.security.cs.pub.ro/challenges?category=web-sessions)  
**[7++]** You can play with other challenges on the same platform [here](https://sss-ctf.security.cs.pub.ro/challenges?category=web-sessions)  
