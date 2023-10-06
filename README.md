# Patterns_and_flags
Week 2 Files, Patterns and Flags. 
Day1 File Objects. 

The File object in JavaScript is part of the File API, which allows web applications to interact with files on the user’s local system. 
It represents a file that the user has selected through an HTML file input element (<input type=” file”>). 
The file object contains information about the selected file, such as its name, size, type, and last modification. 
A File objects inherits from Blob and is extended with filesystem related capabilities. 
There are two ways to obtain it: 
1.	A constructor. 
2.	New File (file Parts, Filename, [options]) 
 
fileParts - is an array of Blob/BlufferSource/String values. 
FileName - file name string. 
Options – optional object: 
lastModified -the timestamp (integer date) of last modification. 
 
The file object is particularly useful in scenarios where you want to allow users to upload files to a web application. It enables you to access information about the uploaded files and perform operations om them, such as reading their content, uploading them to a server, or manipulating them using JavaScript.  
Second, more often we get a file from<input type= “file”> or drag ‘n’ drop or the other browser interfaces. In that case, the file gets information from OS. 
As file inherits from Blob, file objects have the same properties, plus: 
Name -the file name. 
lastModified – the timestamp of last modification. 
That’s  how we get a file object from<input type=”file”>: 
 
File reader. 
A file reader is an object with the sole purpose of reading data from blob(and hence File too) objects. 
It delivers the data using events, as reading from disk may take time. 
The choice of read method depends on which format we prefer, how we are going to use the data. 
•	readAsArrayBuffer – for binary files, to do low level binary operations. 
For high-level operations, like slicing, file inherits from Blob, so we can call them directly, without reading. 
•	readAsText – for text files, when we’d like to get a string. 
•	ReadAsDataURL – when we’d like to use this data in src for img or another tag. 
As the reading proceeds, there are events: 
•	Loadstart – loading started. 
•	Progress – occurs during reading. 
•	Load – no errors, reading complete. 
•	Abort – abort() called. 
•	Error – error has occurred. 
•	Loadend – reading finished with either success or failure. 

When the reading is finished, we can access the results as: 
•	Reader.result is the result (if successful). 
•	Reader.error is the error (if failed). 

FETCH.
fetch is a built-in function that allows you to make HTTP requests to a specified resource, typically a URL.
It is used to retrieve data from a server or send data to a server in a web application.
Here's a breakdown of how it works:
fetch(url) initiates a request to the specified url.
It returns a Promise that resolves to a Response object. This object contains information about the response, including headers and the response body.
If the request is successful and the server responds with a status code in the 200 range, the promise is fulfilled and you can handle the response in the .then() block.
If there is an error (e.g., network issues, server error, etc.), the promise will be rejected and you can handle the error in the .catch() block.
It's important to note that fetch will not reject the promise on HTTP error status codes (like 404 or 500). It will only reject if there's a network error or other reason the request couldn't be fulfilled.
The basic syntax is:
let promise = fetch(url, [options])
url – the URL to access.
options – optional parameters: method, headers etc.
The browser starts the request right away and returns a promise.
Getting a response is usually a two-stage process.
First, the promise resolves with an object of the built-in Response class as soon as the server responds with headers.
So we can check HTTP status, to see whether it is successful or not, check headers, but don’t have the body yet.
The promise rejects if the fetch was unable to make HTTP-request, e.g. network problems, or there’s no such site. HTTP-errors, even such as 404 or 500, are considered a normal flow.



Post Requests.
A POST request is one of the HTTP methods used to send data to a server. 
It is commonly used when you want to submit form data or send information in the body od a request to be processed by a server.
A POST request is used to create or update resources on the server. 
When you make a POST request, you typically include data in the request body, which the server can then process and use.
Here’s an example of how you can link a fetch and a POST request together:
1.	You can use the fetch API TO SEND A post request to a server.
This involves using the method:
‘POST’ option in the fetch call and providing the appropriate data in the body parameter.
Explanation:
1.	postData is an example of the data you want to send to the server. 
2.	The fetch function is used to make a POST request the url/link.
3.	The body parameter contains the data you want to send to the server.
4.	The server processes the request, and if it responds with JSON data, we use .json() to parse the response.
5.	The first .then() handles the successful response from the server.
6.	If there any erros, they are caught in the .catch() block.

To make a POST request, or a request with another method, we need to use fetch options:
•	Method- HTTP-method, e.g. POST,
•	Body- one of:
o	A string (e.g. JSON),
o	FormData object, to submit the data as form/multipart,
o	Blob/BlufferSource to send binary data,
o	URLSearchParams, to submit the data in x-www-form-urlencoded encoding, rarely used.

Sending an image.
We can also submit binary data directly using Blob or BufferSource.
Response properties:
1. response.status – HTTP code of the response,
2. response.ok – true is the status is 200-299.
3. response.headers – Map-like object with HTTP 
    headers.

Methods to get response body:
1. response.json() – parse the response as JSON object,
2. response.text() – return the response as text,
3. response.formData() – return the response as.
4. FormData object (form/multipart encoding, see the 
     next chapter),
5. response.blob() – return the response as Blob(binary 
    data with type),
6. response.arrayBuffer() – return the response as 7. 
     ArrayBuffer (pure binary data),

Fetch options so far:
1. method – HTTP-method,
2. headers – an object with request headers (not any 
     header is allowed),
3. body – string, FormData, BufferSource, Blob or 
    UrlSearchParams object to send.

Sending a simple form.
HTML Form: You start with an HTML form. 
This form contains various input fields (like text fields, checkboxes, etc.) and a submit button.
JavaScript to Handle Form Submission:
 You use JavaScript to handle what happens when the form is submitted. 
This involves using an event listener to listen for the form's submission event, preventing the default behaviour (which is to reload the page), and then doing something with the form data.


In this JavaScript code:
1. document.getElementById('myForm') selects the form with the id "myForm".
2. We add an event listener for the form's submit event.
3. When the form is submitted, event.preventDefault() prevents the default form submission      (which would reload the page).
4. We then retrieve the values of the name and email fields.
5. You can now use these values to do something with the data, like sending it to a server (via AJAX) or performing client-side processing.
FormData Methods.
FormData is a built-in JavaScript object that provides an easy way to construct a set of key/value pairs representing form fields and their values.
Its commonly used in conjunction with HTML forms to send data to a server via AJAX or fetch API.
FormData object is a common way to create a bundle of data to send to the server using XMLHttpRequest or fetch.
It replicates the functionality of the HTML form element. We can think of it as an array of arrays. There is one array for each element that we want to send to the server.
The FormData interface provides a way to construct a set of key/value pairs representing form fields and their values, which can be sent using the fetch() , XMLHttpRequest.send() or navigator.sendBeacon() methods. 
It uses the same format a form would use if the encoding type were set to "multipart/form-data."

FormData provides several methods to work with the form data:
1.	FormData.append(name, value): This method appends a new value onto an existing key.
2.	FormData.delete(name): This method allows you to remove the value associated with a specific key from a FormData object.
3.	FormData.entries(): This method returns an iterator that allows you to loop through all key/values pairs contained in the FormData object.
4.	FormData.get(name): This method retrieves the first value associated with a given key from within a FormData object.
5.	FormData.getAll(name): This method retrieves all the values associated with aa given key from within a FormData object and returns them as an array.
6.	FormData.has(name): This method retuns a Boolean indicating whether a FormData object contains a certain key.
7.	FormData.set(name, value): This method sets a new value for an existing key inside a FormData object, or adds the key if it does not already exist.
Sending form with a File.
1.	HTML Form Setup:
•	Create an html form that includes a file input field.
•	The enctype=” multipart/form-data” attribute is crucial for forms that include file uploads. It specifies how the form data should be encoded before sending it to the server.
•	The <input type= “file”> element allows users to select files from their local device.

2.	JavaScript to Handle Form Submission:
•	When the form is submitted, it prevents the defaulter behavio(Which would reload the page).
•	It then creates a FormDate object using new FormDate(this): This collects all the form fields, including the file, into a data structure that can be sent via an HTTP request.
•	Next, it uses Fetch(or you can use XMLHttpRequest) to send an AJAX POST request to the server. Replace ‘https://example.com/upload’ with the actual URL where you want to send the file.
•	The server is expected to handle the file upload. Once the response is received, it can be processed accordingly.
Sending a form with a Blob Data.
Sending a form with Blob data refers to the process of submitting a web form that includes binary large object (Blob) data.
Blobs are used to store binary data in a format that is easily readable by computers, such as images, audio files, or other multimedia.
FormData objects are used to capture HTML form and submit it using fetch or another network method.
We can either create new FormData(form) from an HTML form, or create an empty object, and then append fields with methods:
1.	formData.append(name, value)
2.	formData.append(name, blob, fileName)
3.	formData.set(name, value)
4.	formData.set(name, blob, fileName).



Two peculiarities here:
The set method removes fields with the same name, append doesn’t.
To send a file, 3-argument syntax is needed, the last argument is a file name, that normally is taken from user filesystem for <input type="file">.
Other methods are:
1.	formData.delete(name)
2.	formData.get(name)
3.	formData.has(name).


Using Forms.
Forms are a fundamental part of web applications as they allow users to input data, submit it to a server, and perform various actions based on user interactions. 
JavaScript can be used to enhance the functionality and interactivity of forms in several ways. 
Here's how it works:
1.	 HTML Form Structure:
•	First, you need to create an HTML form within your web page. 
•	A form is typically defined using the <form> element.
•	It contains various form controls like text inputs, radio buttons, checkboxes, and buttons.
•	Each form control should have a unique name or ID to access it via JavaScript.
2.	Accessing Form Elements:
•	JavaScript can be used to access form elements by their names or IDs. 
•	This allows you to retrieve the user's input and manipulate form elements dynamically.
•	 You can use methods like document.getElementById() or document.querySelector() to access form controls.

3.	Handling Form Submission:
You can use JavaScript to intercept the form submission process and perform actions before the form is submitted to the server. This is often done using the submit event.


Simple Requests.
There are two types of cross-domain requests:
1.	Simple requests.
All the others.
Simple Requests are, well, simpler to make, so let’s start with them.
A simple request is a request that satisfies two conditions:
Simple method: GET, POST or HEAD
Simple headers – the only allowed custom headers are:
•	Accept,
•	Accept-Language,
•	Content-Language,
•	Content-Type with the value application/x-www-form-urlencoded, multipart/form-data or text/plain.

Any other request is considered “non-simple”. For instance, a request with PUT method or with an API-Key HTTP-header does not fit the limitations.
The essential difference is that a “simple request” can be made with a <form> or a <script>, without any special methods.
So, even a very old server should be ready to accept a simple request.
Contrary to that, requests with non-standard headers or e.g. method DELETE can’t be created this way. For a long time, JavaScript was unable to do such requests. So an old server may assume that such requests come from a privileged source, “because a webpage is unable to send them”.
When we try to make a non-simple request, the browser sends a special “preflight” request that asks the server – does it agree to accept such cross-origin requests, or not?
And, unless the server explicitly confirms that with headers, a non-simple request is not sent.
Now we’ll go into details. All of them serve a single purpose – to ensure that new cross-origin capabilities are only accessible with explicit permission from the server.
A "simple request" is a term used in the context of the Cross-Origin Request Sharing (CORS) policy in web development. 
CORS is a security feature implemented by web browsers to control and restrict cross-origin HTTP requests, which are requests made from one domain (origin) to a different domain. 
Simple requests are a category of cross-origin requests that have certain characteristics and are subject to less stringent security restrictions compared to "preflight requests."

CORS for Simple Request.
If a request is cross-origin, the browser always adds Origin header to it.
For instance, if we request https://anywhere.com/request from https://javascript.info/page, the headers will be like:
GET /request
Host: anywhere.com
Origin: https://javascript.info
As you can see, Origin contains exactly the origin (domain/protocol/port), without a path.
The server can inspect the Origin and, if it agrees to accept such a request, adds a special header Access-Control-Allow-Origin to the response. That header should contain the allowed origin (in our case https://javascript.info), or a star *. Then the response is successful, otherwise an error.
The browser plays the role of a trusted mediator here:
It ensures that the correct Origin is sent with a cross-domain request.
If checks for correct Access-Control-Allow-Origin in the response, if it is so, then JavaScript access, otherwise forbids with an error.
CORS, or Cross-Origin Resource Sharing, is a security feature implemented by web browsers to control and manage cross-origin HTTP requests made by web pages written in JavaScript. 
CORS is important because it helps prevent potentially malicious web pages from making unauthorized requests to a different domain (origin) on behalf of a user.
CORS specifically deals with cross-origin requests made from web pages, including simple requests.
Simple requests, as mentioned earlier, are a subset of cross-origin requests that meet specific criteria, including using HTTP methods like GET, HEAD, or POST with certain headers.
They are considered less risky compared to other types of requests, like those with custom HTTP methods or headers.
Here's how CORS works for simple requests in JavaScript and what it does:

Same-Origin Policy (SOP): By default, web browsers enforce the Same-Origin Policy (SOP), which restricts web pages from making requests to domains other than the one from which the web page was loaded. This policy is a fundamental security measure to protect users from potential security vulnerabilities.
CORS Headers: To enable cross-origin requests, the server that hosts the resources (e.g., an API) can include special HTTP response headers in its responses. These headers include:
Access-Control-Allow-Origin: This header specifies which origins (domains) are allowed to access the resources. For simple requests, this header often contains the origin of the requesting web page.
Access-Control-Allow-Methods: This header lists the HTTP methods (e.g., GET, POST) that are allowed when making requests to the resource.
Access-Control-Allow-Headers: This header specifies which HTTP headers are allowed in the request.
Access-Control-Allow-Credentials: If this header is set to true, it indicates that the browser can include credentials (e.g., cookies) in the request. Note that including credentials in cross-origin requests requires specific server configuration and additional precautions.
Browser Enforcement: When a JavaScript code in a web page attempts to make a cross-origin request (including a simple request), the browser checks for the presence of CORS headers in the server's response.
If the necessary CORS headers are present and permit the request, the browser allows the request to proceed. 
If the headers are missing or do not allow the request, the browser blocks the request and raises a security error.
Response Headers.
Response headers are an essential part of HTTP (Hypertext Transfer Protocol) responses sent by web servers when a client, such as a web browser or another application, requests a resource. These headers provide metadata and instructions to the client about how to handle the response and the resource it requested.
Response headers play a crucial role in the communication between web servers and clients, ensuring that resources are delivered correctly, securely, and efficiently. 
They provide essential information for browsers and other clients to interpret and handle HTTP responses appropriately.
Non-Simple Requests.
A "non-simple request" refers to an HTTP request that is not considered "simple" according to the rules defined in the Same-Origin Policy.
This policy is a security measure implemented by web browsers to prevent web pages from making requests to a different domain than the one the page came from, unless the target domain explicitly allows it.
A "simple request" is an HTTP request that meets certain criteria and does not trigger a preflight request.
 Simple requests include common HTTP methods like GET, HEAD, and POST, and they only use simple request headers (i.e., headers that are considered safe to be sent cross-origin without requiring a preflight request).
In contrast, a "non-simple request" includes requests that:

1.	Use methods other than GET, HEAD, or POST (e.g., PUT, DELETE).
2.	Include custom headers other than the simple request headers.
3.	Have a Content-Type other than application/x-www-form-urlencoded, multipart/form-data, or text/plain.
When a non-simple request is made, the browser sends a preflight request (an HTTP OPTIONS request) to the target server to ask for permission to make the actual request. 
The server responds with the appropriate headers indicating whether the request is allowed or not. If allowed, the actual request is then made.
The purpose of this mechanism is to prevent certain types of cross-origin requests that could pose security risks if not properly controlled. It helps protect user data and sensitive information from being accessed by malicious websites.
The specific function of a non-simple request is determined by the HTTP method used and the content of the request. For example, a non-simple request with the PUT method might be used to update data on a server, while a non-simple request with custom headers could be used for various purposes such as authentication or passing additional metadata. The exact behavior and handling of a non-simple request depends on how the server is configured to handle it.
Credentials.
Networking methods split cross-origin requests into two kinds: “simple” and all the others.
Simple requests must satisfy the following conditions:
1.	Method: GET, POST or HEAD.
2.	Headers – we can set only:
1.	Accept
2.	Accept-Language
3.	Content-Language
4.	Content-Type to the value application/x-www-form-urlencoded, multipart/form-data or text/plain.
The essential difference is that simple requests were doable since ancient times using <form> or <script> tags, while non-simple was impossible for browsers for a long time.
So, the practical difference is that simple requests are sent right away, with Origin header, but for other ones the browser makes a preliminary “preflight” request, asking for permission.
For simple requests:
1.	The browser sends Origin header with the origin.
2.	For requests without credentials (not sent default), the server should set:
1.	Access-Control-Allow-Origin to * or same value as Origin
3.	For requests with credentials, the server should set:
1.	Access-Control-Allow-Origin to the same value as Origin
2.	Access-Control-Allow-Credentials to true
Additionally, if JavaScript wants to access non-simple response headers:
1.	Cache-Control
2.	Content-Language
3.	Content-Type
4.	Expires
5.	Last-Modified
6.	Pragma
Then the server should list the allowed ones in Access-Control-Expose-Headers header.For non-simple requests, a preliminary “preflight” request is issued before the requested one:
1.	The browser sends OPTIONS request to the same URL, with headers:
1.	Access-Control-Request-Method has requested method.
2.	Access-Control-Request-Headers lists non-simple requested headers
2.	The server should respond with status 200 and headers:
1.	Access-Control-Allow-Methods with a list of allowed methods,
2.	Access-Control-Allow-Headers with a list of allowed headers,
3.	Access-Control-Max-Age with a number of seconds to cache permissions.
3.	Then the actual request is sent, the previous “simple” scheme is applied.


Fetch API
The Fetch API is a modern JavaScript interface for making network requests (such as HTTP requests). It provides a more powerful and flexible way to interact with web resources compared to older techniques like using XMLHttpRequest.
The main functions of the Fetch API are:
1.	Sending HTTP Requests: The Fetch API allows you to send HTTP requests to servers or other online resources. You can make requests using different HTTP methods like GET, POST, PUT, DELETE, etc.
2.	Handling Responses: It provides a clean way to handle the responses from these requests, including reading the response body and extracting relevant information.
3.	Working with Promises: The Fetch API is promise-based. This means it uses JavaScript Promises to handle asynchronous operations. This allows for more readable and maintainable asynchronous code.

The Fetch API also supports sending data in the body of a request, setting custom headers, and handling different response types (e.g., JSON, text, Blob, etc.).
Overall, the Fetch API provides a more modern and flexible way to interact with web resources, making it a cornerstone of modern web development.

Patterns and flags.
In the context of regular expressions, "patterns" and "flags" are two essential components:
Patterns:
1.	Pattern: A regular expression pattern is a sequence of characters that defines a search pattern. It's used to match or find strings within text based on a certain criteria or structure.
2.	Metacharacters: These are special characters in regular expressions that have a reserved meaning. For example, . matches any character, * matches zero or more occurrences of the preceding character, and | represents alternation.
3.	Character Classes: These are used to match specific sets of characters. For example, [0-9] matches any digit, and [a-zA-Z] matches any uppercase or lowercase letter.
4.	Quantifiers: These specify how many times a character or group of characters can occur. For example, * means zero or more occurrences, + means one or more occurrences, and ? means zero or one occurrence.

5.	Anchors: These are used to specify the position in the text where a match should occur. For example, ^ matches the start of a line, and $ matches the end of a line.

Flags:
1.	Flags: Flags are optional parameters that can be added to a regular expression to change its behavior. They are usually represented as a single letter after the closing delimiter of the regular expression.
2.	Global (g): When this flag is used, the regular expression will match all occurrences in the input string, rather than just the first one.
3.	Case Insensitive (i): This flag makes the regular expression case-insensitive, so it will match both uppercase and lowercase letters.
4.	Multiline (m): If this flag is set, ^ and $ will match the start and end of lines within a multi-line string, instead of just the start and end of the entire string.
5.	Dot All (s): This flag allows the dot (.) to match newline characters as well.
6.	Unicode (u): Enables full Unicode matching.
Usage.
"Usage" refers to the manner in which something is used or employed.
It encompasses how an object, tool, system, or concept is put into practice to achieve a specific purpose or goal.
To search inside a string, we can use method search.
Here’s an example:
let str = "I love JavaScript!"; // will search here 
let regexp = /love/;
alert( str.search(regexp) ); // 2
The str.search method looks for the pattern /love/ and returns the position inside the string. As we might guess, /love/is the simplest possible pattern. What it does is a simple substring search.
The code above is the same as:
let str = "I love JavaScript!"; // will search here
let substr = 'love';
alert( str.search(substr) ); // 2 
So searching for /love/ is the same as searching for "love".
But that’s only for now. Soon we’ll create more complex regular expressions with much more searching power.
Colors
From here on the color scheme is:
regexp – red
string (where we search) – blue
result – green
When to use new RegExp?
Normally we use the short syntax /.../. But it does not support variable insertions ${...}.
On the other hand, new RegExp allows to construct a pattern dynamically from a string, so it’s more flexible.
Here’s an example of a dynamically generated regexp:
let tag = prompt("Which tag you want to search?", "h2");
let regexp = new RegExp();
// finds <h2> by default
alert( "<h1> <h2> <h3>".search(regexp));
Flags.
In JavaScript, "flags" usually refer to the optional parameters that can be added to a regular expression. 
These flags modify the behaviour of the regular expression pattern during matching. Flags are represented as a single letter after the closing delimiter of the regular expression.
These flags provide additional control over how regular expressions are applied in JavaScript.
Here are the commonly used flags in JavaScript:
1. Global (g):
When the g flag is used, the regular expression will match all occurrences in the input string, rather than just the first one.
2. Case Insensitive (i):
This flag makes the regular expression case-insensitive, so it will match both uppercase and lowercase letters.
3. Multiline (m):
If this flag is set, ^ and $ will match the start and end of lines within a multi-line string, instead of just the start and end of the entire string.

4. Dot All (s):
This flag allows the dot (.) to match newline characters as well.
5. Unicode (u):
Enables full Unicode matching.
Methods of regexp and strings.
These methods provide powerful tools for working with strings and regular expressions in JavaScript. They are fundamental for tasks like pattern matching, data extraction, and text manipulation.
In JavaScript, both regular expressions (RegExp) and strings have a set of methods that allow you to work with them in various ways.
Methods of RegExp:
exec(str):
Searches for a match in a specified string. Returns an array of information about the match, or null if no match is found.
test(str):
Tests for a match in a string. Returns true if a match is found, false otherwise.
Methods of String:
match(regexp):
Searches the string for matches with a regular expression. Returns an array of matches or null if no matches are found.
split(separator):
Splits a string into an array of substrings based on a specified separator (which can be a regular expression).
toLowerCase() and toUpperCase():
Convert the string to all lowercase or all uppercase letters, respectively.
