# Fixed App Launchers for Linux
 
Lately so many apps are failing to run.

Usually the problem is the variety of features in the desktop environment, rather than the apps themselves -- or it _is_ the apps, but only because they haven't yet caught up to whatever new standards (or lack thereof) one corner of the f/oss/gnu/linux community is running with. (E.g. wayland, nvidia, xdg-portals, mesa, vesa, all this kinda stuff.)

This repo is to contain the app launcher fixes that I've written for my computer, based on scraping together solutions from people around the web, forums, reddit, matrix, etc.

**Do note that these are what work for me, so may not work for you!**
**Also perhaps they'll give you some clues as to how to fix your situation.**

The fixes are mainly things like launch env commands and .desktop files.  

So far I have launchers for:
* Github Desktop app  
* Obsidian - a .desktop file that isn't included in the AppImage  
* Steam - it keeps crashing on launch recently, apparently due to either Arch's removal of lib32 libraries (there's a fix for that too but YMMV) or Nvidia's latest 590 driver (or both)  
* FontLab 8  


### Steam
Try running this:  
`env -u GDK_IM_MODULE -u GTK_IM_MODULE -u WAYLAND_DISPLAY GDK_BACKEND=x11 /usr/bin/steam %U`  

### GitHub Desktop
Try running this:  
`env -u GTK_IM_MODULE github-desktop`  


The commands are formatted for fish, but also work in bash.  
If they work, you can add them to your own .desktop launchers.  
To do so, copy the main .desktop file from your system's `/usr/share/applications` or `/usr/local/share/applications` folder into your home folder's `~/.local/share/applications` folder, then edit the new file.  
Change the `Exec` line to match the new command; or to match your own customised command if you had to tweak it to work for you.  

You can also save these as aliases for your terminal shell.  
In fish, this is done with:  
`alias --save alias-command 'full command to run'`  
