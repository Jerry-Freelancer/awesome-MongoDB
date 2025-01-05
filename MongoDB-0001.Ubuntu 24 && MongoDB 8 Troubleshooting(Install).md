\## <p align="center">Ubuntu 24 && MongoDB 8 Troubleshooting(Install)</p>



Troubleshooting: **"gpg: no valid OpenPGP data found."**



```
root@db01:/home/demo# cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=24.04
DISTRIB_CODENAME=noble
DISTRIB_DESCRIPTION="Ubuntu 24.04 LTS"
root@db01:/home/demo# lsb_release
No LSB modules are available.
root@db01:/home/demo# apt-get install gnupg curl
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
gnupg is already the newest version (2.4.4-2ubuntu17).
gnupg set to manually installed.
curl is already the newest version (8.5.0-2ubuntu10.6).
curl set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 140 not upgraded.
root@db01:/home/demo# curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
curl: (60) SSL certificate problem: certificate has expired
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
gpg: no valid OpenPGP data found.
root@db01:/home/demo# curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor^C
root@db01:/home/demo# echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse
root@db01:/home/demo#
root@db01:/home/demo#
root@db01:/home/demo# apt-get update
Hit:3 http://security.ubuntu.com/ubuntu noble-security InRelease
Hit:1 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble InRelease
Hit:2 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble-updates InRelease
Hit:4 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble-backports InRelease
Get:5 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease [3,005 B]
Err:5 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 41DE058A4E7DCA05
Reading package lists... Done
W: GPG error: https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 41DE058A4E7DCA05
E: The repository 'https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease' is not signed.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
root@db01:/home/demo# curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
File '/usr/share/keyrings/mongodb-server-8.0.gpg' exists. Overwrite? (y/N) curl: (60) SSL certificate problem: certificate has expired
                                                                                                                                      More details here: https://curl.se/docs/sslcerts.html

                         curl failed to verify the legitimacy of the server and therefore could not
                                                                                                   establish a secure connection to it. To learn more about this situation and
            how to fix it, please visit the web page mentioned above.

Enter new filename:
gpg: no valid OpenPGP data found.
gpg: dearmoring failed: File exists
root@db01:/home/demo# apt-get install -y mongodb-org
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package mongodb-org
root@db01:/home/demo# curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc
curl: (60) SSL certificate problem: certificate has expired
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
root@db01:/home/demo# chmod -R 777 /home/
root@db01:/home/demo# ls -lsa
total 20
0 drwxrwxrwx 4 demo demo  156 Jan  3 03:07 .
0 drwxrwxrwx 3 root root   40 Jan  3 03:14 ..
4 -rwxrwxrwx 1 demo demo  134 Jan  3 03:06 .bash_history
4 -rwxrwxrwx 1 demo demo  220 Mar 31  2024 .bash_logout
4 -rwxrwxrwx 1 demo demo 3771 Mar 31  2024 .bashrc
0 drwxrwxrwx 2 demo demo   34 Jan  3 02:11 .cache
4 -rwxrwxrwx 1 demo demo  807 Mar 31  2024 .profile
0 drwxrwxrwx 2 demo demo   29 Jan  3 02:11 .ssh
0 -rwxrwxrwx 1 demo demo    0 Jan  3 02:12 .sudo_as_admin_successful
4 -rwxrwxrwx 1 demo demo   50 Jan  3 03:07 .Xauthority
root@db01:/home/demo# cd /home/
root@db01:/home# ls -lsa
total 8
0 drwxrwxrwx  3 root root   40 Jan  3 03:14 .
4 drwxr-xr-x 23 root root 4096 Jan  3 02:14 ..
0 drwxrwxrwx  4 demo demo  156 Jan  3 03:07 demo
4 -rw-rw-r--  1 demo demo 1676 Jan  3 03:14 server-8.0.asc
root@db01:/home# gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg --dearmor
File '/usr/share/keyrings/mongodb-server-8.0.gpg' exists. Overwrite? (y/N) y




^M^C
gpg: signal Interrupt caught ... exiting

root@db01:/home#
root@db01:/home# gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg --dearmor
^C
gpg: signal Interrupt caught ... exiting

root@db01:/home# curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
File '/usr/share/keyrings/mongodb-server-8.0.gpg' exists. Overwrite? (y/N) curl: (60) SSL certificate problem: certificate has expired
                                                                                                                                      More details here: https://curl.se/docs/sslcerts.html

                         curl failed to verify the legitimacy of the server and therefore could not
                                                                                                   establish a secure connection to it. To learn more about this situation and
            how to fix it, please visit the web page mentioned above.

Enter new filename:
gpg: no valid OpenPGP data found.
gpg: dearmoring failed: File exists
root@db01:/home#
root@db01:/home# curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc |    sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg    --dearmor
curl: (60) SSL certificate problem: certificate has expired
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
gpg: no valid OpenPGP data found.
root@db01:/home#
root@db01:/home#
root@db01:/home# cat /etc/apt/sources.list.d/mongodb-org-8.0.list

deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse
root@db01:/home# vi /etc/apt/sources.list.d/mongodb-org-8.0.list
root@db01:/home# apt-get update
Hit:1 http://security.ubuntu.com/ubuntu noble-security InRelease
Hit:2 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble InRelease
Get:3 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease [3,005 B]
Hit:4 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble-updates InRelease
Err:3 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 41DE058A4E7DCA05
Hit:5 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble-backports InRelease
Reading package lists... Done
W: GPG error: https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 41DE058A4E7DCA05
E: The repository 'https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease' is not signed.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
root@db01:/home# apt-key list
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
/etc/apt/trusted.gpg.d/ubuntu-keyring-2012-cdimage.gpg
------------------------------------------------------
pub   rsa4096 2012-05-11 [SC]
      8439 38DF 228D 22F7 B374  2BC0 D94A A3F0 EFE2 1092
uid           [ unknown] Ubuntu CD Image Automatic Signing Key (2012) <cdimage@ubuntu.com>

/etc/apt/trusted.gpg.d/ubuntu-keyring-2018-archive.gpg
------------------------------------------------------
pub   rsa4096 2018-09-17 [SC]
      F6EC B376 2474 EDA9 D21B  7022 8719 20D1 991B C93C
uid           [ unknown] Ubuntu Archive Automatic Signing Key (2018) <ftpmaster@ubuntu.com>

root@db01:/home# curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
   --dearmor
File '/usr/share/keyrings/mongodb-server-8.0.gpg' exists. Overwrite? (y/N) curl: (60) SSL certificate problem: certificate has expired
                                                                                                                                      More details here: https://curl.se/docs/sslcerts.html

                         curl failed to verify the legitimacy of the server and therefore could not
                                                                                                   establish a secure connection to it. To learn more about this situation and
            how to fix it, please visit the web page mentioned above.

Enter new filename: 1
gpg: no valid OpenPGP data found.
root@db01:/home# curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc |    sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg    --dearmor
File '/usr/share/keyrings/mongodb-server-8.0.gpg' exists. Overwrite? (y/N) curl: (60) SSL certificate problem: certificate has expired
                                                                                                                                      More details here: https://curl.se/docs/sslcerts.html

                         curl failed to verify the legitimacy of the server and therefore could not
                                                                                                   establish a secure connection to it. To learn more about this situation and
            how to fix it, please visit the web page mentioned above.

Enter new filename: 1
File '1' exists. Overwrite? (y/N) y
gpg: no valid OpenPGP data found.
root@db01:/home# echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse
root@db01:/home#
root@db01:/home# sudo apt-get update
Hit:1 http://security.ubuntu.com/ubuntu noble-security InRelease
Get:2 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease [3,005 B]
Err:2 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 41DE058A4E7DCA05
Hit:3 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble InRelease
Hit:4 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble-updates InRelease
Hit:5 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble-backports InRelease
Reading package lists... Done
W: GPG error: https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 41DE058A4E7DCA05
E: The repository 'https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease' is not signed.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
root@db01:/home# apt-key list
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
/etc/apt/trusted.gpg.d/ubuntu-keyring-2012-cdimage.gpg
------------------------------------------------------
pub   rsa4096 2012-05-11 [SC]
      8439 38DF 228D 22F7 B374  2BC0 D94A A3F0 EFE2 1092
uid           [ unknown] Ubuntu CD Image Automatic Signing Key (2012) <cdimage@ubuntu.com>

/etc/apt/trusted.gpg.d/ubuntu-keyring-2018-archive.gpg
------------------------------------------------------
pub   rsa4096 2018-09-17 [SC]
      F6EC B376 2474 EDA9 D21B  7022 8719 20D1 991B C93C
uid           [ unknown] Ubuntu Archive Automatic Signing Key (2018) <ftpmaster@ubuntu.com>

root@db01:/home# ls -lsa
total 8
0 drwxrwxrwx  3 root root   49 Jan  3 03:24 .
4 drwxr-xr-x 23 root root 4096 Jan  3 02:14 ..
0 -rw-r--r--  1 root root    0 Jan  3 03:24 1
0 drwxrwxrwx  4 demo demo  156 Jan  3 03:17 demo
4 -rw-rw-r--  1 demo demo 1676 Jan  3 03:14 server-8.0.asc
root@db01:/home# curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc
curl: (60) SSL certificate problem: certificate has expired
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
root@db01:/home# curl -fsSL http://www.mongodb.org/static/pgp/server-8.0.asc
curl: (60) SSL certificate problem: certificate has expired
More details here: https://curl.se/docs/sslcerts.html

curl failed to verify the legitimacy of the server and therefore could not
establish a secure connection to it. To learn more about this situation and
how to fix it, please visit the web page mentioned above.
root@db01:/home#  sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg
gpg: directory '/root/.gnupg' created
gpg: keybox '/root/.gnupg/pubring.kbx' created
gpg: WARNING: no command supplied.  Trying to guess what you mean ...



^C
gpg: signal Interrupt caught ... exiting

root@db01:/home# cat
1               demo/           server-8.0.asc
root@db01:/home# cat server-8.0.asc | gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg --dearmor
File '/usr/share/keyrings/mongodb-server-8.0.gpg' exists. Overwrite? (y/N) y
root@db01:/home#
root@db01:/home# echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse
root@db01:/home# cat /etc/apt/sources.list.d/mongodb-org-8.0.list
deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse
root@db01:/home# apt-get update
Hit:1 http://security.ubuntu.com/ubuntu noble-security InRelease
Get:2 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 InRelease [3,005 B]
Get:4 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse arm64 Packages [18.0 kB]
Hit:3 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble InRelease
Get:5 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 Packages [17.9 kB]
Hit:6 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble-updates InRelease
Hit:7 http://mirrors.tuna.tsinghua.edu.cn/ubuntu noble-backports InRelease
Fetched 38.9 kB in 3s (12.0 kB/s)
Reading package lists... Done
root@db01:/home# apt-key list
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
/etc/apt/trusted.gpg.d/ubuntu-keyring-2012-cdimage.gpg
------------------------------------------------------
pub   rsa4096 2012-05-11 [SC]
      8439 38DF 228D 22F7 B374  2BC0 D94A A3F0 EFE2 1092
uid           [ unknown] Ubuntu CD Image Automatic Signing Key (2012) <cdimage@ubuntu.com>

/etc/apt/trusted.gpg.d/ubuntu-keyring-2018-archive.gpg
------------------------------------------------------
pub   rsa4096 2018-09-17 [SC]
      F6EC B376 2474 EDA9 D21B  7022 8719 20D1 991B C93C
uid           [ unknown] Ubuntu Archive Automatic Signing Key (2018) <ftpmaster@ubuntu.com>

root@db01:/home# apt-get install -y mongodb-org
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  mongodb-database-tools mongodb-mongosh mongodb-org-database mongodb-org-database-tools-extra mongodb-org-mongos mongodb-org-server mongodb-org-shell
  mongodb-org-tools
The following NEW packages will be installed:
  mongodb-database-tools mongodb-mongosh mongodb-org mongodb-org-database mongodb-org-database-tools-extra mongodb-org-mongos mongodb-org-server
  mongodb-org-shell mongodb-org-tools
0 upgraded, 9 newly installed, 0 to remove and 140 not upgraded.
Need to get 173 MB of archives.
After this operation, 653 MB of additional disk space will be used.
Get:1 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 mongodb-database-tools amd64 100.10.0 [46.4 MB]
Get:2 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 mongodb-mongosh amd64 2.3.7 [54.2 MB]
Get:3 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 mongodb-org-shell amd64 8.0.4 [2,606 B]
Get:4 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 mongodb-org-server amd64 8.0.4 [41.4 MB]
Get:5 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 mongodb-org-mongos amd64 8.0.4 [30.9 MB]
Get:6 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 mongodb-org-database-tools-extra amd64 8.0.4 [7,382 B]
Get:7 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 mongodb-org-database amd64 8.0.4 [3,062 B]
Get:8 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 mongodb-org-tools amd64 8.0.4 [2,398 B]
Get:9 https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0/multiverse amd64 mongodb-org amd64 8.0.4 [2,428 B]
Fetched 173 MB in 11min 0s (262 kB/s)
Selecting previously unselected package mongodb-database-tools.
(Reading database ... 83709 files and directories currently installed.)
Preparing to unpack .../0-mongodb-database-tools_100.10.0_amd64.deb ...
Unpacking mongodb-database-tools (100.10.0) ...
Selecting previously unselected package mongodb-mongosh.
Preparing to unpack .../1-mongodb-mongosh_2.3.7_amd64.deb ...
Unpacking mongodb-mongosh (2.3.7) ...
Selecting previously unselected package mongodb-org-shell.
Preparing to unpack .../2-mongodb-org-shell_8.0.4_amd64.deb ...
Unpacking mongodb-org-shell (8.0.4) ...
Selecting previously unselected package mongodb-org-server.
Preparing to unpack .../3-mongodb-org-server_8.0.4_amd64.deb ...
Unpacking mongodb-org-server (8.0.4) ...
Selecting previously unselected package mongodb-org-mongos.
Preparing to unpack .../4-mongodb-org-mongos_8.0.4_amd64.deb ...
Unpacking mongodb-org-mongos (8.0.4) ...
Selecting previously unselected package mongodb-org-database-tools-extra.
Preparing to unpack .../5-mongodb-org-database-tools-extra_8.0.4_amd64.deb ...
Unpacking mongodb-org-database-tools-extra (8.0.4) ...
Selecting previously unselected package mongodb-org-database.
Preparing to unpack .../6-mongodb-org-database_8.0.4_amd64.deb ...
Unpacking mongodb-org-database (8.0.4) ...
Selecting previously unselected package mongodb-org-tools.
Preparing to unpack .../7-mongodb-org-tools_8.0.4_amd64.deb ...
Unpacking mongodb-org-tools (8.0.4) ...
Selecting previously unselected package mongodb-org.
Preparing to unpack .../8-mongodb-org_8.0.4_amd64.deb ...
Unpacking mongodb-org (8.0.4) ...
Setting up mongodb-mongosh (2.3.7) ...
Setting up mongodb-org-server (8.0.4) ...
info: Selecting UID from range 100 to 999 ...

info: Adding system user `mongodb' (UID 110) ...
info: Adding new user `mongodb' (UID 110) with group `nogroup' ...
info: Not creating `/nonexistent'.
info: Selecting GID from range 100 to 999 ...
info: Adding group `mongodb' (GID 110) ...
info: Adding user `mongodb' to group `mongodb' ...
Setting up mongodb-org-shell (8.0.4) ...
Setting up mongodb-database-tools (100.10.0) ...
Setting up mongodb-org-mongos (8.0.4) ...
Setting up mongodb-org-database-tools-extra (8.0.4) ...
Setting up mongodb-org-database (8.0.4) ...
Setting up mongodb-org-tools (8.0.4) ...
Setting up mongodb-org (8.0.4) ...
Processing triggers for man-db (2.12.0-4build2) ...
Scanning processes...
Scanning linux images...

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
root@db01:/home# systemctl status mongod
○ mongod.service - MongoDB Database Server
     Loaded: loaded (/usr/lib/systemd/system/mongod.service; disabled; preset: enabled)
     Active: inactive (dead)
       Docs: https://docs.mongodb.org/manual
root@db01:/home# systemctl start mongod
root@db01:/home# mongosh
Current Mongosh Log ID: 67775cbc4a26c2ce8a567a2a
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.3.7
Using MongoDB:          8.0.4
Using Mongosh:          2.3.7

For mongosh info see: https://www.mongodb.com/docs/mongodb-shell/


To help improve our products, anonymous usage data is collected and sent to MongoDB periodically (https://www.mongodb.com/legal/privacy-policy).
You can opt-out by running the disableTelemetry() command.

------
   The server generated these startup warnings when booting
   2025-01-03T03:42:51.193+00:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
   2025-01-03T03:42:51.194+00:00: For customers running the current memory allocator, we suggest changing the contents of the following sysfsFile
   2025-01-03T03:42:51.194+00:00: For customers running the current memory allocator, we suggest changing the contents of the following sysfsFile
   2025-01-03T03:42:51.194+00:00: We suggest setting the contents of sysfsFile to 0.
   2025-01-03T03:42:51.194+00:00: We suggest setting swappiness to 0 or 1, as swapping can cause performance problems.
------

test>
```

Solutions from MongoDB official website: 

During the **Import the public key used by the package management system** step of the [Install MongoDB Community Edition](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/#std-label-install-community-ubuntu-pkg) procedure, you may encounter a `"gpg: no valid OpenPGP data found."` error.

Repeating the **Import the public key used by the package management system** step of the [Install MongoDB Community Edition](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/#std-label-install-community-ubuntu-pkg) procedure typically resolves this issue. Ensure you are copying the command and key exactly as documented.



Official website means that repeating the steps of * * import the public key used by the package management system during the installation of MongoDB Community Edition can usually solve this problem. Ensure that the commands and keys are copied exactly according to the document.

Treatment process: same as above