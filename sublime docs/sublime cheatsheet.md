# Sublime cheatsheet



## Command shortcuts


    ^M              - find matching brace


    ^ ⌘ G         - multi-select editing; select string, then hit ^ ⌘ G



## Cool basic features 

https://code.tutsplus.com/tutorials/sublime-text-2-tips-and-tricks-updated--net-21519

    CTRL `              - open console for IDE\debugging
    SHIFT ⌘ P         - command pallette
    ⌘ P               - file switching


Multi select 

    ⌘ select          - multi-select (editing changes at multiple cursors)
    OPT ⌘ G           - quick find (whatever is at the cursor)
    CTRL ⌘ G          - Use ⌘ + select to multi-select  
                        - CTRL ⌘ G to quick find all occurances of selection.

Goto Symbol

    ⌘ R               - go to definition of any symbol, including functions, variables, etc

Whole Word Searching

    ⌘ D               - selection is now for whole word

Emojis

    CTRL ⌘ Space      - emoji and unicode




## sublime bookmarks
https://packagecontrol.io/packages/Sublime%20Bookmarks

Adding Bookmarks

    ⌘ + SHIFT + P, select Sublimebookmarks | Add Bookmark  (^ SHIFT F2)  Type Name

Remove Bookmarks

    ⌘ + SHIFT + P, select Sublimebookmarks | Remove Bookmark


## emmett 

http://docs.emmet.io/actions/go-to-pair/

http://docs.emmet.io/ 

    Type html:5 and press Ctrl/⌘ + e, and it is expanded to a basic HTML 5 page template. Simple!



## Go to Matching Pair

<http://docs.emmet.io/actions/go-to-pair/>

    SHIFT + CTRL + T        



## Sublime Console

As strange as it is, I often forget that the _command_ textarea is located at 
the bottom of the console.  You can't type in the input area.  


## Custom Keybindings

Show/Create Key Bindings
Preferences | Key Bindings

Handling key binding conflicts
http://pandasauce.org/2013/04/fixing-broken-sublime-text-hotkeys/

In Sublime Console : 

    sublime.log_input(True)         # optional 
    sublime.log_commands(True)

Modify Keybindings
Preferences → Package Settings → Package Name → Key Bindings (Default)

If you can't edit the file, then use :
Open Command Pallette (Shift + ⌘ + P) | PackageResourceViewer | Open Resource | <package> Default.sublime-keymap

Just edit the file.  




