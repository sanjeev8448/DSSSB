# 1. Internet

The Internet is a global system of interconnected computer networks that communicate using the Internet protocol suite, commonly known as TCP/IP.

It connects private, public, academic, business and government networks around the world.

### How does the Internet work?

Suppose you open a website on your laptop.

1. Your device connects to a local network using Wi-Fi or Ethernet.
    
2. DNS may resolve the website's domain name to an IP address.
    
3. Your device sends packets toward the destination through its network gateway.
    
4. Routers forward packets across interconnected networks.
    
5. The destination server processes the request and sends a response.
    

### How a device connects to the Internet

Your laptop

Local router / gateway

Internet service provider (ISP)

Interconnected networks

Destination server

This is a simplified logical path. Real Internet traffic can cross many networks and routers, and the return path can be different from the forward path.

### Common Internet services

- World Wide Web (WWW)
    
- Email
    
- File transfer
    
- Voice and video calls
    
- Online gaming
    
- Remote access
    
- Cloud applications
    
- Internet messaging
    

### Important Internet-related terms

|Term|Meaning|
|---|---|
|ISP|Internet Service Provider; provides Internet connectivity|
|IP address|Logical address used to identify network endpoints|
|Router|Forwards packets between IP networks|
|DNS|Resolves domain names and other DNS records|
|TCP/IP|Protocol suite used for communication across interconnected networks|
|Client|A device or application requesting a service|
|Server|A system or application providing a service|

### Internet versus intranet versus extranet

|Internet|Intranet|Extranet|
|---|---|---|
|Global interconnection of networks|Private organizational network|Controlled access to selected resources for external parties|
|Publicly reachable services may be available to Internet users|Normally restricted to an organization|Often used by suppliers, customers or partners|
|Example: Public websites|Internal company portal|Business portal for approved suppliers|

Exam traps:

- The Internet is a network of networks.
    
- The Internet is not the same as the WWW.
    
- An ISP provides connectivity; it is not the same as DNS.
    
- The Internet can be used without browsing websites, for example through email or other Internet applications.
    

# 2. URL — Uniform Resource Locator

A URL (Uniform Resource Locator) is a type of identifier that specifies where a resource can be accessed and, depending on the scheme, how to access it.

URLs are used for web pages, images, files and other resources.

### Example URL

`https://www.example.com:443/products?id=25#details`

This URL can be divided into several components.

### Anatomy of a URL

[https://www.example.com:443/products?id=25#details](https://www.example.com:443/products?id=25#details)

https://

Scheme

Specifies the access scheme or protocol context.

www.example.com

Host

Identifies the domain or host.

:443

Port

Optional explicit port number.

/products

Path

Identifies a resource or route on the server.

?id=25

Query

Carries parameters or other query information.

#details

Fragment

Identifies a section or fragment within the resource; normally processed by the client, not sent as part of the HTTP request target.

Not every URL contains every component. For example, the port, query and fragment may all be omitted.

### Common URL schemes

|Scheme|Common use|
|---|---|
|`http://`|Web communication using HTTP|
|`https://`|Web communication protected using TLS|
|`ftp://`|Historically used to identify FTP resources|
|`mailto:`|Identifies an email address to be handled by an email application|
|`file:`|Identifies a resource in a file system|

Modern browsers may restrict or no longer support some older URL schemes or behaviours, depending on security policy.

### URL versus domain name

Consider:

`https://www.example.com/about`

- `www.example.com` is the host name.
    
- `https://www.example.com/about` is the complete URL.
    

A domain name is a naming component; a URL can contain a scheme, host, path and other components.

### URL versus URI

URI stands for Uniform Resource Identifier. It is the broader term for identifying a resource.

A URL is a type of URI that identifies a resource by its location or access mechanism in the relevant scheme.

For introductory exam purposes, remember that every URL is generally treated as a URI, but not every URI must be a URL.

### Exam traps

- URL = Uniform Resource Locator.
    
- Domain name and URL are not interchangeable.
    
- `https` is the scheme, not the domain name.
    
- `?` introduces the query component; `#` introduces the fragment.
    
- The fragment is normally not sent to the server in the HTTP request.
    
- A URL does not necessarily have a query string or an explicit port.
    

# 3. WWW — World Wide Web

WWW stands for World Wide Web. It is a system of interlinked web pages and other resources that users can access over the Internet.

The Web uses technologies such as URLs, HTTP/HTTPS, browsers and web servers.

The WWW was invented by Tim Berners-Lee at CERN in 1989. It developed into a widely used way to publish, link and access information over the Internet.

### Main components of the Web

|Component|Function|
|---|---|
|Web browser|Requests and displays web content|
|Web server|Receives requests and returns resources or responses|
|Web page|A document or resource displayed by a browser|
|Website|A collection of related web pages and resources|
|URL|Identifies a web resource's location or access method|
|HTTP/HTTPS|Protocols used to exchange web requests and responses|
|Hyperlink|A link that lets users navigate to another resource or location|

### How does the WWW work?

1. You enter a URL in a browser.
    
2. DNS may resolve the host name to an IP address.
    
3. The browser connects to the server using the applicable network and transport protocols.
    
4. The browser sends an HTTP request, often over a protected HTTPS connection.
    
5. The server returns a response.
    
6. The browser interprets the returned content and displays the page.
    

### Browser–Web Server Model

Web browser

Client

HTTP request

HTTP response

Web server

Responds to requests

### Important distinction: Internet vs WWW

|Internet|WWW|
|---|---|
|Global interconnection of networks|A system of linked web resources that operates over the Internet|
|Infrastructure that carries many kinds of traffic|One major service using that infrastructure|
|Supports web, email, VoIP, file transfer and more|Primarily accessed using browsers and HTTP/HTTPS|
|Broader concept|One service available through the Internet|

Example: You can send email or make a VoIP call over the Internet without visiting a web page.

### Exam traps

- WWW is not the same as the Internet.
    
- Tim Berners-Lee invented the Web at CERN in 1989.
    
- HTTP/HTTPS is used for web communication.
    
- A browser is a client; a web server responds to requests.
    
- The Web uses hyperlinks to connect resources.
    

# 4. Web

The word Web is the common shortened name for the World Wide Web. In ordinary networking questions, “Web” and “WWW” generally refer to the same system.

However, related terms have different meanings.

### Web page vs website vs web browser vs web server

|Term|Meaning|Example|
|---|---|---|
|Web page|An individual web resource or document|An article page|
|Website|A collection of related web pages and resources|A university's public site|
|Web browser|Client software for accessing web content|Chrome, Firefox, Edge|
|Web server|Software or a system that responds to web requests|A server running a web application|
|Web application|An interactive application accessed through a browser or web interface|Online banking or a spreadsheet app|

### Static versus dynamic web pages

Static web page: The server typically returns content that has been prepared in advance, such as a fixed HTML page.

Dynamic web page: The content may be generated or customized in response to a request, user account, database data, current conditions or application logic.

|Static page|Dynamic page|
|---|---|
|Often serves prebuilt content|May generate content on demand|
|May need a content update to change its contents|Can show different content for different users or requests|
|Example: a simple fixed information page|Example: an account dashboard|

A static page can still contain JavaScript for interactive behaviour. Static versus dynamic describes how content is delivered or generated, not simply whether a page has animations.

### Web technologies

|Technology|Typical role|
|---|---|
|HTML|Structures web content|
|CSS|Controls presentation and layout|
|JavaScript|Adds client-side behaviour and interactivity|
|HTTP/HTTPS|Transfers requests and responses|
|Web server|Serves resources and may run server-side logic|
|Database|Stores information used by dynamic applications|

Exam trap: HTML is a markup language, CSS is a style-sheet language, and JavaScript is a programming language. HTTP is a network protocol. They serve different purposes.

# 5. Email — Electronic Mail

Email (electronic mail) is an Internet service that allows users to send and receive electronic messages over a network.

An email may contain text, files, images, documents and other attachments.

### Main components of an email system

- Mail User Agent (MUA): The application used to compose, send, read and manage emails.
    
- Mail server: Stores, sends, receives or relays email.
    
- SMTP: Sends and relays email between clients and mail servers or between mail servers.
    
- POP3 / IMAP: Protocols commonly used by clients to retrieve or access email stored on a server.
    
- DNS MX records: Identify mail servers responsible for accepting email for a domain.
    

### How email is sent

Suppose you send an email from `alice@example.com` to `bob@example.net`.

1. Alice composes the email in a mail application.
    
2. Her application submits the outgoing message to her mail server using SMTP.
    
3. The sending mail server uses DNS information, such as MX records for `example.net`, to locate a receiving mail server.
    
4. SMTP relays the message to the receiving mail server.
    
5. Bob reads or retrieves the email through webmail or a mail client using the service provided, commonly with IMAP or POP3.
    

### Email Delivery Process

Sender's mail application

Sender's mail server

SMTP submission

Receiving mail server

SMTP relay

Recipient's mail application

IMAP, POP3 or webmail

This is a simplified flow. Real systems may involve filtering services, relays, queues, anti-spam checks and other intermediate systems.

### Important parts of an email

Consider a simplified message:

```
From: alice@example.com
To: bob@example.net
Subject: Meeting

Hello Bob,
The meeting starts at 10 AM.
```

|Part|Purpose|
|---|---|
|From|Identifies the stated sender|
|To|Main recipient or recipients|
|CC|Sends a visible copy to additional recipients|
|BCC|Sends a copy to recipients whose addresses are hidden from other recipients in the ordinary message display|
|Subject|Brief description of the email|
|Body|Main message content|
|Attachment|File included with the message|

The visible `From` field does not, by itself, prove that the sender is authentic. Email authentication mechanisms help receivers assess whether a message is authorized to come from a domain.

### Email protocols and ports

|Protocol|Function|Common port(s)|
|---|---|---|
|SMTP|Sending and relaying email|TCP 25|
|SMTP submission|Client submission to a mail server|TCP 587|
|SMTP over implicit TLS|Secure submission|TCP 465|
|POP3|Retrieving mail|TCP 110|
|POP3 over implicit TLS|Secure POP3 retrieval|TCP 995|
|IMAP|Accessing and synchronizing email|TCP 143|
|IMAP over implicit TLS|Secure IMAP access|TCP 993|

These are conventional port assignments. Servers can be configured differently, and STARTTLS can secure a connection that starts on a traditional non-implicit-TLS port.

### SMTP vs POP3 vs IMAP

|Feature|SMTP|POP3|IMAP|
|---|---|---|---|
|Main purpose|Sending and relaying|Retrieving messages|Accessing and synchronizing messages|
|Typical direction|Sender/client to outgoing server, then server to server|Mail server to client|Client interacts with mailbox on server|
|Server-side folder and synchronization features|Not its main role|Limited in the traditional model|Supports folders and synchronization|
|Exam clue|Outgoing email|Download-oriented retrieval|Server-side mailbox synchronization|

### Advantages of email

- Fast communication over long distances.
    
- Supports multiple recipients.
    
- Allows documents and other files to be attached.
    
- Provides a written record of communication.
    
- Supports asynchronous communication: sender and recipient do not need to be online simultaneously.
    

### Limitations

- Unwanted messages and phishing.
    
- Attachment-based malware risks.
    
- Spoofing and impersonation risks.
    
- Attachment-size and mailbox-storage limits.
    
- Delivery may be delayed or rejected.
    

### Exam traps

- SMTP sends or relays email; POP3 and IMAP are used to retrieve or access received email.
    
- Email does not require both sender and recipient to be online at the same time.
    
- Webmail is an email application accessed through the Web; email itself is a broader Internet service.
    
- An email attachment can contain many types of data, not just text.
    

# 6. VoIP — Voice over Internet Protocol

VoIP stands for Voice over Internet Protocol.

It is a technology that carries voice communication using IP networks, rather than relying exclusively on traditional circuit-switched telephone networks.

Examples include Internet-based voice calls, softphone applications, and IP phones used in offices.

### How does VoIP work?

1. A microphone captures the speaker's voice.
    
2. The audio is digitized and encoded using a voice codec.
    
3. The audio is placed into packets.
    
4. The packets travel across an IP network.
    
5. The receiving system reorders and buffers the packets as needed, decodes the audio and plays it through a speaker.
    

### VoIP Communication

Speaker's voice

Digitization and codec

Voice converted into encoded digital audio

Voice packets

Transported over an IP network

Receive, buffer and decode

Audio reconstructed for playback

Recipient hears the voice

### Important VoIP protocols

|Protocol / technology|Main purpose|
|---|---|
|SIP|Initiates, modifies and terminates multimedia communication sessions|
|RTP|Carries real-time audio or video media|
|RTCP|Provides control and quality-monitoring information associated with RTP sessions|
|UDP|Commonly carries real-time media when low overhead is useful|
|IP|Routes packets across networks|
|Codecs|Encode and decode voice, with different quality and bitrate trade-offs|

SIP and RTP are not the same. SIP helps establish and manage a call; RTP commonly carries the media. VoIP is a broad technology, so not every implementation uses the same protocol stack.

### VoIP versus traditional telephone service

|Feature|VoIP|Traditional circuit-switched telephone|
|---|---|---|
|Underlying network|IP network|Traditional circuit-switched network|
|Data representation|Digitized voice carried over packets|Depends on the telephone system; classic circuit-switched systems reserve a circuit|
|Resource use|Network capacity generally shared using packet switching|Dedicated circuit resources allocated for the call|
|Quality dependence|Strongly affected by latency, jitter, packet loss and congestion|Depends on circuit and transmission quality|
|Examples|IP phone, Internet calling app|Classic circuit-switched landline call|

Traditional telephone networks have evolved considerably, and not all present-day telephone services use classic circuit switching. The comparison describes the traditional models relevant to introductory exams.

### Important VoIP quality terms

|Term|Meaning|
|---|---|
|Latency|Delay between sending and receiving media|
|Jitter|Variation in packet delay|
|Packet loss|Media packets that fail to arrive|
|Codec|Encodes and decodes voice|
|Echo cancellation|Reduces acoustic or signal echo|
|QoS|Quality-of-Service mechanisms that can prioritize or manage traffic|

### Advantages

- Can reduce communication costs depending on the network and service plan.
    
- Supports voice and other media over IP infrastructure.
    
- Enables integration with messaging, conferencing and business applications.
    
- Can support geographically distributed teams and remote workers.
    

### Limitations

- Voice quality may degrade when the network is congested.
    
- High latency and jitter can disrupt conversation.
    
- Packet loss can cause gaps in audio.
    
- Power outages or connectivity failures can interrupt service when backup options are unavailable.
    
- Emergency calling and location handling depend on the service and configuration.
    

### Exam traps

- VoIP means Voice over Internet Protocol.
    
- VoIP carries voice over IP networks, usually using packet-based communication.
    
- SIP is commonly used for call/session signalling; RTP carries real-time media in many systems.
    
- UDP is commonly used for real-time media, but VoIP does not inherently require every part of every call to use UDP.
    
- Jitter is variation in delay, whereas latency is delay itself.
    

# 7. Internet, URL, WWW, Web, Email and VoIP — comparison table

|Topic|What it is|Key technology / protocol|Exam clue|
|---|---|---|---|
|Internet|Global interconnection of networks|TCP/IP, IP routing|Network of networks|
|URL|Identifier specifying a resource's location or access method|Scheme, host, path, optional query/fragment|Uniform Resource Locator|
|WWW|System of interlinked web resources|HTTP/HTTPS, URLs, browsers|Invented by Tim Berners-Lee|
|Web|Common short name for the WWW|Web pages, hyperlinks, browsers|Client-server web access|
|Email|Electronic messaging service|SMTP, POP3, IMAP, DNS MX|Send, relay and retrieve messages|
|VoIP|Voice communication over IP networks|SIP, RTP, IP; often UDP for media|Voice packets over an IP network|

## 8. Quick exam revision

Memorize the following distinctions:

- Internet vs WWW: The Internet is the global network infrastructure; the WWW is a service running over it.
    
- URL vs domain name: A domain name is one component that may appear in a URL.
    
- HTTP vs HTTPS: HTTPS uses TLS to secure HTTP communication.
    
- Web page vs website: A page is an individual resource; a website groups related resources.
    
- SMTP vs POP3: SMTP sends and relays email; POP3 retrieves it.
    
- POP3 vs IMAP: POP3 is traditionally download-oriented; IMAP supports server-side mailbox access and synchronization.
    
- VoIP vs SIP: VoIP is the general technology; SIP is a protocol commonly used to manage call sessions.
    
- SIP vs RTP: SIP manages signalling; RTP commonly carries audio and video media.
    
- DNS vs URL: DNS resolves names to records; a URL identifies a resource and may contain a host name.
    
- Internet vs ISP: The Internet is the interconnected network system; an ISP provides connectivity to it.