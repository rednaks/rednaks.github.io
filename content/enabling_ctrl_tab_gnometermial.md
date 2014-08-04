Title: Using Ctrl-Tab to switch between tabs in gnome-terminal
Date:  2013-07-25 15:46
Category: tweaks
Tags: linux, gnome, gnome-terminal, shortcut, hack, terminator


If you are like me using `Ctrl-Tab` (resp `Ctrlt-Shift-Tab`) to switch tabs in Firefox and you find that the default way to switch tabs is harmful, indeed, the default shortcuts are `Ctrl-PageUp` (resp `Ctrl-PageDown`). The two buttons are so far and you can’t really be fast in switching.

The good news is that you can customize it in preferences edition, but the bad news is that the Tab button is not allowed.

Gnome developers said that this is a reserved key by `GTK`. and this could not be considered as a bug.

Well I tried to force the values in the settings database and modified it manually using gsettings. and yes ! It works !

    :::bash
    $ gsettings set  org.gnome.Terminal.Legacy.Keybindings:/org/gnome/terminal/legacy/keybindings/ next-tab '<Primary>Tab'
    $ gsettings set  org.gnome.Terminal.Legacy.Keybindings:/org/gnome/terminal/legacy/keybindings/ prev-tab '<Primary><Shift>Tab'

So I don’t know if gnome developers are aware of that because they keep ignoring binding Tab key.

This was a little hack, that I wanted to share with you. If you don't want to bother yourself, there is a good alternative to gnome-terminal which is [Terminator (Terminal Emulator)](https://code.google.com/p/jessies/wiki/Terminator) with some great additional features.

