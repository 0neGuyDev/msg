## What is msg?

`msg` is a simple script I use to produce nice and consistent messages, prefixed properly and what not, most of the looks are inspired from [pacman](https://wiki.archlinux.org/index.php/Pacman) and [yay](https://github.com/Jguer/yay)

Here's an example of how the messages can look:

```
$ msg --test

 Status message!
> Other message!
:: Action message!
Error: Error message!
==> Action Warn message!
==> Action Info message!
Success: Success message!
Warning: Warning message!
 -> Notice message!
(1/5) Progress message!
```

All of them having customizable colors and prefixes, meaning if you don't want the error message to have "Error:" as it's prefix you can change it (At least you'll be able to soon...) currently it's handled as the third argument (this'll likely change to env variables), however certain messages can't be configured (progress message)

The main objective of this was instead of creating functions inside all of my scripts for making good looking output I made this script to make sure they all have the same "design"/colors to them, without having it to be in every one of them, not to mention this can also be used interactively. 

<!-- I haven't switched it to POSIX sh yet, will do soon.
Furthermore if you have Dash or a minimal `/bin/sh` symlink 
-->

Outside of that you can also color the actual message with escape sequences. Meaning if you want part of the message red you can add `\e[31m` somewhere and to stop the red add `\e[0m` so `msg "An error occured in \e[31mscript\e[0m fix it" error` would produce and error message where the word "script" is in red. For more info on this read up on terminal codes, [here's](https://wiki.bash-hackers.org/scripting/terminalcodes) a good place to get a good grip on how it works.

## Options

As of right now the decision is to not have any command line arguments outside of `--test` which prints the example message shown above. Which also means all the customization won't be done with command line arguments. Instead it'll be done with environment variables (As mentioned before).

That way scripts unless they're evil won't be able to overwrite it as well. Overall the purpose is for you to be able to change it as the user and all scripts using `msg` gets changed as well.

However an issue arises if the user wants (as an example) their warning msg prefix to be "WARNING!!" instead of "Warning:" and a script needs to provide a different message that isn't an warning message but still needs to be in yellow. Lets say the script provides "Issue:" as the third argument, that'll change the "Warning:" to "Issue:"

But as you can guess this would mean when an error comes up it says "WARNING!!" but when this script uses it's own method it'll show just "Issue:" and it might seem out of place.

Perhaps the best idea is just to encourage developers not to provide their own prefix.

## How to install!

Currently there's no package on any package manager as I haven't bothered to make one, but I will sometime in the future probably. For now you'll have to copy the `msg` file from the repository and put it in a directory that's in your `$PATH`

A way of doing this that'll work for most people is by entering this command:
```
curl https://raw.githubusercontent.com/0neGal/msg/main/msg -o ~/.local/bin/msg | chmod +x ~/.local/bin/msg
```

However make sure `~/.local/bin/msg` is actually in your `$PATH` not to mention that it exists.

## Other info!

I'm currently thinking of porting this to Rust or C to make it a little bit (a lot) faster, as it's not very complicated, also this script needs a lot of refactoring, as it was originally only intended as a small script in my dotfiles.

If I were to port it this repo would be renamed to `msg-sh` and the port would then just become `msg` that is so all links, link to the better version. I'd then also archive this repo, as it'd be quite dumb to use it over a C/Dlang/Rust/Go or whatever rewrite.
