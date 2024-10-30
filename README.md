# Set-up your own SMB server on Linux

I am a linux user (not that it matters but it helps the sceneario) and recently I’ve been looking for ways to transfer files ( documents and media ) from my Iphone onto my linux machine.
I spent some time searching for solutions on google but all of them required using third party software (which is okay) I even went as far as to download one of these apps to try but it just didn’t work maybe I did something wrong but after hours of trying, I still could not get it to work so, I had to look for other alternatives. And so for the fifth time in my life I had to put my networking knowledge to use. This is how to setup a SMB server on your linux machine for transferring files between your iphone and your linux machine. I should also mention that this tutorial is “technical” and that normal users could follow along if they have minimal knowledge on how computer network operate and how Samba works :)

1. Install samba on your linux machine ( sudo apt install samba ).
2. Now let us create a directory in your user home folder and name it sambashare ( mkdir sambashare ) 
3. We’d then need to add the share’s directory to the smb.config file. You can use your favorite text editor to do this. 
   sudo vim / etc/ samba / smb.config

4. Add the following to the end of the config file and save (make sure to replace user with the current user’s:
     [sambashare]
	comment = First Share
	path = / home / <user> / sambashare
	read only = no
	browsable = yes
	
5.   Now let’s set a password for our new smb user :
	sudo smbpasswd -a <user>

6.   Now samba must be allowed through the firewall :

	sudo ufw allow samba

7.   Restart smbd :
	sudo service smbd restart

<picture>
 <source media="(prefers-color-scheme: dark)" srcset="YOUR-DARKMODE-IMAGE">
 <source media="(prefers-color-scheme: light)" srcset="YOUR-LIGHTMODE-IMAGE">
 <img alt="YOUR-ALT-TEXT" src="YOUR-DEFAULT-IMAGE">
</picture>


