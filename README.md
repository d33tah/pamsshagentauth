DO NOT USE THIS FORK
====================

This is for experimental purposes only. Please do not use this fork.

Old contents of the README:
===========================

pam_ssh_agent_auth is a PAM module which permits PAM authentication via your
keyring in a forwarded ssh-agent.

Release 0.10.2 is stable, and has been tested on FreeBSD, Solaris 10, Solaris 11,
RHEL5, RHEL6, Debian Wheezy, Ubuntu 12.04 (LTS), Ubuntu 13.10,
and MacOS X 10.7.

This module can be used to provide authentication for anything run locally that
supports PAM. It was written specifically with the intention of permitting
authentication for sudo without password entry, and also has been proven useful
for use with su as an alternative to wheel.

It serves as middle ground between the two most common, and suboptimal
alternatives for large-scale system administration: allowing rootlogin via ssh,
or using NOPASSWD in sudoers. This module allows for ssh public-key
authentication, and it does this by leveraging an authentication mechanism you
are probably already using, ssh-agent.

There are caveats of course, ssh-agent forwarding has it’s own security risks
which must be carefully considered for your environment. In cases where there
are not untrustworthy intermediate servers, and you wish to retain traceability,
accountability, and required authentication for privileged command invocation,
the benefits should outweigh the risks. Release 0.10.2 can be downloaded from
SourceForge: https://sourceforge.net/project/showfiles.php?group_id=249556

If you encounter any issues with usability or security, please use the project's
SourceForge tracker:
https://sourceforge.net/tracker2/?group_id=249556&atid=1126337

Note that if you wish to use this for sudo, you will need a version of sudo that
preserves the env_keep environment during authentication; and ideally a version
incorporating my minor patch which ensures RUSER is set during PAM authentication.

sudo 1.6.8p12 does not work correctly with this PAM module, because it clears the
environment (even env_keep variables) prior to attempting PAM authentication.

sudo 1.7.2p1 or later is preferred, as it correctly sets PAM_RUSER for
authentication.
