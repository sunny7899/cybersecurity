
Untold Windows Tips and Secrets By Ankit Fadia ankit@bol.net.in

Welcome to another Hacking Truths Manual. This time I have a collection of Tips and Tricks which no body normally knows, the secrets which Microsoft is afraid to tell the people, the information which you will seldom find all gathered up and arranged in a single file. To fully reap this Manual you need to have a basic understanding of the Windows Registry, as almost all the Tricks and Tips involve this file. 

****************

Important Note: Before you read on, you need to keep one thing in mind. Whenever you make changes to the Windows Registry you need to Refresh it before the changes take place. Simply press F5 to refresh the registry and enable the changes. If this does not work Restart your system

****************

Exiting Windows the Cool and Quick Way

Normally it takes a hell lot of time just Shutting down Windows, you have to move your mouse to the Start Button, click on it, move it again over Shut Down, click, then move it over the necessary option and click, then move the cursor over the OK button and once again (you guessed it) click.This whole process can be shortened by creating shortcuts on the Desktop which will shut down Windows at the click of a button. Start by creating a new shortcut( right click and select New> Shortcut). Then in the command line box, type (without the quotes.)

'C:\windows\rundll.exe user.exe,exitwindowsexec'

This Shortcut on clicking will restart Windows immediately without any Warning. To create a Shortcut to Restarting Windows, type the following in the Command Line box:

'c:\windows\rundll.exe user.exe,exitwindows'

This Shortcut on clicking will shut down Windows immediately without any Warning. 

Ban Shutdowns : A trick to Play on Lamers

This is a neat trick you can play on that lamer that has a huge ego, in this section I teach you, how to disable the Shut Down option in the Shut Down Dialog Box. This trick involves editing the registry, so please make backups. Launch regedit.exe and go to 

HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer

In the right pane look for the NoClose Key. If it is not already there then create it by right clicking in the right pane and selecting New > String Value.(Name it NoCloseKey ) Now once you see the NoCloseKey in the right pane, right click on it and select Modify. Then Type 1 in the Value Data Box.

Doing the above on a Win98 system disables the Shut Down option in the Shut Down Dialog Box. But on a Win95 machine if the value of NoCloseKey is set to 1 then click on the Start > Shut Down button displays the following error message:

This operation has been cancelled due to restrictions in effect on this computer. Please contact your system administrator.

You can enable the shut down option by changing the value of NoCloseKey to 0 or simply deleting the particular entry i.e. deleting NoCloseKey.

Instead of performing the above difficult to remember process, simply save the following with an extension of .reg and add it's contents to the registry by double clicking on it.

REGEDIT4

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer]

"NoClose"="1"

Disabling Display of Drives in My Computer

This is yet another trick you can play on your geek friend. To disable the display of local or networked drives when you click My Computer go to :

HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer

Now in the right pane create a new DWORD item and name it NoDrives. Now modify it's value and set it to 3FFFFFF (Hexadecimal) Now press F5 to refresh. When you click on My Computer, no drives will be shown. To enable display of drives in My Computer, simply delete this DWORD item. It's .reg file is as follows:

REGEDIT4

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer]

"NoDrives"=dword:03ffffff

Take Over the Screen Saver

*(Not Check) To activate and deactivate the screen saver whenever you want, goto the following registry key:

HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\ScreenSavers

Now add a new string value and name it Mouse Corners. Edit this new value to -Y-N. Press F5 to refresh the registry. Voila! Now you can activate your screensaver by simply placing the mouse cursor at the top right corner of the screen and if you take the mouse to the bottom left corner of the screen, the screensaver will deactivate. 

Pop a banner each time Windows Boots

To pop a banner which can contain any message you want to display just before a user is going to log on, go to the key:

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\WinLogon

Now create a new string Value in the right pane named LegalNoticeCaption and enter the value that you want to see in the Menu Bar. Now create yet another new string value and name it: LegalNoticeText. Modify it and insert the message you want to display each time Windows boots. This can be effectively used to display the company's private policy each time the user logs on to his NT box. It's .reg file would be:

REGEDIT4

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Winlogon]

"LegalNoticeCaption"="Caption here."

Delete the Tips of the Day to save 5KB

Windows 95 had these tips of the day which appeared on a system running a newly installed Windows OS. These tips of the day are stored in the Windows Registry and consume 5K of space. For those of you who are really concerned about how much free space your hard disk has, I have the perfect trick.

To save 5K go to the following key in Regedit:

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Tips

Now simply delete these tricks by selecting and pressing the DEL key.

Change the Default Locations

To change the default drive or path where Windows will look for it's installation files, go to the key:

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Setup\SourcePath

Now you can edit as you wish.

Secure your Desktop Icons and Settings

You can save your desktop settings and secure it from your nerdy friend by playing with the registry. Simply launch the Registry Editor go to:

HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer

In the right pane create a new DWORD Value named NoSaveSettings and modify it's value to 1. Refresh and restart for the settings to get saved.

CLSID Folders Explained

Don't you just hate those stubborn stupid icons that refuse to leave the desktop, like the Network Neighborhood icon. I am sure you want to know how you can delete them. You may say, that is really simple, simply right click on the concerned icon and select Delete. Well not exactly, you see when you right click on these special folders( see entire list below)neither the rename nor the delete option does not appear. To delete these folders, there are two methods, the first one is using the System Policy Editor(Poledit in the Windows installation CD)and the second is using the Registry.


