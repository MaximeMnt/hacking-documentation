## Intro

### Intro To Researching
- Start from a question: 
  - Example: How can I extract data from this image? 
    - Search for an answer for this question and work your way through untill you have a full understanding of the topic.
This is a really good way to conduct research: Start with a question; get an initial understanding of the topic; then look into more advanced aspects as needed.

### Vulnerability scanning
Often in hacking you'll come across software that might be open to exploitation. For example, Content Management Systems (such as Wordpress, FuelCMS, Ghost, etc) are frequently used to make setting up a website easier, and many of these are vulnerable to various attacks. So where would we look if we wanted to exploit specific software?

The answer to that question lies in websites such as:

- [ExploitDB](https://www.exploit-db.com/)
- [NVD](https://nvd.nist.gov/vuln/search)
- [CVE Mitre](https://cve.mitre.org/)

**NVD** keeps track of CVEs (Common Vulnerabilities and Exposures) -- whether or not there is an exploit publicly available -- **so it's a really good place to look if you're researching vulnerabilities in a specific piece of software. CVEs take the form: CVE-YEAR-IDNUMBER**

**ExploitDB** tends to be very useful for hackers, as it often actually contains exploits that can be downloaded and used straight out of the box. **It tends to be one of the first stops when you encounter software in a CTF or pentest.**

If you're inclined towards the CLI on Linux, Kali comes pre-installed with a tool called "searchsploit" which allows you to search ExploitDB from your own machine. This is offline, and works using a downloaded version of the database, meaning that you already have all of the exploits already on your Kali Linux!

### Manual Pages 
Get more information about a command by using the `man` functionality built in Linux!
If you don't know how to use a tool, `man` shoudl be your first port of call.

### Final Thoughts
You may have been told in school that there are good sources and bad sources of information. That may be true when it comes to essays and referencing information; however, it's my pleasure to state that it does not apply here. Any information can potentially be useful -- so feel free to use blogs, wikipedia, or anything else that contains what you're looking for! Blogs especially can often be very valuable for learning when it comes to information security, as many security researchers keep a blog.


## Linux Fundamentals
**Searching for files:**
- Find
- Grep

**Find**
Find files and folders in your linux system.
We can use `find` to lookup specific files. You can search using specific parameters like `-name` example: `find -name rockyou.txt`.

**Grep**
We can search through te content of files with the `grep` command.

**Shell operators**
| Symbol/Operator | Description                                                                                                                                      |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| &               | This operator allows you to run commands in the background of your terminal.                                                                     |
| &&              | This operator allows you to combine multiple commands together in one line of your terminal.                                                     |
| >               | This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere. |
| >>              | This operator does the same function of the `>` operator but appends the output rather than replacing (meaning nothing is overwritten).          |

**File**
You can use `file` to determine the type of a file.

**Permissions**
Certain users cannot access certain files or folders by default on Linux.
To view the setup permissons on a file you can run `ls -lh`. 


**Common Directories**

*/etc*
This root directory is one of the most important root directories on your system. The etc folder (short for etcetera) is a commonplace location to store system files that are used by your operating system. 

*/var*
The "/var" directory, with "var" being short for variable data,  is one of the main root folders found on a Linux install. This folder stores data that is frequently accessed or written by services or applications running on the system. For example, log files from running services and applications are written here (/var/log), or other data that is not necessarily associated with a specific user (i.e., databases and the like).

*/root*
Unlike the /home directory, the /root folder is actually the home for the "root" system user. There isn't anything more to this folder other than just understanding that this is the home directory for the "root" user. But, it is worth a mention as the logical presumption is that this user would have their data in a directory such as "/home/root" by default.  

*/tmp*
This is a unique root directory found on a Linux install. Short for "temporary", the /tmp directory is volatile and is used to store data that is only needed to be accessed once or twice. Similar to the memory on your computer, once the computer is restarted, the contents of this folder are cleared out.

What's useful for us in pentesting is that ==any user can write to this folder by default.== Meaning once we have access to a machine, it serves as a good place to store things like our enumeration scripts.