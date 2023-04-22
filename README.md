# Description
Send WhatsApp Images/Videos/PDF/Documents/Voice Messages automatically using Tasker.

Previous post intro:-

>Recently I've been getting a lot of inquiries on how to send images, videos or documents in WhatsApp using Tasker. Possibly with the screen off, phone locked, without unlocking, etc. Had some time to make this so here it is.

# Details
Contains assets that are used for running mdtest directly in Tasker, without needing Termux.

Made for Project V3.

# Disclaimer
You are responsible for what you do with this.

# Instructions
### For Tasker Users
Check this Tasker Reddit **[post](https://www.reddit.com/r/tasker/comments/11wi2om/project_share_sendreceive_whatsapp_message/)** for more info and importable Taskernet links.

### For CLI Users
**NOTE:-**
>This section is helpful for those who want to make shell scripts to use `mdtest` to send messages. Not recommended for Tasker beginners since there are ready made Taskenet links in the Tasker Reddit Post that you can import.

The previous **Project V2** was made with solely Tasker in mind and didn't have CLI support.

I'm adding preliminary CLI support with some improvements in this **Project V3**.

#### CLI In Tasker
Added preliminary CLI support to run `mdtest` from within Tasker itself using action [Run Shell].

1\) Set it up as described in this Tasker Reddit **[post](https://www.reddit.com/r/tasker/comments/11wi2om/project_share_sendreceive_whatsapp_message/)**.

This will prepare Tasker to enable CLI support natively.

Your [Run Shell] action to use `mdtest` will look like this -

    #!/system/bin/sh
    cd /data/data/net.dinglisch.android.taskerm/files/whatsmeow3/mdtest
    sh ./mdtest COMMAND PARAMETERS

And your [Run Shell] action to use `ffmpeg`(check [this](https://github.com/HunterXProgrammer/Tasker-mdtest#note-about-audio-messages)) will look like this -

    #!/system/bin/sh
    sh /data/data/net.dinglisch.android.taskerm/files/whatsmeow3/ffmpeg/ffmpeg -y -i "/path/to/input/file" -codec:a libopus -ac 1 -ar 48000 -f ogg "/path/to/output/file"
    ##

Check **[Commands And Parameters](https://github.com/HunterXProgrammer/Tasker-mdtest#commands-and-parameters)** for more info about the available CLI commands.

#### CLI In Termux
CLI Setup:-

1\) Install and open [Termux](https://f-droid.org/en/packages/com.termux/) in your device.

2\) Grab the pre-compiled  binary from **[releases](https://github.com/HunterXProgrammer/Tasker-mdtest/releases/tag/mdtest-V3-assets)** or use the build script to compile it yourself in Termux.

**Eg:-** Depending on your device architecture(use `uname -m` to find out), you can download for `arm`,`arm64`(aarch64),`x86` and `x86_64` like this -

    arch=arm64 && curl -s -L -O "https://github.com/HunterXProgrammer/Tasker-mdtest/releases/download/mdtest-V3-assets/mdtest-${arch}.zip" && mkdir -p ~/whatsmeow3/mdtest && unzip -o -d ~/whatsmeow3/mdtest mdtest-${arch}.zip && chmod -R 700 ~/whatsmeow3/mdtest

OR

You can build and compile it by yourself in Termux using the build script -

    pkg upgrade -y

&nbsp;

    curl -s -L "https://github.com/HunterXProgrammer/Tasker-mdtest/releases/download/mdtest-V3-assets/install_whatsmeow3_termux.sh" | bash

3\) After that confirm WhatsApp qr code like this -

>Now to connect it to WhatsApp -
>
>Type -
>
>`cd ~/whatsmeow3/mdtest && ./mdtest`
>
>to check if WhatsApp qr code is generated properly.
>
>**Note:-** In case qr code is too big, you can pinch the screen to resize it.
>
>The code refreshes every 60s, so quickly take a picture of it using a spare phone and
>
>open WhatsApp -> ⋮ (menu) -> Linked Devices
>
>and scan this code in the main device.

This finishes the CLI setup.

Your script will look like this -

    #!/data/data/com.termux/files/usr/bin/bash
    cd ~/whatsmeow3/mdtest
    ./mdtest COMMAND PARAMETERS

### Commands And Parameters

The **COMMAND** and **PARAMETERS** are:-

    appstate <types...>
    request-appstate-key <ids...>
    checkuser <phone numbers...>
    subscribepresence <jid> 
    presence <available/unavailable>
    chatpresence <jid> <composing/paused> [audio]
    getuser <jids...>
    getavatar <jid> [existing ID] [--preview] [--community]
    getgroup <jid>
    subgroups <jid>
    communityparticipants <jid>
    getinvitelink <jid> [--reset]
    queryinvitelink <link>
    querybusinesslink <link>
    acceptinvitelink <link>
    setdisappeartimer <jid> <days>
    send <jid> <text>
    sendpoll <jid> <max answers> <question> -- <option 1> / <option 2> / ...
    react <jid> <message ID> <reaction>
    revoke <jid> <message ID>
    senddoc <jid> <document path> <title> [mime-type]
    sendvid <jid> <video path> [thumbnail path]
    sendaudio <jid> <audio path>
    sendimg <jid> <image path> [thumbnail path] [caption <note: if sending caption without specifying "thumbnail path", then put "null" in it's place.>]
    setstatus <message>
    sendbutton <jid> <title> <text body> <footer> <button1> [button2] [button3] (Note: [] is optional)
    sendlist <jid> <title> <text body> <footer> <button text> <list header> <list title 1> <list description 1> [list title X] [list description X] (Note: Upto 15 item pairs. [] is optional)
    markread <jid> <message ID 1> [message ID X] (Note: Can add multiple message IDs to mark as read. [] is optional)

The **"<>"** means required and the **"[ ]"** means optional.

#### Note About JID
For single contacts, JID is usually the country-code followed by the phone-number and appended with "@s.whatsapp.net".  
**Eg:-** Say country-code is "91", then JID will be ->  
919876543210@s.whatsapp.net

For group contacts, JID is usually the group phone-number appended with "@g.us".  
**Eg:-** 1234567890987654321@g.us

#### Note About Audio Messages
As explained **[here](https://www.reddit.com/r/tasker/comments/10wiahq/comment/j7q87s6/)** -

>About sending audio voice message, WhatsApp is extremely specific on what type of audio file it can accept.
>
>The audio file must be Mime-Type: application/ogg, audio/ogg, sent as audio/ogg; codecs=opus, Container: ogg and Codec: opus.
>
>So in case you want to send a mp3 file, you'd have to convert it into ogg with the above specifications.
>
>We will be using the versatile `ffmpeg` to convert the mp3,wav etc, audio files into ogg.

In Termux install `ffmpeg` using `pkg install -y ffmpeg` and then -

    ffmpeg -y -i "/path/to/input/file" -codec:a libopus -ac 1 -ar 48000 -f ogg "/path/to/output/file"

You can use this properly optimized output audio file in the voice messages.

# Credits
**[whatsmeow](https://github.com/tulir/whatsmeow) -** Go library `mdtest` is based on.

**[Termux](https://github.com/termux/termux-app) -** The best Android terminal. Allows compiling `mdtest` natively without needing PC or cross-toolchains. `ffmpeg` binaries used from here.

**[TermuxAm](https://github.com/termux/TermuxAm) -** Allows apps to use `am` command from user shell.

**[zoom](https://github.com/anitasv/zoom) -** Javascript library that allows making cool zoomable/rotatable Tasker webview Scenes.

**[Comment](https://www.reddit.com/r/tasker/comments/k0r7h9/comment/gdn5ovn/) by [OwlIsBack](https://www.reddit.com/u/OwlIsBack) -** Java functions used in Tasker to get per-line buffer of shell command.
