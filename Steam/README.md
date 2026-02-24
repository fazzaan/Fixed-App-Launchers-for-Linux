# Steam launcher

## The command
First, test my launch command. If it works for you, then use it directly; otherwise, do some further research and testing to make a command that works on your machine.  

Try running this:  
`env -u GDK_IM_MODULE -u GTK_IM_MODULE -u WAYLAND_DISPLAY GDK_BACKEND=x11 /usr/bin/steam %U`  

Did it work?  

If yes, then keep going:

## The terminal alias
Second, bind the command to a short word to launch in your terminal.  
This step isn't required, but if you use a terminal often, it makes sense to do so.  
Note that this method is for the fish command-line shell.  

`alias --save fix-steam 'env -u GDK_IM_MODULE -u GTK_IM_MODULE -u WAYLAND_DISPLAY GDK_BACKEND=x11 /usr/bin/steam %U'`  

Replace `fix-steam` with whatever you like, and the `env...` part with whatever launch command worked for you.  

## The launcher in your app menu

This is the part that integrates it into your desktop shell.  
It's a .desktop file, and it lives in your OS's filesystem.  
You can have your own version of the .desktop file and customise it to your liking.  
If you give it the same name, it will overrule the one from the OS.  

### Step 1. Copy the .desktop file

In a terminal, run  
`cp /usr/share/applications/steam.desktop ~/.local/share/applications/`  

### Step 2. Edit the .desktop file

Go to the Exec line in the .desktop file.  
For safety, _duplicate_ the line, and comment out the original one. That means add a # before it.  
Now, replace the command `steam` with your new command -- the long one starting with `env`, not the short alias you made (that only works in the terminal).  

The Steam .desktop file has loads of entries, shortcut links to different parts of the steam app, which appear in the desktop launcher's menu. Once the app is running, these will all work fine. But if you like to use those menu items to _launch_ Steam, you'll need to replace the `steam` command with the `env` command string in _all_ of them.  

### Step 3. Test the .desktop file

Hit save, then go to your terminal and run this command:  
`desktop-file-validate .local/share/applications/steam.desktop`  
This should reveal if you made any errors in the .desktop file.  
There are hints, warnings and errors.  
Actually, some of the errors can be ignored too.  
Try it out and see what happens.  

### Step 4. Launch the .desktop file

So there's no way to launch a .desktop file from itself, but the desktop shell can do it, and usually there's a user-facing command too. In GNOME/GTK, there's the command `gtk-launch`. Use it like so:  
`gtk-launch steam`  
And if you've done it right, this should launch successfully!  

### Step 5. Update the desktop apps database

This step isn't strictly necessary, as the desktop shell should update itself periodically, but in my experience it can sometimes be slow to update after you save your custom .desktop file.  
To be sure that you're not accidentally launching an old version of the .desktop file from your desktop's app launcher, run this command in the terminal:  
`update-desktop-database ~/.local/share/application`  



And that should be it!
