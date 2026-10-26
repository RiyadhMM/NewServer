# newserver: building and securing an Ubuntu server from scratch

**Status: in progress (started October 2026).** I'm building a Linux server step by step to learn how to set up, secure and rebuild a server the way a sysadmin would. Every config file I write goes in this repository.

## What I have done so far 

- Ubuntu Server 26.04 LTS in a VirtualBox VM. SSH and web are port-forwarded to `127.0.0.1` only, so nothing outside my PC can reach them.
- A named admin user `ops` with sudo, instead of logging in as root. Root logins removed
- SSH key login (ed25519), with root login and password login turned off: [`config/ssh/10-security.conf`](config/ssh/10-security.conf)
- Checked with `sshd -T` that my settings are the ones in use. A forced password login gets `Permission denied (publickey)`.

#**Something I learned ** Ubuntu installer adds `/etc/ssh/sshd_config.d/50-cloud-init.conf`, which turns password login back on. OpenSSH reads these files in name order and the first value wins, so I named my file `10-...` to load first over the '50', then that overided ubuntus file.

## Next

- [ ] ufw firewall (only SSH and web open)
- [ ] fail2ban for SSH
- [ ] Automatic security updates
- [ ] nginx website with security headers
- [ ] Nightly backups, plus a restore test
- [ ] A status page
- [ ] `setup.sh` to rebuild the whole server from this repo
