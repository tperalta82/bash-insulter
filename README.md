# bash-insulter
Randomly insults the user when typing wrong command.

Change insults as needed :)

```bash
noob@bender:~ $ sl

  Y u no speak computer???

-bash: sl: command not found
noob@bender:~ $ gti status

  This is why nobody likes you.

-bash: gti: command not found
noob@bender:~ $ sp aux

  Go outside.

-bash: sp: command not found
```

# Compatibility
* Bash v4 and newer
* Zsh

# Installation

    # Install google-speech Python3 library
    pip3 install google-speech
    
    # Clone this repo, add a softlink in /etc, and add permissions
    sudo ln -sf bash-insulter/src/bash.command-not-found /etc/bash.command-not-found
    chmod u+x bash-insulter/src/bash.command-not-found

    sudo apt-get install sox libsox-fmt-mp3 streamer imagick

Then source the file automatically for new logins by adding the following to `/etc/bash.bashrc` or any of the other locations where you can configure your shell automatically during login (zsh have different config files):
```
if [ -f /etc/bash.command-not-found ]; then
    . /etc/bash.command-not-found
fi
```
Login again and type some invalid commands for the effects to be audible.

# Configuration
bash-insulter can be customized, or even be made polite and nice, by populating `CMD_NOT_FOUND_MSGS` or `CMD_NOT_FOUND_MSGS_APPEND` environment variables. The values should be arrays. `CMD_NOT_FOUND_MSGS` replaces the default messages, while `CMD_NOT_FOUND_MSGS_APPEND` appends more messages to the existing ones.

It is probably cleanest to source a file populating the environment variable as needed. In this example I create a file `/etc/bash.command-not-found-messages` with the following content:

    CMD_NOT_FOUND_MSGS=(
        "You are so smart!"
        "You look pretty today!"
        "I don't know what to say"
    )
    
Then source this file before you source the script:
```
if [ -f /etc/bash.command-not-found-messages ]; then
    . /etc/bash.command-not-found-messages
fi

if [ -f /etc/bash.command-not-found ]; then
    . /etc/bash.command-not-found
fi
```

Then logout and in again. The end result is that you will now use your messages instead of the default ones.
