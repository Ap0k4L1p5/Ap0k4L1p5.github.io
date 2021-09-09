## **USBRipper**
### Forensic Challenge

![usb.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/USBRipper/usb.png)

CHALLENGE DESCRIPTION:

There is a sysadmin, who has been dumping all the USB events on his Linux host all the year... Recently, some bad guys managed to steal some data from his machine when they broke into the office. Can you help him to put a tail on the intruders? Note: once you find it, "crack" it.

---

Start with downloading the zip file given and extracted it.
Once extracted, it contained 2 files which is **auth.json** and **syslog** file. Based on the challenge description stated, these 2 files are all about the USB events that happened within the sysadmin PC.

![unzip.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/USBRipper/unzip.png) 

Take a look on the **syslog** file, it’s a dump of every USB activities has ever occurred.
![syslog.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/USBRipper/syslog.png)

While **auth.json** is a json file that authenticated any USB based on the model and manufacturer.
![auth.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/USBRipper/auth.png)

Which means that any legit USB that have ever been used will be listed within the **auth.json** file. In order to identify any “intruder”, any USB listed from the syslog file must not be in the auth.json file.

Therefore, some analysis needs to be done between those 2 files. Since this is a forensic challenge, I did some research and found tools named USBRip. Well, that’s what this challenge all about I guess.
![G.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/USBRipper/G.png) 

Incase need an extra understanding about this tools, may refer this [link](https://github.com/snovvcrash/usbrip).

Therefore, without further a due I start fire up that tool using the command follows:

> <code>usbrip events violations auth.json -f syslog</code>

![usbrip.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/USBRipper/usbrip.png)

As a result, it found one event from the **syslog** that not suited to the json file. 

After several Google-fu on understanding the output above, it appeared to be the Serial Number is a MD5 encoded string.

![md5.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/USBRipper/md5.png)

Once reversed, it turned out to be a text formed "<samp>mychemicalromance</samp>". Since its something that came out from a violated USB events, I tried to put in a flag then submit. Well, that’s a flag for this challenge when append with the HTB{}. 

<br>

![ez.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/USBRipper/ez.png)

*  ##### [BACK](/content/pages/writeup.html "Back to Homepage")
 
