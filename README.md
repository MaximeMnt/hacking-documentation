# hacking-documentation

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
| Symbol/Operator      | Description |
| -------------------- | ----------- |
| &                    | This operator allows you to run commands in the background of your terminal.       |
| &&                   | This operator allows you to combine multiple commands together in one line of your terminal.        |
| >                  | This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere.        |
| >>                   | This operator does the same function of the `>` operator but appends the output rather than replacing (meaning nothing is overwritten).        |

