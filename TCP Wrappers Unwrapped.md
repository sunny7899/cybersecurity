_________________________________________________________________________

 

TCP Wrappers Unwrapped By Ankit Fadia Ankit@bol.net.in

_________________________________________________________________________

 

If you are running a Linux box and connect to the net through it, then there is every chance of someone else using or misusing the services running on your system. If someone gets to know your IP, then it does give the attacker an opportunity to be able to use the services or daemons running on varous ports of your system for malicious purposes. Thus it has become very important to ensure that you define a access list which controls who all can have access to what services on your system and who all should be blocked or denied access to any of the services on your system. This is where TCP Wrappers are so efficient but easy to use. 

 

So What Exactly are TCP Wrappers?

Well, TCP Wrappers basically act as efficient tools which allow us to define a set of rules called the access control rules. These access control rules control or define which hosts or machines are allowed to access and use the services running on the local machine(where the TCP Wrappers are installed and configured) and which hosts or machines are denied access to these services. So they infact are somewhat (well, quite remotely) something like Firewalls. They check to see who has requested the connection and if the connection requestor in amongst the deny list, then he is not allowed to open a connection. 

Besides controlling the access to various services on your system, TCP wrappers also allow you to log and know who is using what service at what time and even for what purpose. The best thing about TCP Wrappers is that they can also be used to set boobey traps to catch lamers. Read on for more details.

Now, the above can be arranged as below:

 

Anyway, before we go on, we need to have basic understanding of how exactly, Linux responds to a connection request. Now, the thing to remember here is that all requests for connections received by a Linux box, are transferred to the Internet Daemon or the 'inetd'. The 'inetd' is the main daemon on a Linux Machine, which receives all connection requests on behalf of all services or daemons running on all the Port Numbers. Now, once the 'inetd' receives a connection request, it uses 2 configuration files two determine what to do next. These two files are:

1. /etc/services
2. /etc/inetd.conf

The first one, the /etc/services file contains the names of the various Services and the corresponding port numbers on which they run. It is basically used by the 'inetd' to figure out what service runs on a particular Port Number.

The Second File, the /etc/inetd.conf contains the names of various services and the names of the corresponding daemons or programs providing those services. It is used by 'inetd' to figure out which program or daemon to call on when there is a request for a connection to a particular service.

Both these files work together and are interlinked. To understand with a real life example, as to how exactly the 'inetd' uses these two files to allow remote connections to take place, read the below paragraph.

Let us assume that the server is Y and the client(connection requestor) is X. Now, X send Y a packet containing the Port Number to which it wants to connect (In this case 23 or the Telnet Port) and other such information required for a TCP connection to start. At Y, the 'inetd' daemon responds to the connection request and looks up the /etc/services file for the service name running on Port 23 (This Port number is mentioned in the packet sent by X). The /etc/services/ responds to 'inetd' saying that the service name running on Port 23 is Telnet. Then, 'inetd' contacts '/etc/inetd.conf' and asks for the name of the daemon or program which runs the telnet service. The '/etc/inetd.conf' file replies saying that a daemon called in.telnetd. Then 'inetd' runs in.telnetd and that is when its job is over and it starts listening for other connection requests.

So, basically a remote system doesn't start out by directly communicating with the various daemons, but instead communicates only with the 'inetd' in the beginning.

 

Now, if we want to restrict some particular hosts from accessing our system and allow only a predefined set of hosts to access our system, they what do we do? This is when, TCP Wrappers come to the rescue.

A TCP Wrapper acts as a daemon which resides between the main daemon of the linus system i.e. the 'inetd' and other programs or daemons like in.ftpd, in.telnetd etc. As all connections to the linux box will pass through the inetd, they will also definitely pass through the TCP Wrapper. Right? Thus, if there are certain rules which are defined by TCP Wrappers, then they indeed can be used to manipulate access control.

NOTE: Normally, the inetd is configured to call the concerned programs or daemons like telnetd etc. However, once TCP wrappers are installed, then the inetd is configured to call on the Wrapper instead of the concerned daemon.

Anyway, once the inetd daemon calls on the TCP Wrapper or sends the packet recevied to the wrapper, the wrapper collects the source IP from the packet and accordingly allows or denies a connection. Irrespective of whether the connection is allowed or denied, the wrapper enters a log into the system log file.

 

NOTE: Now, I am assuming that you have been able to install the TCP Wrapper daemon i.e. /usr/sbin/tcpd For more information on how to install the TCP Wrapper read the Linux Documentation, Help or man pages. Or visit: www.linuxdoc.com or www.linux.com or www.newbielinux.com

 

Anyway, now, how does the TCP Wrapper daemon i.e. /usr/sbin/tcpd decide whether to allow access to a particular host or not? Well, the Wrapper is helped in this aspect by two files: 

1. The /etc/hosts.allow
2. The /etc/hosts.deny

As soon as the inetd sends the connection request to the Wrapper, tcpd scans the /etc/hosts.allow for a match for the hostname of the connection requestor. If a match is found, then the connection is opened. However, if no matches are found, then it searchs the /etc/hosts.deny file for a match. Well, if even then no match is found or even if both the files are empty, then the connection is allowed to be opened.

NOTE: By Default both of them are empty, allowing everyone to open connections. 

 

Now, that we know how tcpd works, let us move on to how exactly to configure it. The important thing to remember while configuring a tcpd, is what level of security do you really want your system to have. Whatever kind of setup you may have, you basically are left out with two options-:

1. The Not So Secure But Service Providing System: which means that mosts services are open and most people are allowed access to it. This would be the best option for you, if your system is used as server providing services like mail, FTP, Telnet etc to a number of legitimate users. This way not only can you provide services to legitimate users, but also ensure that unwanted hosts or clients do not get access to the services offered by your server.

2. The Secure But No Service Providing System: This is typically meant for those of you who are very security conscious and for those whose system is not providing services to legitimate users. This ensures that no one misuses your system.

The Not So Secure But Service Providing System

In this case, as we allow access to most services, the /etc/hosts.allow list is practically empty. While, the /etc/hosts.deny file contains rules which govern as to which hosts to disallow access. Let us take an example of a typical rule of the /etc/hosts.deny file to understand how exactly rules work.

The following is a hosts.deny entry which denies access to the Telnet and FTP services to anyone coming from abc.isp.com and anyone coming from the domain isp.net:

in.telnetd in.ftpd : abc.isp.com .isp.net

Note: The '.' preceeding the isp.net tells tcpd to disallow access to the FTP and Telnet daemons to anyone coming from a system in the isp.net domain.

If you want to deny access to all services, the above will change to:

ALL: abc.isp.com .isp.net 

Above, the ALL wildcard was used to restrict access to all services. Like ALL, there are a number of similiar Wildcards, which can be used for access control. Some common ones are:

LOCAL: This matches for hostnames coming from the local domain.
UNKNOWN: Matches hosts which are unresolved by DNS.
KNOWN: Matches hosts which are resolved by DNS.
PARANOID: Matches hosts whose names does not match with it's IP.

*******************
HACKING TRUTH: To allow access to all services to systems within your local domain, enter the following line in your /etc/hosts.allow:
ALL : LOCAL
********************

The Secure But No Service Providing System

The thing to remember here is that the hosts.allow file is checked first and then the hosts.deny and access is allowed only if no match is found in the hosts.deny file Anyway, in order to restrict all services or disallow all services to all hosts, then enter the following line in the hosts.deny file:

ALL : ALL

The hosts.allow file should contain the service name and the hosts to which access should be allowed. Now, we would certainly like to be able to access all services running on our own machine from our own machine. So, in the hosts.allow file, enter the below line:

ALL:localhost 

Now, say you want to be able to access the FTP daemon from abc.com, then enter the following line:

in.ftpd : abc.com

But, say you want to disallow hosts coming from the isp.net domain, and allow all other hosts to access the telnet daemon, then enter the following line:

in.telnetd : ALL EXCEPT isp.net

Got it? Well, that ends this editon of the manual on TCP Wrappers, I will soon be updating this with informationon how to Set Boobey traps to Catch Lamers and more exciting tips and tricks. 

 

Ankit Fadia

Ankit@bol.net.in

 

http://www.ankitfadia.com


To receive tutorials written by Ankit Fadia on everything you ever dreamt of in your Inbox, join his mailing list by sending a blank email to: programmingforhackers-subscribe@egroups.com

 

Wanna ask a question? Got a comment to make? Criticize, Comment and more…..by sending me an Instant Message on MSN Messenger. The ID that I use is: ankit_fadia@hotmail.com

 

Wanna learn Hacking? Wanna attend monthly lectures and discussions on various Networking/Hacking topics? Lectures, Debates and Discussions, get it all by simply joining The Hacking Truths club by clicking Here

 

