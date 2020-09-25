MBSync
=========

This is a pretty simple role intended to make it a little bit easier to manage
mbsync installs and configurations. If you want to manage your user account(s)
and mail access, this might be useful for you.

Requirements
------------

None.

Role Variables
--------------

All values are defined and documented in [defaults/main.yml](defaults/main.yml).

This role is meant to be used on a user account, so `mbsync_user` and
`mbsync_group` should be set to a real user. If the specified user doesn't
exist, the role will fail.

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: myworkstations
      roles:
         - role: dudefellah.mbsync
           mbsync_user: dudefellah
           mbsync_group: dudefellah
           mbsync_mbsyncrc_content: |
             # {{ ansible_managed }}
             Expunge None

             MaildirStore local
             Path ~/Mail/
             Subfolders Verbatim

             IMAPStore myemail
             Host imap.myemail.com
             User dudefellah@example.com
             PassCmd "sed -n -e 's,^machine imap\\.myemail\\.com login dudefellah@example.com password \\(.*\\),\\1,p' < $HOME/.netrc"

             Channel myemail
             Master :myemail:
             Slave :local:
             Expunge Slave
             Sync Pull All
             Patterns *

License
-------

GPLv2+

Author Information
------------------

Dan Thomson - https://github.com/dudefellah
