# Wireshark Investigation: DVWA Login

## Investigation Overview

This investigation analyzed HTTP traffic generated during a controlled login to the Damn Vulnerable Web Application (DVWA) running on Metasploitable 2.

The traffic was captured with Wireshark on the Kali Linux analyst workstation.

## Lab Systems

| System | IP Address | Role |
| Kali Linux | `192.168.8.100` | Analyst workstation |
| Metasploitable 2 | `192.168.8.101` | Web application server |

## Investigation Objective

The objective was to observe and understand the network traffic generated during a web application login.

The investigation focused on:

- HTTP GET requests
- HTTP POST requests
- HTTP status codes
- HTTP redirects
- Session cookies
- The relationship between client requests and server responses

## Evidence Observed

### 1. Login Page Request

The client requested:

GET /dvwa/login.php

The server responded with:

HTTP/1.1 200 OK

This indicates that the login page was successfully returned.

2. Login Form Submission
The client submitted:

POST /dvwa/login.php

The request used:

Content-Type: application/x-www-form-urlencoded

Wireshark decoded the form fields and showed that login credentials were transmitted in the HTTP request body.

The actual password is intentionally not documented in this repository.

3. Server Redirect

The server responded:

HTTP/1.1 302 Found
Location: index.php

The response was associated with the login POST request.

4. Session Information

The subsequent request to:

GET /dvwa/index.php

included a PHP session cookie:

PHPSESSID

This allows the application to associate the request with the existing client session.

5. Successful Page Retrieval

The server then responded:

HTTP/1.1 200 OK

for:

/dvwa/index.php

Traffic Sequence

GET /dvwa/login.php
        |
        | 200 OK
        v
Login page
        |
        | POST /dvwa/login.php
        v
302 Found
Location: index.php
        |
        | GET /dvwa/index.php
        | PHP session cookie
        v
200 OK


SOC Analysis
Observation

An HTTP login sequence was observed between the Kali workstation and the Metasploitable 2 web server.

Evidence

The captured traffic contained:

A login page request
An HTTP POST containing form data
A 302 redirect
A subsequent request for index.php
A PHP session cookie
A 200 OK response

Assessment

The sequence is consistent with a successful login.

Because the activity was intentionally generated during a controlled lab exercise, it was expected activity.

Security Finding

The login was performed over unencrypted HTTP.

Because HTTP does not provide encryption, the submitted form data and session information were visible in the packet capture.

In a real environment, transmitting authentication credentials over unencrypted HTTP would represent a significant security concern.

Tools Used
Kali Linux
Wireshark
Metasploitable 2
DVWA
Key Learning

This investigation demonstrated how a SOC analyst can follow an application transaction across multiple packets rather than interpreting a single packet in isolation.

The investigation followed:

Observation → Context → Evidence → Assessment

