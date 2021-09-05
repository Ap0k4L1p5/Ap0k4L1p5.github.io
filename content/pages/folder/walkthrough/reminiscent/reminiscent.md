## **Reminiscent**
### Forensic Challenge

![c.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/c.png)

CHALLENGE DESCRIPTION:

Suspicious traffic was detected from a recruiter's virtual PC. A memory dump of the offending VM was captured before it was removed from the network for imaging and analysis. Our recruiter mentioned he received an email from someone regarding their resume. A copy of the email was recovered and is provided for reference. Find and decode the source of the malware to find the flag.

---

Based on the given file, extracted 3 files which one of it is a .elf file. It’s a memory dump file from a virtual PC as per stated from the description. Other 2 files are text file and eml file which are just info of the image given and the email recovered file respectively.

![s1.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/s1.png) 

Since there is a memory dump file, I started with scan the process occurred using Volatility tool. Its a common tool for forensic investigation and analysis. Command as follows:

<code>Volatilify -f ‘flounder-pc-memdump.elf’ --profile=Win7SP1x64 psscan</code>

Memory dump profile can be found in the imageinfo.txt.

Based on the result, there some suspicious process happened involving the **explorer.exe** and **thunderbird.ex**. As shown below, PID of **thunderbird.ex** run on PPID of **explorer.exe**. PPID is a Parent PID, means that it run through the internet explorer. As far as I know, Thunderbird is a mail server services but nevermind, proceed with retrieving other artifact.

![s2.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/s2.png)

Next step was trying to analyze network communication thru command below.

<code>Volatilify -f ‘flounder-pc-memdump.elf’ --profile=Win7SP1x64 netscan</code>
![s3.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/s3.png)

There is malicious IP same as mentioned in **resume.eml** file. The IP also shown that the connection was established and it was invoking **powershell.exe** in the PC. Means that resume sent is a malicious file that trigger the **powershell.exe**.

Proceed with the analysis, I tried to list all of files in the memory dump and resulting a lot of files. To ease my work, I narrowed down the listing by grep resume only.

<code>Volatilify -f ‘flounder-pc-memdump.elf’ --profile=Win7SP1x64 filescan | grep resume</code>
![s4.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/s4.png)

2 files found! I proceed with downloading the file with **rw** permission to further analysis using command as follows:

<code>volatility -f '/root/Desktop/Misc/reminiscent/flounder-pc-memdump.elf' --profile=Win7SP1x64 dumpfiles -Q 0x000000001e8feb70 --dump-dir ~/Desktop/Misc/reminiscent/</code>

![s5.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/s5.png)

Once done, I read the dat file using **cat** command and it display powershell command was executed but in Base64 encoded.
![s6.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/s6.png)

In order to decode it, I pasted the code in **cyberchef** and turned out it is another Base64 encoded code.
![s7.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/s7.png)

After clean it up a bit by eliminating all the dot, once again decode it in **cyberchef** and flag can be found in the decoded command.
![s9.png](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/s8.png)

<br>

![e.jpg](https://raw.githubusercontent.com/Ap0k4L1p5/Ap0k4L1p5.github.io/master/content/pages/folder/walkthrough/reminiscent/e.jpg)

*  ##### [BACK](/content/pages/writeup.html "Back to Homepage")
 
