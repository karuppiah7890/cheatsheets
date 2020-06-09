# Mac OS

This is my cheatsheet for anything related to Mac OS

1. How do I lock my computer?

Use `Control + Command + Q`

Or use Alfred App and choose Lock option in it

2. How do I logout of my computer?

Use `Command + Shift + Q`

Or use Alfred App and choose Log Out option in it

3. How do I sleep, shutdown or restart my computer?

Use `Fn + Power Button` and choose your option to sleep / shutdown / restart

Or use Alfred App and choose Sleep / Shut Down / Restart option in it

4. How do I navigate to the extreme right end of a line or extreme left end?

Use `Command + Right arrow` for extreme right
Use `Command + Left arrow` for extreme left

5. How do I navigate to the top (starting) of a doc / file or bottom (ending)?

Use `Command + Up arrow` for top
Use `Command + Down arrow` for bottom

6. How do I navigate a line word by word towards right or left?

Use `Option + Right arrow` for navigating word by word to the right
Use `Option + Left arrow` for navigating word by word to the left

7. I try to update my Mac OS version using `Software Update` and click
`Update Now`. It does restart, but it never updates or gives any error! Why is
that?

I have noticed this to happen some two times now. I suspected the disk storage
space to be the issue - the OS not having enough free disk space in the system
to do it's upgrade automatically or even when you trigger manually. I fixed
this by checking my disk usage using `Disk Utility` and `Storage Management`.
Decrease it as much as possible to create more free disk space. The last time I
tried to upgrade, I made sure I had at least 15 - 16 GB free disk space - that
did the trick!

8. MacOS Catalina tells me "xyz" cannot be opened because the developer
cannot be verified. What do I do?

For binaries / executables, that is command line programs, this is what
I do in my terminal -

```
$ sudo xattr -d com.apple.quarantine <path-to-binary>
```

Apart from this, you can also go to `Security & Privacy` and then `General`
and look for a message saying `"abc" was blocked from use because it is
not from an identified developer` and there will be a button near it called
`Allow Anyway` to allow the program. You can click this button to allow
your program to run too! 

9. How to take screenshot of the whole screen?

Use `Command + Shift + 3`

10. How to take screenshot of a part of a screen?

Use `Command + Shift + 4` and select the part of the screen you want to
take screenshot of.

11. How to take screenshot of a particular window?

You can use the method mentioned in Q10 above, but it can be tedious to
select the whole window yourself when you can use your computer's help.

Use `Command + Shift + 4` first. Now you will see a cursor with a
selection symbol. Now press `Space` and you will see the symbol
turn into a camera symbol and when you hover over any window, that
window will turn blue to show it's on focus, and then press `Enter`
to take screenshot of the window.

This takes the screenshot of the window so beautifully - the screenshot
is padded with some background and the window has some shadow behind it
to give an elevation like feel. And the whole window can be clearly
seen, along with the title bar with close, minimize, full screen
buttons. It's just pretty!

12. How to do move around in a browser page in a page up and page down manner?
More like scrolling one page at a time

Use `Space` for down and `Shift + Space` for up in browsers and places wherever
it works :P Or you can use `Fn + Down` for down and `Fn + Up` for up

13. How to do delete function similar to windows delete key? That is, delete
things in front of the cursor

`delete` in MacOS works like `Backspace` in windows, yes - it deletes the
characters behind the cursor. To delete characters in front of the cursor,
use `Fn + delete` :)

14. How to minimize window with keyboard shortcut?

Usually the shortcut `Command + M` works in most MacOS applications.

15. How to maximize window with keyboard shortcut?

When there's window of the application and it's been minimized, you can use
`Command + Tab` to focus on the application, and let go of the `Tab` key press
after focussing on the application, but don't let go of the key press of
`Command` while doing this, while having `Command` key pressed, press `Option`
key too and then let go of the `Command` key to see the window get maximized.

16. How to find the definition of a word in Spotlight using Dictionary app?

Many results will be shown. To move to the definition, use `Command + L` to
reach the definition result showing dictionary app result
