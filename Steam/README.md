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

## The launcher icon

This is the part that integrates it into your desktop shell.  
It's a .desktop file, and it lives in your OS's filesystem.  
You can have your own version of the .desktop file and customise it to your liking.  
If you give it the same name, it will overrule the one from the OS.  

### Step 1. Copy the .desktop file

In a terminal, run  
`cp /usr/share/applications/steam.desktop ~/.local/share/applications/`
