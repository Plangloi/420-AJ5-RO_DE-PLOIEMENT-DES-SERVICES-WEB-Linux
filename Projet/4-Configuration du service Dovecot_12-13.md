# 12-Installation et Configuration du service Dovecot :


1. Install dovecot-pop3d :
```bash
apt install dovecot-pop3d -y
```
2. Install devecot-imapd :
```bash
apt install dovecot-imapd -y
```
3. Edit dovecot.conf :
```bash
vi /etc/dovecot/dovecot.conf
```
```yml
protocols = pop3 imap
!include_try /usr/share/dovecot/protocols.d/*.protocol

dict {
  #quota = mysql:/etc/dovecot/dovecot-dict-sql.conf.ext
}

!include conf.d/*.conf

```


4. Edit 10-mail.comf :  
```bash
vi /etc/dovecot/conf.d/10-mail.conf
```
```yml
## Dovecot configuration file

# If you're in a hurry, see http://wiki2.dovecot.org/QuickConfiguration

# "doveconf -n" command gives a clean output of the changed settings. Use it
# instead of copy&pasting files when posting to the Dovecot mailing list.

# '#' character and everything after it is treated as comments. Extra spaces
# and tabs are ignored. If you want to use either of these explicitly, put the
# value inside quotes, eg.: key = "# char and trailing whitespace  "

# Most (but not all) settings can be overridden by different protocols and/or
# source/destination IPs by placing the settings inside sections, for example:
# protocol imap { }, local 127.0.0.1 { }, remote 10.0.0.0/8 { }

# Default values are shown for each setting, it's not required to uncomment
# those. These are exceptions to this though: No sections (e.g. namespace {})
# or plugin settings are added by default, they're listed only as examples.
# Paths are also just examples with the real defaults being based on configure
# options. The paths listed here are for configure --prefix=/usr
# --sysconfdir=/etc --localstatedir=/var

protocols = pop3 imap

# Enable installed protocols
!include_try /usr/share/dovecot/protocols.d/*.protocol


dict {
  #quota = mysql:/etc/dovecot/dovecot-dict-sql.conf.ext
}

# Most of the actual configuration gets included below. The filenames are
# first sorted by their ASCII value and parsed in that order. The 00-prefixes
# in filenames are intended to make it easier to understand the ordering.
!include conf.d/*.conf

# A config file can also tried to be included without giving an error if
# it's not found:
!include_try local.conf
root@ubuntu-server:/home/ipat#
root@ubuntu-server:/home/ipat#
root@ubuntu-server:/home/ipat# cat /etc/de
debconf.conf    debian_version  default/        deluser.conf    depmod.d/
root@ubuntu-server:/home/ipat# cat /etc/dovecot/conf.d/10-mail.conf

## Mailbox locations and namespaces
mail_location = maildir:~/Maildir

namespace inbox {
  inbox = yes
}

mail_privileged_group = mail



protocol !indexer-worker {
  # If folder vsize calculation requires opening more than this many mails from
  # disk (i.e. mail sizes aren't in cache already), return failure and finish
  # the calculation via indexer process. Disabled by default. This setting must
  # be 0 for indexer-worker processes.
  #mail_vsize_bg_after_count = 0
}

root@ubuntu-server:/home/ipat#
```


5. Edit 10-master.conf :
```bash
vi /etc/dovecot/conf.d/10-master.conf
```
```yml
#default_process_limit = 100
#default_client_limit = 1000

# Default VSZ (virtual memory size) limit for service processes. This is mainly
# intended to catch and kill processes that leak memory before they eat up
# everything.
#default_vsz_limit = 256M

# Login user is internally used by login processes. This is the most untrusted
# user in Dovecot system. It shouldn't have access to anything at all.
#default_login_user = dovenull

# Internal user is used by unprivileged processes. It should be separate from
# login user, so that login processes can't disturb other processes.
#default_internal_user = dovecot

service imap-login {
  inet_listener imap {
    port = 143
  }
  inet_listener imaps {
    port = 993
    ssl = yes
  }

  # Number of connections to handle before starting a new process. Typically
  # the only useful values are 0 (unlimited) or 1. 1 is more secure, but 0
  # is faster. <doc/wiki/LoginProcess.txt>
  #service_count = 1

  # Number of processes to always keep waiting for more connections.
  #process_min_avail = 0

  # If you set service_count=0, you probably need to grow this.
  #vsz_limit = $default_vsz_limit
}

service pop3-login {
  inet_listener pop3 {
    port = 110
  }
  inet_listener pop3s {
    port = 995
    ssl = yes
  }
}

service submission-login {
  inet_listener submission {
    port = 587
  }
}

service lmtp {
  unix_listener lmtp {
   #mode = 0666
  }

  # Create inet listener only if you can't use the above UNIX socket
  #inet_listener lmtp {
    # Avoid making LMTP visible for the entire internet
    #address =
    #port =
  #}
}

service imap {
  # Most of the memory goes to mmap()ing files. You may need to increase this
  # limit if you have huge mailboxes.
  #vsz_limit = $default_vsz_limit

  # Max. number of IMAP processes (connections)
  #process_limit = 1024
}

service pop3 {
  # Max. number of POP3 processes (connections)
  #process_limit = 1024
}

service submission {
  # Max. number of SMTP Submission processes (connections)
  #process_limit = 1024
}

service auth {
  # auth_socket_path points to this userdb socket by default. It's typically
  # used by dovecot-lda, doveadm, possibly imap process, etc. Users that have
  # full permissions to this socket are able to get a list of all usernames and
  # get the results of everyone's userdb lookups.
  #
  # The default 0666 mode allows anyone to connect to the socket, but the
  # userdb lookups will succeed only if the userdb returns an "uid" field that
  # matches the caller process's UID. Also if caller's uid or gid matches the
  # socket's uid or gid the lookup succeeds. Anything else causes a failure.
  #
  # To give the caller full permissions to lookup all users, set the mode to
  # something else than 0666 and Dovecot lets the kernel enforce the
  # permissions (e.g. 0777 allows everyone full permissions).
  unix_listener auth-userdb {
    #mode = 0666
    #user =
    #group =
  }

  # Postfix smtp-auth
  #unix_listener /var/spool/postfix/private/auth {
  #  mode = 0666
  #}

  # Auth process is run as this user.
  #user = $default_internal_user
}

service auth-worker {
  # Auth worker process is run as root by default, so that it can access
  # /etc/shadow. If this isn't necessary, the user should be changed to
  # $default_internal_user.
  #user = root
}

service dict {
  # If dict proxy is used, mail processes should have access to its socket.
  # For example: mode=0660, group=vmail and global mail_access_groups=vmail
  unix_listener dict {
    #mode = 0600
    #user =
    #group =
  }
}
```
6. Edit 10-ssl.conf :
```bash
vi /etc/dovecot/conf.d/10-ssl.conf
```

```yml
## SSL settings
# SSL/TLS support: yes, no, required. <doc/wiki/SSL.txt>
ssl = yes

ssl_cert = </etc/dovecot/private/dovecot.pem
ssl_key = </etc/dovecot/private/dovecot.key
```


7. Edit 10-auth.conf :
```bash
vi /etc/dovecot/conf.d/10-auth.conf
```

```yml
## Authentication processes

# Disable LOGIN command and all other plaintext authentications unless
# SSL/TLS is used (LOGINDISABLED capability). Note that if the remote IP
# matches the local IP (ie. you're connecting from the same computer), the
# connection is considered secure and plaintext authentication is allowed.
# See also ssl=required setting.
disable_plaintext_auth = no


# Space separated list of wanted authentication mechanisms:
#   plain login digest-md5 cram-md5 ntlm rpa apop anonymous gssapi otp
#   gss-spnego
# NOTE: See also disable_plaintext_auth setting.
auth_mechanisms = plain

##
## Password and user databases

!include auth-system.conf.ext

```


8. Aller dans le répertoire private :
```
cd /etc/dovecot/private/
```
8. Voir le contenu :
```
ls
```
9. Démarrer le service dovecot avec :
```
service dovecot restart
```
10. Voir le statut du service dovecot :
```
service status
```
ou

```
systemctl status dovecot
```
![Test dovecot](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/74b0841a-45f9-4f0d-a156-653b93fa1be9)


# 13-Test du service Dovecot :

```bash
echo "Test LOMBARD" | mail -s "Test Lombard CLI" lombard@ns.local
```
```bash
root@ubuntu-server:/home/lombard/Maildir/cur# cat 1712686749.Vfd00I8009eM814624.ubuntu-server\:2\,


Return-Path: <root@ubuntu-server>
X-Original-To: lombard@ns.local
Delivered-To: lombard@ubuntu.ns.local
Received: by ubuntu.ns.local (Postfix, from userid 0)
	id C64E520E8F; Tue,  9 Apr 2024 18:19:09 +0000 (UTC)


Subject: Test Lombard CLI Patrice Langlois
To: <lombard@ns.local>
User-Agent: mail (GNU Mailutils 3.14)
Date: Tue,  9 Apr 2024 18:19:09 +0000
Message-Id: <20240409181909.C64E520E8F@ubuntu.ns.local>
From: root <root@ubuntu-server>

Test LOMBARD
```

![Screenshot 2024-04-08 at 10 49 31 PM](https://github.com/Plangloi/420-AJ5-RO_DE-PLOIEMENT-DES-SERVICES-WEB-Linux/assets/48372629/f955fa5a-ddcb-40d3-9f51-929c135b6922)

