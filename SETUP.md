webtier setup
=======

Local Installation:
-------------------

1. Setup a VM running Ubuntu >= 12.04

2. Clone this repo to your VM. (Location doesn't matter.)

3. Copy `./config.template` to `./config` and edit hostnames and credentials for your environment.

4. Run `sudo ./local-setup` to install and configure apache, php, and dependencies. You only need to run this once.

5. Run `sudo ./install` to install webtier itself. You can run this repeatedly without harm, and should re-run it whenever webtier config files change.

5.1. Beer!

Some extra VM notes:
--------------------

1. If your local webtier will be connecting to other components in eng (RDS, Rainking), you'll need to make sure it's connected to the Temboo VPN. You can accomplish this using bridged networking to a host OS on the VPN, or you can setup a VPN client inside your VM. To help with the latter method `local-setup` installs `vpnc`, but does not configure it. See `/etc/vpnc/default.conf` for more.

2. Git makes it very easy to push or pull changes from separate copies of the repo on your host and guest OSes... but if you're lazy like me, you probably want a single shared filesystem to skip this step. To accomplish this in VirtualBox (methods will differ for other VM software) I cloned the repo to OS X, then set it up as a "shared folder" inside Ubuntu, mounted (with the VirtualBox Guest Utilities) at `/media/sf_webtier`. I then had to add the `www-data` user to the `vboxsf` group (and restart apache) before it could read the files. I also ran the following inside my webtier repo: `git config core.filemode false` -- otherwise VirtualBox's tinkering with shared folder file modes caused Ubuntu's git to think every file had changed.
