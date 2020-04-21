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

