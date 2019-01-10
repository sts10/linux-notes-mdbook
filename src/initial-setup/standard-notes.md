# Setting up Standard Notes on Linux

First, let's [download Standard Notes for Linux](https://standardnotes.org/).

## Where to put the AppImage file? 

Here's one way that works: Create a directory at `~/standard-notes/` and move the AppImage file there. Also, go download a PNG of the Standard Notes logo and place it in this directory. 

## Creating the `.desktop` file

If you don't yet have a `.desktop` file for Standard Notes, we'll create one. At `~/.local/share/applications/standard-notes.desktop` paste the following:

```
[Desktop Entry]
Type=Application
Name=StandardNotes
Exec=/home/$USER/standard-notes/standard-notes-*-x86_64.AppImage 
Icon=/home/$USER/standard-notes/standard-notes.png
Terminal=false
Categories=Office;Notes;
```

Now, after a computer restart, Standard Notes should come up when you search your applications.

[More on desktop files in the Arch Wiki](https://wiki.archlinux.org/index.php/desktop_entries).
