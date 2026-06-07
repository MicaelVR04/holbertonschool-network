# What Happens When You Type https://www.google.com in Your Browser and Press Enter

When you type `https://www.google.com` into your browser and press Enter, a lot happens in a very short amount of time. The browser has to find the correct server, create a network connection, secure that connection, send the request, and receive the page that will be displayed on your screen.

This is the general flow.

## 1. The Browser Parses the URL

The browser first reads the URL:

```text
https://www.google.com
```

The `https` part tells the browser to use HTTPS, which is HTTP over an encrypted TLS/SSL connection. The hostname is `www.google.com`, and because no custom port is written in the URL, the browser uses port `443`, which is the default port for HTTPS traffic.

## 2. DNS Finds the IP Address

Computers do not use names like `www.google.com` to send packets across the internet. They use IP addresses. DNS, or Domain Name System, translates the domain name into an IP address.

The browser and operating system first check local caches. If the address is not cached, the computer asks a DNS resolver. The resolver may ask root DNS servers, top-level domain servers for `.com`, and authoritative DNS servers for `google.com`.

At the end of this process, the browser receives an IP address for `www.google.com`.

## 3. TCP/IP Creates a Connection

After the browser has the IP address, it opens a connection to the server using TCP/IP.

IP is responsible for addressing and routing packets between the client and the server. TCP is responsible for creating a reliable connection. TCP uses a three-way handshake:

```text
SYN
SYN-ACK
ACK
```

Once this handshake is complete, the browser and server can reliably exchange data.

## 4. Firewalls Inspect the Traffic

Before the request reaches the application infrastructure, it may pass through one or more firewalls. A firewall filters network traffic based on rules. For example, it may allow HTTPS traffic on port `443` but block unwanted traffic on other ports.

Firewalls help reduce the exposed attack surface of the infrastructure.

## 5. HTTPS/TLS Secures the Connection

Because the URL starts with `https`, the browser and server perform a TLS handshake. During this step, the server presents an SSL/TLS certificate that proves it is allowed to serve `www.google.com`.

The browser verifies the certificate. If it is valid, the browser and server agree on encryption keys. After that, the traffic is encrypted. This protects the request and response from being read or modified by someone between the browser and the server.

## 6. The Request Reaches a Load Balancer

Large websites like Google do not usually send all traffic to one server. A load balancer receives incoming traffic and distributes it across multiple backend servers.

The load balancer improves availability and performance. If one backend server is overloaded or unhealthy, traffic can be sent to another healthy server.

## 7. The Web Server Handles the HTTP Request

The request is then sent to a web server. A web server, such as Nginx or Apache, handles HTTP requests and responses.

The web server may serve static files directly, such as images, CSS, or JavaScript. If the request needs dynamic content, the web server forwards it to an application server.

## 8. The Application Server Runs the Logic

The application server runs the website's backend code. It decides what response should be generated.

For example, it may check user information, generate personalized content, or call other internal services. If it needs stored data, it asks a database.

## 9. The Database Provides Data

The database stores structured information. The application server may request data from the database, such as account information, page content, settings, or other records.

The database returns the requested data to the application server, and the application server uses it to build the response.

## 10. The Response Comes Back to the Browser

After the response is generated, it travels back through the web server, the load balancer, the firewall, and the encrypted TCP connection to the browser.

The browser receives the HTML, CSS, JavaScript, images, and other resources needed to display the page. It parses the HTML, builds the DOM, applies CSS, runs JavaScript, and renders the final page on the screen.

## Summary

Typing `https://www.google.com` and pressing Enter starts a chain of systems working together:

```text
Browser -> DNS -> TCP/IP -> Firewall -> HTTPS/TLS -> Load Balancer -> Web Server -> Application Server -> Database
```

Each layer has a role. DNS finds the server, TCP/IP transports the data, HTTPS encrypts it, firewalls filter it, load balancers distribute it, web servers receive it, application servers process it, and databases provide stored information.

All of this usually happens in less than a second.
