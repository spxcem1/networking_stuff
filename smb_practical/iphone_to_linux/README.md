# Set-up your own SMB server on Linux

I am a linux user (not that it matters but it helps the sceneario) and recently I’ve been looking for ways to transfer files ( documents and media ) from my Iphone onto my linux machine.
I spent some time searching for solutions on google but all of them required using third party software (which is okay) I even went as far as to download one of these apps to try but it just didn’t work maybe I did something wrong but after hours of trying, I still could not get it to work so, I had to look for other alternatives. And so for the fifth time in my life I had to put my networking knowledge to use. This is how to setup a SMB server on your linux machine for transferring files between your iphone and your linux machine. I should also mention that this tutorial is “technical” and that normal users could follow along if they have minimal knowledge on how computer network operate and how Samba works :)

## Set-up Samba on your Linux Machine
1. Install samba on your linux machine
	```
 	sudo apt install samba.
	```
2. Now let us create a directory in your user home folder and name it sambashare
 	```
 	mkdir sambashare
  	``` 
3. We’d then need to add the share’s directory to the smb.config file. You can use your favorite text editor to do this. 
	```
   	sudo vim / etc/ samba / smb.config
	```
4. Add the following to the end of the config file and save (make sure to replace <user> with your current user’s)
	```
 	[sambashare]
	comment = First Share
	path = / home / <user> / sambashare
	read only = no
	browsable = yes
	```
5.   Now let’s set a password for our new smb user :
        ```
        sudo smbpasswd -a <user>
        ```  	
	
6.   Now samba must be allowed through the firewall :
        ```
        sudo ufw allow samba
        ```
7.   Restart smbd :
        ```
        sudo service smbd restart
        ```

Now you should have SMB up and running with your smb share ready to share files. Obviously your SMB share would be empty since you haven't conducted any transfers. So now let's turn our attention to your iphone.


## Connecting Your Iphone To Your Linux Machine via SMB

I don't know about you but my iOS is a bit dated 😅 but not that old. I'm using an iphone 8 which is running iOS 16.7.10, oh come on there couldn't be that much that has changed right?😐
But I'm sure regardless of your iOS version ( as long as it's >= to mine ) would work for this tutorial, hopefully.

1.   Open <b>Files</b>> on your iphone ( this thing ⬇️ )
     

        ![icon-files-download-28](https://github.com/user-attachments/assets/a5149f94-67c5-47d5-9f8a-7126e6ca4daa)
   
2.   Now I'll be using screenshots to illustrate what to do from here on out ( and a little bit of explanation ). <b>Files</b> is the default file manager for iOS but it has a feature that allows us to connect to a server on the same network. Opening <b>Files</b> for the first time should look something like the pic below.

   
        ![pic11](https://github.com/user-attachments/assets/cdad96cb-9517-436b-b58e-7cc11a940112)

3.   Now tap on the three dots at the upper right corner of the screen and select <b>Connect to Server</b>

	

        ![photo_5843854437515379853_y](https://github.com/user-attachments/assets/dda31496-6488-4044-8db5-9798aef2d48e)

4.   Okay now we should have a panel to type in our server's IP. Now let's see if our smb server setup was worth it.
        ```
        smb://<SMB server IP>/<smb_share>
        ```
5.   The above illustration is the format we'd have to follow if we were to connect to our SMB server via our Iphone. In this case my server would obviously have a different IP so make sure you know your server's IP, and the smb share.
     The image below illustrates how I would connect to my SMB server from my Iphone :
     
     ![gog1](https://github.com/user-attachments/assets/7cac114a-724f-49a5-a8b8-110a8386395d)

6.   Once you're done with that, tap <b>Connect</b>. The next screen prompts us for whom we would like  to "connect as" and  since I didn't set up a guest user for samba, we'll be connecting as a <b>Registered User</b>. Note that the registered user is your current         user you used to set-up the smb server on your linux machine. Below is how I would connect to my server :

     
     ![gog2](https://github.com/user-attachments/assets/a76f6fa9-d137-49a9-b212-11c7929a8312)

7.   After typing in your registered username and password, tap <b>Next</b> to finally connect to your smb server. You should see your previously created smb share on your iphone. You can treat this share as any other folder in your Files such as your       Downloads folder, Icloud folder, etc you can copy and paste or even move any file or folder into the share and it would immediately upload to the server ( depending on the size of the files ) and you'd see it show up in the smb share on your            linux machine.

Below I'd like to send a bunch of files from my Iphone onto my linux machine.

![again1](https://github.com/user-attachments/assets/e004d4cf-83b8-448f-a260-8728145ff144)


I've put them all in a single folder.

Now I'd copy the directory/folder and paste it into the smb share ( sambashare ) 


![photo_5843854437515379882_y](https://github.com/user-attachments/assets/8de4eb9f-c9d9-4edd-bd5d-f6321ac15f7d)


![photo_5843854437515379880_y](https://github.com/user-attachments/assets/f884d4bd-cc8e-412d-9826-5a279d268a38)

After the upload is done, we can see that the folder is now present in the share on our phone.


![photo_5843854437515379879_y](https://github.com/user-attachments/assets/121d9207-f4fd-4eaa-af97-2a91aaf6153a)

Now let's see if the uploaded files would show up on our linux machine.

![jjj](https://github.com/user-attachments/assets/78a468a4-398e-471b-8662-4badb721ba6b)



Yes, yes it worked, on the left you can see the uploaded folder in our  samba share and on the right you can see the files in that folder.


 And that is how you can transfer files between your Iphone and your linux machine...
 Later ✌️
