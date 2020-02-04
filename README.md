# Telephonic-Server-Asterisk
How to setup telephonic server in linux (Centos)

Telephonic Server Asterisk 

 

1. Disable SELinux in Centos. 

#  vim /etc/selinux/config 

#   SELINUX=disable 

 

2. Install Required Packages 

#  yum install -y epel-release dmidecode gcc-c++ ncurses-devel libxml2-devel make wget openssl-devel newt-devel kernel-devel sqlite-devel libuuid-devel gtk2-devel jansson-devel binutils-devel libedit libedit-devel 

 

3. Create user for Asterick 

# adduser asterisk -c "Asterisk User" 

# passwd asterisk    // change pass “master” 

# usermod -aG wheel asterisk 

# su asterisk 

 

4. Create a temporary directory 

# mkdir ~/build && cd ~/build 

 

5. PJSIP download page and grab the package 

    make sure to use the latest version: 

# wget https://www.pjsip.org/release/2.9/pjproject-2.9.tar.bz2 

# tar xvjf pjproject-2.9.tar.bz2 

# cd pjproject-2.9 

# ./configure CFLAGS="-DNDEBUG -DPJ_HAS_IPV6=1" --prefix=/usr --libdir=/usr/lib64 --enable-shared --disable-video --disable-sound --disable-opencore-amr 

 

6. Check errors or warnings. All dependencies are installed: 

# make dep 

7. Link Lib 

# make && sudo make install && sudo ldconfig 

8. Ensure that all libraries are installed 

# ldconfig -p | grep pj 

 

Install Asterisk on CentOS 

 

1. Asterick Installation  

# cd ~/build 

# wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-16-current.tar.gz 

# tar -zxvf asterisk-16-current.tar.gz 

# cd asterisk-16.5.1 

2. Enable mp3 support to play music (Optional Step) 

# sudo yum install svn 

# sudo ./contrib/scripts/get_mp3_source.sh 

3. Run the configure script to prepare the package for compiling 

# sudo contrib/scripts/install_prereq install 

# ./configure --libdir=/usr/lib64 --with-jansson-bundle 

4. Install missing dependencies 

# yum install patch 

5. Re-run the configure script 

( Step 3) 

6. Start the build process 

# make menuselect 

7. Music on hold feature,enable the “format_mp3” feature from “Add-ons”  section. Save your list and run these command 

# make && sudo make install 

8. To install the sample configuration files 

# sudo make samples 

9. To start Asterisk on boot 

# sudo make config 

  

10. Update the ownership of the following directories and files 

  

# sudo chown asterisk. /var/run/asterisk 

# sudo chown asterisk. -R /etc/asterisk 

# sudo chown asterisk. -R /var/{lib,log,spool}/asterisk 

  

11. Test installation 

  

# sudo service asterisk start 

# sudo asterisk –rvv 

 

12. To see a list of available commands 

 

asterisk*CLI> core show help 

 

13. To exit the Asterisk prompt 

 

asterisk*CLI> exit 
