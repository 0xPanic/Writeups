![Description](/auctf2020/img/description.png)

Clicking the link took me to the default apache page, so I decided to go straight into gobuster to find other pages.

![Gobuster](/auctf2020/img/gobuster.png)

First time I ran it the /cgi-bin/ directory stood out to me, so I ran it again on that directory and discovered the scriptlet file located within.

![Scriptlet](/auctf2020/img/whoami.png)

This appears to be a bash script that just runs whoami. Since this is bash, let's try exploiting shellshock. (cgi-bin + ctf - user input = shellshock)

To begin, I intercepted the request firefox was making to the script in burpsuite

![Burp1](/auctf2020/img/burp1.png)

And then hitting ctrl + R to send it to the repeater to make things eaiser.
![Burp2](/auctf2020/img/burp2.png)

To test for shellshock, we can replace the user agent string with `() { :;}; echo; echo vulnerable` . If the response from the server contains the word `vulnerable`, we have a hit.

And it did.
![Burp3](/auctf2020/img/burp3.png)

My home network wouldn't allow me to catch a reverse shell, but burpsuite is all the shell I need at this point. After some poking around, I found something interesting at /root (full path for ls was required)

![Burp3](/auctf2020/img/binls.png)

catting the file revealed hex data
![Burp3](/auctf2020/img/bincat.png)

So I threw that into cyberchef and decoded from hex. After decoding that cyberchef was nice enough to point out that this was gzipped data and just handed me the flag.
![Burp3](/auctf2020/img/cyberchef.png)

Success! This was a really fun challenge.

