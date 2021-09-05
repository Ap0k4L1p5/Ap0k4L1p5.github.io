---
layout: encrypted
---

## **USBRipper**
### Forensic Challenge

![usb.png](https://github.com/Ap0k4L1p5/private-repo/blob/master/folder/_protected/usbripper/usb.png)

CHALLENGE DESCRIPTION:

There is a sysadmin, who has been dumping all the USB events on his Linux host all the year... Recently, some bad guys managed to steal some data from his machine when they broke into the office. Can you help him to put a tail on the intruders? Note: once you find it, "crack" it.

---

Start with downloading the zip file given and extracted it.
Once extracted, it contained 2 files which is **auth.json** and **syslog** file. Based on the challenge description stated, these 2 files are all about the USB events that happened within the sysadmin PC.
![unzip.png](https://github.com/Ap0k4L1p5/private-repo/blob/master/folder/_protected/usbripper/unzip.png) 

Take a look on the **syslog** file, it’s a dump of every USB activities has ever occurred.
![syslog.png](https://github.com/Ap0k4L1p5/private-repo/blob/master/folder/_protected/usbripper/syslog.png)

While **auth.json** is a json file that authenticated any USB based on the model and manufacturer.
![auth.png](https://github.com/Ap0k4L1p5/private-repo/blob/master/folder/_protected/usbripper/auth.png)

Which means that any legit USB that have ever been used will be listed within the **auth.json** file. In order to identify any “intruder”, any USB listed from the syslog file must not be in the auth.json file.

Therefore, some analysis needs to be done between those 2 files. Since this is a forensic challenge, I did some research and found tools named USBRip. Well, that’s what this challenge all about I guess.
![G.png](https://github.com/Ap0k4L1p5/private-repo/blob/master/folder/_protected/usbripper/G.png) 

Incase need an extra understanding about this tools, may refer this [link](https://github.com/snovvcrash/usbrip).

Therefore, without further a due I start fire up that tool using the command follows:

`usbrip events violations auth.json -f syslog`

![usbrip.png](https://github.com/Ap0k4L1p5/private-repo/blob/master/folder/_protected/usbripper/usbrip.png)

As a result, it found one event from the **syslog** that not suited to the json file. 

After several Google-fu on understanding the output above, it appeared to be the Serial Number is a MD5 encoded string.
![md5.png](https://github.com/Ap0k4L1p5/private-repo/blob/master/folder/_protected/usbripper/md5.png)

Once reversed, it turned out to be a text formed "`mychemicalromance`". Since its something that came out from a violated USB events, I tried to put in a flag then submit. Well, that’s a flag for this challenge when append with the HTB{}. 

<br>

![ez.png](https://github.com/Ap0k4L1p5/private-repo/blob/master/folder/_protected/usbripper/ez.png)
 
