# JavaScript_intermediate_week1
Introduction to Intermediate JavaScript
Week 0
Frames and windows 
Popups and window methods
•	Popup window is one of the oldest methods to show the additional documents to user.
Example 
Basically, you just run:
window.open('https://javascript.info/') this will open  new window with a given URL.

•	The initial idea was to show another content without closing the main window.
•	there are other ways to do that: we can load content dynamically with fetch and show it in a dynamically generated <div>. So, popups are not something we use every day.
•	Also, popups are tricky on mobile devices, that don’t show multiple windows simultaneously.
•	Still, there are tasks where popups are still used, e.g. for OAuth authorization (login with Google/Facebook/…), because:
1.	A popup is a separate window with its own independent JavaScript environment so opening a popup with third part nontrusted site is safe.
2.	Its very easy to open popup.
3.	A popup can navigate (change URL) and send massages to opener windows. 
 
Activity 1 - Popup Blocking
•	In the past, evil sites abused popups a lot, a bad page could open tons of popups window wit ads. So now most browsers tr to block popups and protect the user. 
•	Most browsers block popups if they ae called outside of use-triggered event handlers lie onclick.
For example
Direct Window Opening:
In this scenario, a popup window is being opened directly when the code is executed. The behaviour of this code depends on the browser's popup blocking settings. If the browser allows popups for the website 'https://javascript.info', the window will open. If the browser blocks popups for that website or in general, it may show a notification indicating that the popup was blocked.
// popup blocked
window.open('https://javascript.info');
Window Opening Triggered by a Button Click:
In this scenario, a popup window is opened when a button with the id button is clicked. The window.open() function is called in response to the button click event. This is a common way to handle popups, as it allows users to trigger the popup intentionally rather than it happening automatically.
Again, whether the popup is blocked or allowed depends on the browser's settings and whether the user has configured their browser to allow popups from the website 'https://javascript.info'.
// popup allowed
button.onclick = () => {
  window.open('https://javascript.info');
};

window.open
•	The syntax to open a popup is: windw.open(url,name,params).
Window features:
•	menubar (yes/no) – shows or hides the browser menu on the new window.
•	toolbar (yes/no) – shows or hides the browser navigation bar (back, forward, reload etc) on the new window.
•	location (yes/no) – shows or hides the URL field in the new window. FF and IE don’t allow to hide it by default.
•	status (yes/no) – shows or hides the status bar. Again, most browsers force it to show.
•	resizable (yes/no) – allows to disable the resize for the new window. Not recommended.
•	scrollbars (yes/no) – allows to disable the scrollbars for the new window. Not recommended.


A minimalistic Window
•	this refers to a small and basic window or pop-up that you can crate and control using JavaScript code.
•	This window typically has very few features and is often used for specific purposes, such as showing alerts, messages, or simple user interfaces.
Below are the key points to understanding about a minimalist window in JavaScript. 
•	Small and basic, it’s a tiny window that doesn’t have all the bells and whistles of a regular web browser window, it can be resized, doesn’t have many buttons. 
•	Controlled with JavaScript: You use JavaScript code to create, open, and manipulate this window. For example, you can decide when it opens and closes, what it displays, and its size and position on the screen.

•	Common Uses: Minimalist windows are often used for simple tasks like showing alert messages to users, displaying login or registration forms, or presenting small interactive elements like a calculator.
•	Limited Functionality: They are not meant for complex web applications but rather for specific, straightforward tasks where a minimal interface is sufficient.
Below is an example of a minimalistic window in JavaScript.
// Create a minimalist window with a simple message
var myWindow = window.open('', 'Minimalist Window', 'width=300,height=200');

// Add content to the window (in this case, a message)
myWindow.document.write('<p>Hello, this is a minimalist window!</p>');

// Close the window after a few seconds
setTimeout(function() {
  myWindow.close();
}, 5000); // This closes the window after 5 seconds (5000 milliseconds)

Accessing popup from window
•	Accessing a popup from a window in JavaScript means that you want to interact with or control a small, additional window that has been opened by your main web page. Here's some basic information about it.
•	Opening a Popup: You can use JavaScript to open a small new window or popup from your main web page. This new window can display a different webpage or some specific content.
•	
•	Accessing the Popup: After opening the popup, you can use JavaScript to interact with it. This includes things like changing its content, resizing it, moving it, or even closing it.
•	
•	Communication: You can also use JavaScript to send and receive information between the main window and the popup. This allows you to pass data or messages back and forth.
•	
•	Use Cases: Popups are commonly used for various purposes, like showing login forms, displaying additional information, or confirming actions (like "Are you sure you want to delete this?").
•	
•	Security Considerations: Be cautious with popups, as they can sometimes be misused for malicious purposes. Most modern web browsers have built-in popup blockers to protect users from unwanted or harmful popups.

Accessing popup from window.  

Closing a popup
•	To close a window, win.close()
•	To check if a window is closed win.closed.
 

Scrolling a window.
•	Scroll the window x pixels right and y down lative the current scroll.

 
Focus/Blur on a window
•	Theoretically, there are window.focus() and window.blur() methods to focus/unfocus on a window. And there are also focus/blur events that allow to catch the moment when the visitor focuses on a window and switches elsewhere.
•	Although, in practice they are severely limited, because in the past evil pages abused them.
•	For instance, look at this code:
•	window.onblur = () => window.focus();
•	When a user attempts to switch out of the window (window.onblur), it brings the window back into focus. The intention is to “lock” the user within the window.
•	So browsers had to introduce many limitations to forbid the code like that and protect the user from ads and evils pages. They depend on the browser.
•	For instance, a mobile browser usually ignores window.focus() completely. Also focusing doesn’t work when a popup opens in a separate tab rather than a new window.
•	Still, there are some use cases when such calls do work and can be useful.
•	For instance:
•	When we open a popup, it might be a good idea to run newWindow.focus() on it. Just in case, for some OS/browser combinations it ensures that the user is in the new window now.
•	If we want to track when a visitor actually uses our web-app, we can track window.onfocus/onblur. That allows us to suspend/resume in-page activities, animations etc. But please note that the blur event means that the visitor switched out from the window, but they still may observe it. The window is in the background, but still may be visible.


Introduction to Day 2
Cross window communication
Same origin.
•	Two URLs are said to have same origin if they have same protocol, domain, and port.
Below is URLs that shares the same origin.
•	http://site.com
•	http://site.com/
•	http://site.com/my/page.html
These ones do not share the same origin.
•	http://www.site.com (another domain: www.matters)
•	http://site.org (another domain: .orgmatters)
•	https://site.com (another protocol: https)
•	http://site.com:8080 (another port: 8080)

In action: iframe
•	An <iframe> tag hosts a separate embedded window, with its own separate document and window objects.
We can access them using properties:
o	iframe.contentWindow to get the window inside the <iframe>.
o	iframe.contentDocument to get the document inside the <iframe>, короткий аналог iframe.contentWindow.document.
When we access something inside the embedded window, the browser checks if the iframe has the same origin. If that’s not so then the access is denied (writing to location is an exception, it’s still permitted).
For instance, let’s try reading and writing to <iframe>from another origin:
 

•	An iframe in JavaScipt is like window or frame inside a webpage.
•	It’s away to show another webpage or content from a different source right within the main webpage.
Here's how it works:
•	Embedding Content: With JavaScript, you can create an iframe element on your webpage. Think of it as a special area on your page that can display a completely different webpage or content from elsewhere on the internet.
•	Showing External Websites: You can use an iframe to display content from other websites. For example, you might want to show a YouTube video, a Google Map, or a Twitter feed directly on your webpage. You just need to specify the URL of that content in the iframe.
•	Keeping Things Separate: The cool thing about iframes is that they keep the content inside them separate from the main webpage. This means that the styles and scripts on the external webpage won't interfere with the main page, and vice versa.
•	Interactive Elements: You can interact with the content inside the iframe using JavaScript. For example, you can make buttons or links that change what's displayed inside the iframe or communicate with it in other ways.
•	Use Cases: Iframes are commonly used for embedding videos, maps, social media feeds, or even entire web applications within a webpage. They are a way to bring external content into your site seamlessly.
•	think of an iframe to bring content from other websites or sources into your webpage, creating a kind of "window" to display that content without leaving your site. It's a versatile tool for enhancing the functionality and richness of your webpages.
Window on subdomains.document.domain in JavaScript.
JavaScript and how it relates to windows on subdomains in simple terms:
Windows on Subdomains:
•	 When we talk about "windows" in web development, we're referring to browser windows or tabs that display web pages. Subdomains are parts of a website's address that come before the main domain. For example, "blog.example.com" is a subdomain of "example.com."
document.domain:
•	 In JavaScript, document.domain is a property that allows web pages on different subdomains of the same main domain to communicate with each other, even though browsers typically have a security policy that prevents such communication.
Simple Explanation:
•	Imagine you have a main website at "example.com" and a separate blog at "blog.example.com." Normally, web pages on "example.com" can't directly interact with pages on "blog.example.com" due to security restrictions. However, by setting document.domain to the same value in both pages (in this case, "example.com"), you're telling the browser to relax its security rules and allow these pages to talk to each other.
Use Cases:
•	Sharing data: You can use document.domain to share information, variables, or functions between web pages on subdomains, making it easier to create integrated features.
•	Cross-origin communication: It's a way to work around the browser's same-origin policy, which restricts communication between different domains.
Security Note:
•	Be cautious when using document.domain because it can potentially introduce security risks. Only use it when you have full control over the subdomains involved and trust them. Misusing it can open up security vulnerabilities.
•	In simple terms, document.domain in JavaScript is a way to make web pages on different subdomains of the same website talk to each other, so they can share information and work together more closely. It's like opening a window between different parts of your own website, but you should be careful with it to ensure security.
Iframe: wrong document pitfall
•	When an iframe comes from the same origin and we access its documents there’s a pitfall.
•	An Iframe immediately has a document but documents is different from the one that loads into it.
•	 
•	Imagine you have a web page (let's call it Page A), and within that page, you have a little window that shows another web page (let's call it Page B). This little window is called an "iframe."
•	Now, the "Iframe: wrong document" pitfall happens when you try to make Page A and Page B talk to each other using JavaScript, but they can't because they belong to different "documents."
•	In simpler words, it's like trying to have a conversation between two people who are in separate rooms, and they can't hear each other because they're in different places.
•	JavaScript on Page A can't easily interact with JavaScript on Page B if they are in separate iframes because they are treated as different documents by the web browser for security reasons. This can make it tricky to share information or make them work together smoothly.
•	To overcome this pitfall, you may need to use special techniques or messaging systems provided by JavaScript or the browser to allow communication between these iframes. It's like having a telephone line between those separate rooms so they can talk to each other even though they are in different places.
Collection: window.frames
•	in JavaScript is like a list of all the windows or frames that are inside a web page. It helps you access and control different parts of a webpage, especially if that webpage contains multiple sections or frames.
•	Imagine a webpage as a puzzle with several pieces. Each piece can be thought of as a frame. With window.frames, you can keep track of and interact with these individual puzzle pieces (frames) from the main puzzle (webpage).
For example, you can use window.frames to do things like:
•	Access content within a specific frame: You can reach inside a particular frame and read or modify its content.
•	Navigate between frames: You can move from one frame to another, almost like switching between different sections of a webpage.
•	Perform actions within frames: You can make something happen within a specific frame, like submitting a form or clicking a button.
•	So, window.frames is like a tool that helps you manage and work with the different parts of a webpage, especially when it's divided into separate frames.
The “sandbox” iframe attribute
•	Allows for the exclusion of certain actions inside an<iframe> in order to prevent it from executing untrusted code.
•	Its sandboxes the iframe by treating it as coming from another origin and /or applying other limitations.
•	There’s a “default set” of restrictions applied for <iframe sandbox src="...">. But it can be relaxed if we provide a space-separated list of restrictions that should not be applied as a value of the attribute, like this: <iframe sandbox="allow-forms allow-popups">.
•	an empty "sandbox" attribute puts the strictest limitations possible, but we can put a space-delimited list of those that we want to lift.
Below is a list of limitations.
allow-same-origin
•	By default "sandbox" forces the “different origin” policy for the iframe. In other words, it makes the browser to treat the iframe as coming from another origin, even if its src points to the same site. With all implied restrictions for scripts. This option removes that feature.

allow-top-navigation
•	Allows the iframe to change parent.location.

allow-forms
•	Allows to submit forms from iframe.

allow-scripts
•	Allows to run scripts from the iframe.

allow-popups
•	Allows to window.open popups from the iframe

javascriptinfo example

•	It demonstrates a sandboxed iframe with the default set of restrictions: <iframe sandbox src="...">. It has some JavaScript and a form.
The purpose of the "sandbox" attribute is only to add more restrictions. It cannot remove them. In particular, it can’t relax same-origin restrictions if the iframe comes from another origin.

Cross Window Messaging
•	Cross-window messaging in JavaScript is like sending notes between different browser windows or tabs.
•	 It's a way for web pages in one window to talk to web pages in another window, even if they're from different websites.
•	Imagine you have two browser tabs open, one showing a game and the other showing a chat application.
•	 Cross-window messaging allows the game to send a message to the chat application, like saying, "I won!" or "Let's chat!" This communication happens securely and helps different parts of a webpage or different webpages work together.
•	To do this, JavaScript provides a special feature called the "Window.postMessage()" method. It allows one window to send a message to another window, and the other window can listen for and respond to these messages.
•	This messaging system is like having a safe way for different parts of the web to talk to each other, making it possible to create interactive and connected web applications.


Day 3
Introduction to Clickjacking
•	Clickjacking is a sneaky trick used by some websites to make you click on things you didn't intend to click on.
•	 It's like when someone puts a transparent sheet over a picture and makes you think you're clicking on the picture, but you're actually clicking on something else.
•	In web terms, it works like this: An attacker creates a webpage with something interesting on it, like a button that says "Click Here for a Prize." But hidden underneath that button is another button, like "Transfer Money" on your online banking page.
•	When you click on the "Click Here for a Prize" button, you're actually clicking on the "Transfer Money" button from your banking page, and bad things can happen without your knowledge or consent. It's a way to trick you into doing something you didn't intend to do.
•	To protect against clickjacking, modern browsers have security measures in place. For example, they may not allow one website to overlay its content on top of another website. This prevents the hidden trickery that clickjacking relies on.
•	So, be cautious when clicking on things online, especially if they seem too good to be true. Browsers are working to keep you safe from clickjacking, but it's always a good idea to be mindful of where you're clicking.


•	To protect against clickjacking in your web applications, you can use a few techniques. 
•	One common approach is to set a Content-Security-Policy (CSP) header in your web server's response. 
•	This header tells the browser which domains are allowed to embed your site in an iframe.
•	In this example below in red, frame-ancestors 'self' tells the browser that only the same domain can embed this page in an iframe. 
•	It prevents other websites from framing your content and potentially engaging in clickjacking.
•	It's important to note that implementing CSP headers is just one aspect of a comprehensive security strategy. 
•	Other security practices like input validation, HTTPS usage, and secure coding practices should also be employed to protect your web application from various security threats, including clickjacking.

Here's an example of how you can set a CSP header in PHP:
<?php
header("Content-Security-Policy: frame-ancestors 'self'");
?>
<!DOCTYPE html>
<html>
<head>
    <title>Your Page</title>
</head>
<body>
    <!-- Your webpage content goes here -->
</body>
</html>

Old school defenses (weak)
•	The oldest defense is a bit of JavaScript which forbids opening the page in a frame (so-called “framebusting”).
•	Old-school or weak defenses in JavaScript refer to outdated or ineffective ways of protecting your code and data in web applications. 
•	These methods are no longer reliable because they are easy for attackers to bypass. 
Here are some examples:
•	Obscured Code: In the past, some developers tried to hide their JavaScript code by obfuscating it, making it difficult for humans to read. However, this doesn't stop determined attackers who can still reverse-engineer the code.
•	Client-Side Validation: Relying solely on client-side validation (checking data on the user's device) for security is weak. Attackers can manipulate or bypass this validation easily.
•	Hidden Fields: Using hidden form fields to store sensitive data is a weak practice. Malicious users can easily view or manipulate these fields using browser developer tools.
•	Security Through Obscurity: This means relying on the secrecy of your methods rather than using well-established security practices. It's weak because it assumes that attackers won't discover how your code works, which is not a safe assumption.
•	No HTTPS: Not using HTTPS for transmitting sensitive data is a significant weakness. Without HTTPS, data can be intercepted and tampered with during transit.
•	Weak Passwords: Allowing weak passwords in user accounts is an old-school defense. It makes your application vulnerable to brute force attacks.
•	These old-school defenses are considered weak because they are either easily circumvented by attackers or they don't provide adequate protection against modern security threats. To build secure web applications, it's essential to use up-to-date security practices and technologies. This includes server-side validation, HTTPS, strong passwords, and staying informed about current security best practices.
•	The oldest defence is a bit of JavaScript which forbids opening the page in a frame (so-called “framebusting”).
•	That looks like this:
if (top != window) {
  top.location = window.location;
}

X-Frame-Options
•	The server-side header X-Frame-Options can permit or forbid displaying the page inside a frame.
•	It must be sent exactly as HTTP-header: the browser will ignore it if found in HTML <meta> tag. So, <meta http-equiv="X-Frame-Options"...> won’t do anything.
•	The header may have 3 values:
DENY
•	Never ever show the page inside a frame.


SAMEORIGIN
•	Allow inside a frame if the parent document comes from the same origin.


ALLOW-FROM domain
•	Allow inside a frame if the parent document is from the given domain.
•	For instance, Twitter uses X-Frame-Options: SAMEORIGIN.

Here’s the result:
•	<iframe src="https://twitter.com"></iframe>

 

Samesite cookie attribute
•	Samesite cookie attribute can also prevent clickjacking attacks.
•	The Samesite cookie attribute is like a rule for cookies that websites use to remember you. It helps protect your privacy and security online.
•	Imagine cookies as small pieces of information that a website saves on your computer to remember things like your login status or what's in your shopping cart. Sometimes, other 
•	websites want to access these cookies to track you or do other things without your permission.
•	Samesite helps prevent this by saying that cookies can only be shared with the website they came from. It's like a bouncer at a party making sure that the snacks you brought are only shared with your friends and not with strangers.
There are three settings for Samesite:
•	"Strict" means cookies are only shared with the same website, no exceptions.
•	"Lax" allows some sharing with other websites, but only when you click on a link from the original website.
•	"None" allows cookies to be shared with any website, but it's not very secure, so it's used carefully.
•	In summary, the Samesite cookie attribute is a rule that helps protect your privacy by controlling how cookies are shared between websites. It's like a security guard for your online snacks.


Day 4
ArrayBuffer

•	An ArrayBuffer in JavaScript is like a special container for storing binary data, which means it can hold a bunch of 0s and 1s.
•	 It's a bit like a box where you can put different types of data, like numbers or text, but it's organized in a way that computers can understand well.
•	Here's a simple way to think about it: Imagine you have a box with a bunch of slots, and each slot can hold a 0 or a 1. You can use these 0s and 1s to represent all sorts of things, like numbers, letters, or even pictures, by arranging them in a specific order.
•	So, when you use an ArrayBuffer in JavaScript, you're basically getting this box where you can put binary data, and then you can work with that data in a very precise and efficient way. It's like having a special toolbox for dealing with binary information.
•	The basic binary object is ArrayBuffer – a reference to a fixed-length contiguous memory area.
We create it like this:
•	let buffer = new ArrayBuffer(16); // create a buffer of length 16

alert(buffer.byteLength); // 16

•	Uint8Array – treats each byte in ArrayBufferas a separate number, with possible values are from 0 to 255 (a byte is 8-bit, so it can hold only that much). Such value is called a “8-bit unsigned integer”.
•	Uint16Array – treats every 2 bytes as an integer, with possible values from 0 to 65535. That’s called a “16-bit unsigned integer”.
•	Uint32Array – treats every 4 bytes as an integer, with possible values from 0 to 4294967295. That’s called a “32-bit unsigned integer”.
•	Float64Array – treats every 8 bytes as a floating point number with possible values from 5.0x10-324to 1.8x10308.


examples of how you can use ArrayBuffer in JavaScript:
Example 1: Storing Numbers
// Create an ArrayBuffer with space for 4 bytes (32 bits)
const buffer = new ArrayBuffer(4);

// Create a view on the buffer to work with it
const view = new DataView(buffer);

// Store an integer (42) into the buffer
view.setInt32(0, 42);

// Retrieve the integer from the buffer
const storedValue = view.getInt32(0);

console.log(storedValue); // Output: 42

In this example, we create an ArrayBuffer to store binary data. We use a DataView to interact with the data inside the buffer. We store the number 42 as a 32-bit integer and then retrieve it from the buffer.

Example 2: Storing Text
// Create an ArrayBuffer with space for 10 characters (each character is 2 bytes)
const buffer = new ArrayBuffer(20);

// Create a view on the buffer to work with it
const view = new DataView(buffer);

// Store text "Hello" into the buffer
for (let i = 0; i < 5; i++) {
  view.setUint16(i * 2, "Hello".charCodeAt(i));
}

// Retrieve and decode the text from the buffer
let text = "";
for (let i = 0; i < 5; i++) {
  text += String.fromCharCode(view.getUint16(i * 2));
}

console.log(text); // Output: "Hello"



TypedArray
•	The common term for all these views (Uint8Array, Uint32Array, etc) is TypedArray. They share the same set of methods and properties.
•	A typed array constructor (be it Int8Array or Float64Array, doesn’t matter) behaves differently depending on argument types.
There are 5 variants of arguments:
•	new TypedArray(buffer, [byteOffset], [length]);
•	new TypedArray(object);
•	new TypedArray(typedArray);
•	new TypedArray(length);
•	new TypedArray();
Typed arrays are used by weGL,canvas, web Audio API, XMLHttpRequests, fetch API, WebSockets, web Workers, Media Sourse API and file API.
•	A TypedArray in JavaScript is like a special way to work with arrays, but it's mainly designed for handling binary data, like numbers, in a more efficient and precise manner.
•	Imagine a regular array as a container where you can put all sorts of things, like numbers, words, or even mix them up. 
•	But with a TypedArray, you decide in advance what kind of data it will hold, such as 32-bit integers or 16-bit floating-point numbers.
•	 It's like having different types of containers for specific types of things, making it easier for your computer to work with them quickly and accurately.
•	In simple terms, a TypedArray is a specialized array that's really good at handling specific types of data, especially binary data, in a more organized and optimized way. It's like using separate boxes for different kinds of objects to keep everything neat and tidy.
Out of bound Behaviour
•	In JavaScript, out-of-bound behavior refers to what happens when you try to access or modify an element in an array or a property of an object using an index or key that doesn't exist within the array or object.
Here's a simple explanation:
•	Imagine you have a row of boxes, each labeled with a number. These boxes represent the elements in an array or properties in an object.
•	 If you try to open or change the contents of a box that has a number that's not on any of the boxes, you'll either get an "undefined" result or an error. It's like trying to find a box labeled "7" when you only have boxes labeled from "1" to "5."
•	In JavaScript, this out-of-bound behavior can cause problems if you're not careful. You might get unexpected results, like "undefined" values, or your code could crash with an error. So, it's essential to make sure you're using valid indexes or keys when working with arrays and objects to avoid these issues.
•	
TypedArray methods
•	TypedArray methods in JavaScript are like special tools or actions you can use to work with arrays that contain specific types of data, like numbers, in a more efficient and precise way.
•	Think of these methods as actions you can perform on your array to do things like adding up all the numbers, finding the largest number, or changing the order of the elements.
•	For example, if you have a box full of numbers, you can use these methods to count, sort, or search for specific numbers in the box without having to check each number one by one.
•	So, TypedArray methods in JavaScript are like a set of handy tools that help you work with arrays of specific data types more easily and effectively. They allow you to perform common tasks on your data without writing lots of complex code from scratch.
•	There are two additional methods:
•	
•	arr.set(fromArr, [offset]) copies all elements from fromArr to the arr, starting at position offset (0 by default).
•	arr.subarray([begin, end]) creates a new view of the same type from begin to end (exclusive). That’s similar to slice method (that’s also supported), but doesn’t copy anything – just creates a new view, to operate on the given piece of data.
•	These methods allow us to copy typed arrays, mix them, create new arrays from existing ones, and so on.


DataView
•	In simple terms, DataView in JavaScript is like a special tool that helps you read and write binary data in a structured way. It's like having a magnifying glass to look closely at tiny details in a big picture.
•	Imagine you have a long string of ones and zeros, which represents various types of data like numbers or text. DataView allows you to pick out and work with specific parts of this string more easily. It helps you read and change the data accurately by knowing how many ones and zeros make up each piece of information.
•	So, DataView is like a tool that helps you manage and make sense of binary data, making it simpler to interact with and manipulate data in a format that computers can understand.
Example 1: Reading Data
•	Suppose you have a binary data buffer that contains a 32-bit integer (4 bytes) and you want to read that integer using DataView:
// Create an ArrayBuffer with binary data
const buffer = new ArrayBuffer(4);
const view = new DataView(buffer);
// Fill the buffer with binary data (e.g., the number 42)
view.setInt32(0, 42);
       // Read the integer from the DataView
const readValue = view.getInt32(0);
console.log(readValue); // Output: 42
Example 2: Writing Data
Now, let's say you want to write binary data into a buffer using DataView:
// Create an empty ArrayBuffer with space for a 16-bit integer (2 bytes)
const buffer = new ArrayBuffer(2);
const view = new DataView(buffer);

// Write a 16-bit integer (e.g., 100) into the buffer
view.setInt16(0, 100);

// Read the written integer from the DataView
const readValue = view.getInt16(0);

console.log(readValue); // Output: 100









