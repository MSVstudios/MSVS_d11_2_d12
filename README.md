# 1. Take a snapshot.
# (Assumed to be done via your server management interface)
# USE REAL TERMINAL

# 2. Update the Debian server
apt update && apt upgrade -y

# 3. Reboot if needed
# (Reboot command as needed)

# 4. Run apt autoremove
apt autoremove -y

# 5. Check free space on the server
df -h

# 6. List PHP packages to uninstall
apt list --upgradable | grep php

# 7. Create a file with PHP package names to uninstall
apt list --upgradable | grep php | cut -d/ -f1 > php_packages_to_remove.txt

# 8. Uninstall any PHP package
xargs apt remove -y < php_packages_to_remove.txt

# 10. Run apt autoremove
apt autoremove -y

# 11. Back up sources files
cp /etc/apt/sources.list /etc/apt/sources.list.bak
cp /etc/apt/sources.list.d/sury-php.list /etc/apt/sources.list.d/sury-php.list.bak

# 12. Install debian-archive-keyring
apt install debian-archive-keyring

# 13. Update the sources list from buster to bullseye
sed -i 's/buster/bullseye/g' /etc/apt/sources.list
sed -i 's/buster/bullseye/g' /etc/apt/sources.list.d/sury-php.list

# 14. Download and save the PHP GPG key
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg

# 15. Run apt-get autoremove --purge
apt-get autoremove --purge -y

# 16. Run apt update
apt update

# 17. Upgrade to version 11
apt upgrade --without-new-pkgs -y

# 18. Run apt full-upgrade
apt full-upgrade -y

# 19 
reboot
apt --purge autoremove

# 19. Check free space on the server again
df -h

# 20. Backup sources files for Bookworm upgrade
cp /etc/apt/sources.list /etc/apt/sources.list.bak11
cp /etc/apt/sources.list.d/sury-php.list /etc/apt/sources.list.d/sury-php.list.bak11

# 21. Update the sources list from bullseye to bookworm
sed -i 's/bullseye/bookworm/g' /etc/apt/sources.list
sed -i 's/bullseye/bookworm/g' /etc/apt/sources.list.d/sury-php.list

# 22. Run apt update for Bookworm
apt update

# 23. Run apt full-upgrade for Bookworm
apt full-upgrade -y

# 24. Run apt --purge autoremove
apt --purge autoremove -y

# 25. Reboot the server if needed
reboot
systemctl reboot

# 26. Reinstall packages
xargs apt install -y < php_packages_to_remove.txt

# 27. Reinstall Webmin repositories
curl -o setup-repos.sh https://raw.githubusercontent.com/webmin/webmin/master/setup-repos.sh
sh setup-repos.sh

apt update

rename inside  source.list 
non-free > non-free non-free-firmware

reisnstal 
proftpd
