---
layout: post
title: "Essential cURL Commands for Developers"
author: andre
categories: [ bash ]
tags: [bash, curl, terminal]
image: /assets/images/feature-images/feature-image-bash.jpg
description: This post provides a quick reference to the cURL commands that I use as a Java developer. This is not a complete set of cURL commands with detailed explanations on what each command does.
comments: true
---

- Table of Contents
{:toc .large-only}

This post provides a quick reference to the cURL commands that I use as a Java developer. This is not a complete set of cURL commands with detailed explanations on what each command does. If you want to read detailed documentation on the different options and arguments of the cURL command, please refer to the *man* pages of the cURL command. 

Furthermore, there are a number of REST Clients and IDEs like Eclipse and IntelliJ that allows you to invoke HTTP requests to a server, however more than often I find myself having to make these calls from the command line as part of a debug process. It is also faster to open a terminal and use these commands to invoke commands than to setup the configuration for different types of requests in your IDE or other UI applications. 

Use this reference to learn the cURL command and add it as a critical tool as part of your skillset. 

## Help and Information Commands
To find help or learn more about the different options and arguements used as part of the curl command, you can type any of the following in the terminal.
```bash
# Display quick help information about the curl command
$ curl --help

# Quick search for specific curl options or arguments
$ curl --help | grep {search_value}

# Display the manual page for the curl command
$ man curl

# Displays information about curl and the libcurl version it uses.
$ curl --version
$ curl -V
```

## General
This section contains the basic curl commands on which you can add more options and arguments listed in the other sections.
```bash
# Retrieve content of URL and display it on screen
$ curl {URL}

# Write output to a file instead of stdout.
$ curl {URL} > {filename}
$ curl -o {filename} {URL}

#  Write output to a local file named like the remote file we get
$ curl -O {URL}

# Enables verbose detail to be displayed
$ curl -v {URL}

# Enables a full trace dump on all incoming and outgoing data.
$ curl --trace {filename} {URL}
 
# Silent Mode: Don’t show progress meter or error messages.
$ curl -s {URL}
```

## HTTP Headers
HTTP headers are the name or value pairs that are displayed in the request and response messages of message headers for Hypertext Transfer Protocol (HTTP). These commands will help you set and read the HTTP Headers.
```bash
# Fetch the headers from the server (HEAD)
$ curl -I {URL}

# Include the HTTP-header in the output
$ curl -i {URL}

# Pass multiple headers as part of the request to the server.
$ curl -H "{HTTP General Header}" -H "{HTTP Request Header}" {URL}

# Include custom HTTP Header in the request to the server.
$ curl -H "{X-Key}:{Value}" {URL}

# Write the received protocol headers to the specified file.
$ curl -D {filename} {URL}
```

## HTTP Cookies
An HTTP cookie is a small piece of data sent from a website and stored on the user's computer by the user's web browser while the user is browsing. These commands will help you set and read the HTTP Cookies.
```bash
# Write all cookies to filename after completed command.
$ curl -c {filename} {URL}

# Read cookies from file and pass data to HTTP Server in Cookie header. 
$ curl -b {filename} {URL}

# Read cookies from data (key:value) and pass to HTTP Server in Cookie header.
$ curl -b "{key1:value1;key2:value2}" {URL}

# Discard all "session cookies". New session started.
$ curl -j {URL}
```

## Proxy
A proxy server is a server that acts as an intermediary for requests from clients seeking resources from other servers. These commands will help set the proxy server URL and port number and also with authentication.
```bash
# Use the specified proxy server and port number
$ curl -x {proxy_url}:{port} {URL}

# Specify the user name and password to use for proxy authentication.
$ curl -U {username}:{password} - x {proxy_url}:{port} {URL}

# Comma-separated list of hosts which do not use a proxy
$ curl --noproxy {url1} -x {proxy_url}:{port} {URL}
```

## FTP Server
The File Transfer Protocol (FTP) is a standard network protocol used for the transfer of computer files between a client and server on a computer network. These commands will help to transfer files to and from a FTP Server.
```bash
# Display a directory listing of an FTP site (Anonymous)
$ curl {FTP_URL}

# Retrieve a file from a FTP site. (Anonymous)
$ curl {FTP_URL}/{filename} 

# Upload a file to a FTP site. (Anonymous)
$ curl -T {filename} {FTP_URL}

# Upload Files to an FTP Server. (Secured)
$ curl -u {ftpuser}:{ftppass} -T {filename} {FTP_URL}

# Upload multiple files to an FTP Server
$ curl -u {ftpuser}:{ftppass} -T "{file1,file2}" {FTP_URL}

# Upload a file to a FTP site and append to an existing file
$ curl -T {filename} -a {FTP_URL}/{filename}
```

## HTTP Post/Put Data
The HTTP POST and PUT request method requests that a web server accepts the data enclosed in the body of the request message, most likely for storing it. These commands will show you how to enclose data as part of a request.
```bash
# Send data in a POST/PUT request to the HTTP server
$ curl -d '{key1=value1&key2=value2}' -X {POST/PUT} {URL}

# Send data from a file in a POST/PUT request to the HTTP server
$ curl -d {@filename} -X {Post/PUT} {URL}
```

## REST API
A RESTful API is an application program interface (API) that uses HTTP requests to GET, PUT, POST and DELETE data. The following commands illustrate how to invoke REST APIs with different HTTP methods.
```bash
# Invoke REST API (GET & JSON)
$ curl -i -H "Content-Type: application/json" -X GET {REST_API}

# Invoke REST API (POST & JSON)
$ curl -i -H "Content-Type: application/json" -X POST -d '{key:value}' {REST_API}

# Invoke REST API (PUT & JSON)
$ curl -i -H "Content-Type: application/json" -X PUT -d '{key:value}' {REST_API}

# Invoke REST API (POST)
$ curl -X DELETE {REST_API}/{ID}
```

## Security
There are numerous ways to authenticate your curl commands against the server. Here are some of the ways to perform authentication.
```bash
# Authenticate with username and password
$ curl -u {username}:{password} {URL}

# Authenticate with SSL certificate and password
$ curl --cert {cert_file.pem}:{password} {URL}
```


## Configuration File
The curl configuration file is named .curlrc (Linux) or _curlrc (Windows) and can be found in the user's home directory.

An example of the file and the entries is as follows:
```bash
# The default Proxy and port to use
proxy = 127.0.0.1:8080
# The proxy username and password
proxy-user = "user:pass"
# The timeout is set to 60 seconds
-m 60
```

## Summary
The curl commands listed in this article is by no means a complete set of curl commands and only serve as a quick reference to be used by developers. To see the full documentation of the curl command, please read the *man* pages of the curl command.

Follow me on any of the different social media platforms and feel free to leave comments.

[1]:https://en.wikipedia.org/wiki/CURL