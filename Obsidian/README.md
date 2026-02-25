# Obsidian launcher

Obsidian is available for Linux as an AppImage and other formats.  
If you're not using the Snap, Flatpak, Deb, or installing from Arch (or the AUR), then you'll have to use the AppImage, which means it won't automatically have a launcher entry in your desktop shell.  
This is partly due to AppImages, but also it is fixable by package developers (somehow, idk details); but don't hold your breath.  

### Arch notes:  
**If you're using either version from the Arch repositories, you don't need to follow my guide for a launcher! It will automatically install the launcher to your desktop's app drawer.**  
* The in-repo (extra) version is currently up to date (1.11.7), but I don't know how long this will be available, because Obsidian _is_ closed-source software. It is only 25MB as it appears to use the on-system version of Electron.  
* The AUR version is currently up to date (1.11.7), but AUR packages are notorious for being abandoned when their maintainers have had enough. Use with caution -- it might go out of date suddenly; in which case, return here and follow my guide for setting up the .desktop file.  


_Assuming you still want to make a .desktop file for your AppImage, please read on._  

First, make sure you've downloaded the Obsidian AppImage.  
Don't rename the AppImage file -- leave it as-is, so that you know what version you've got. That'll make it easier to update in the future.  
Instead, right-click on it and choose "make a link" or "create link" or similar.  
Now, rename the link file, to Obsidian.AppImage to match my .desktop file, or to one of your choosing.  
Put the link file where you want it.  
(I store all my non-installed apps in `~/Programmes`.)  

## The command
I have a Programmes folder in my /home/user folder where I put all my local apps, scripts and bits of software.  
If you didn't make a link to the AppImage called `Obsidian.AppImage` then you'll need to include the version number of the AppImage you downloaded.  

`Exec= sh -c 'exec "$HOME/Programmes/Obsidian.AppImage"'`  

If yours is in a different place inside your `Home` folder, update the .desktop file to match.  
`Exec= sh -c 'exec "$HOME/path/to/your/Obsidian.AppImage"'`  

## The terminal alias
Bind the command to a short word to launch in your terminal.  
This step isn't required, but if you use a terminal often, it makes sense to do so.  
Note that this method is for the fish command-line shell. (It might work for other shells too.)  

`alias --save obsidian-appimg $HOME/Programmes/Obsidian.AppImage`  

Replace `obsidian-appimg` with whatever you like.  

## The launcher in your app menu

This is the part that integrates it into your desktop shell.  
It's a .desktop file, and it lives in your OS's filesystem.  
You can have your own version of the .desktop file and customise it to your liking.  
If you give it the same name, it will overrule the one from the OS.  

### Step 1. Get a .desktop file

Download the Obsidian.desktop file from my repo. #todo [link it here]  

### Step 2. Put it in the right place

All .desktop files have to live in the right places to be discoverable.  
User .desktop files usually live in ~/.local/share/applications.  
* `~` is shorthand for `/home/your-username`. Most terminals understand and respect this symbol in file & folder addresses, but it isn't always parsed correctly in shell scripts (e.g. `.sh`) and .desktop files. That's why we used the convoluted `sh -c 'exec "$HOME/...` in this launcher.  

### Step 3. Point it to your AppImage

If you have done as I said at the start:  
* made the link to the file  
* renamed it to Obsidian.AppImage  
* put it in ~/Programmes  

... then you have just one more task to do -- add the icons! :)  

If you have done things your own way, then open up the `Obsidian,desktop` file and edit the `Exec=` command accordingly!  
Make sure that these are correct:  
* the address - `$HOME/path/to/your/file`  
* the filename - `Obsidian-whatever.AppImage`  

... then you also have just one more task to do -- add the icons! :)  

#todo [add steps to get icons from appimage - now it's gone 3AM]  

### Step 4. Test the .desktop file

Hit save, then go to your terminal and run this command:  
`desktop-file-validate .local/share/applications/steam.desktop`  
This should reveal if you made any errors in the .desktop file.  
There are hints, warnings and errors.  
Actually, some of the errors can be ignored too.  
Try it out and see what happens.  

### Step 5. Launch the .desktop file

So there's no way to launch a .desktop file from itself, but the desktop shell can do it, and usually there's a user-facing command too. In GNOME/GTK, there's the command `gtk-launch`. Use it like so:  
`gtk-launch steam`  
And if you've done it right, this should launch successfully!  

### Step 6. Update the desktop apps database

This step isn't strictly necessary, as the desktop shell should update itself periodically, but in my experience it can sometimes be slow to update after you save your custom .desktop file.  
To be sure that you're not accidentally launching an old version of the .desktop file from your desktop's app launcher, run this command in the terminal:  
`update-desktop-database ~/.local/share/application`  



And that should be it!
