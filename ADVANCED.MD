# Buttons And List Messages Discontinued

Unfortunately several library creators have decided to deprecate sending buttons and list messages due to WhatsApp(Meta) proactively unfixing their fixes.

You can read more about it here:-

**[GitHub - Issue #56](https://github.com/WhiskeySockets/Baileys/issues/56#issuecomment-1542947921)**

This should only affect buttons and list messages. Other messages should work fine.

If it is fixed in the future, I'll add it back.

&nbsp;

# Description
This Section is recommended for advanced Tasker and Termux users.

As mentioned **[here](https://github.com/HunterXProgrammer/Tasker-mdtest#description)**, the **Base [Mdtest Project V3](https://www.reddit.com/r/tasker/comments/11wi2om/project_share_sendreceive_whatsapp_message/)** covers sending **WhatsApp Text/Images/Videos/PDF/Documents/Voice Messages**.

And this **Advanced Mdtest V3** section is an extension to the base **Mdtest Project V3**, which gives additional features like sending/receiving WhatsApp Button Messages, List Messages, Poll Messages, Message Revoke, etc.

**Note:-** WhatsApp has **[currently](https://github.com/tulir/whatsmeow/issues/366)** removed or partially removed sending Button/List/Poll Messages to WhatsApp Business accounts. Normal accounts should work fine.

# Instructions
### For Tasker Users
Check this Tasker Reddit **[post](https://www.reddit.com/r/tasker/comments/12v710y/project_share_whatsapp_advanced_send_messages/)** for more info and importable Taskernet links.

### For CLI Users
#### CLI In Tasker
Refer to this section of **[readme](https://github.com/HunterXProgrammer/Tasker-mdtest#cli-in-tasker)** for Tasker CLI.

### CLI In Termux
Refer to this section of **[readme](https://github.com/HunterXProgrammer/Tasker-mdtest#cli-in-termux)** for Termux CLI.

# List Of Tasker Variables
These variables are populated whenever a WhatApp message of the corresponding type is received.

**Note:-** You need to run **"Mdtest - Start (V3)"** from the **"Receive Messages"** Project in `%mode` = `1` for the variables to be populated in the Task **"This Task Runs When Message Received V3"**.

#### Generally Available For All Message Types:-

`%type` = The type of message received. Can be one of -> message, extended_message, button_response_message, list_response_message or poll_response_message.

`%sender_name` = Name of the sender. Only set if the sender is saved in contacts.

`%sender_pushname` = Push Name of the sender.

`%sender_number` = Phone Number of the sender. Country code followed by the number. Eg:- If country code is "91", then -> 919876543210

`%sender_jid` = The JID of the sender. Country code followed by the number and "@s.whatsapp.net" at the end. Eg:- If country code is "91", then -> 919876543210@s.whatsapp.net

`%receiver_number` = Phone Number of the receiver. Country code followed by the number. Eg:- If country code is "91", then -> 919876543210

`%receiver_jid` = The JID of the receiver. Country code followed by the number and "@s.whatsapp.net" at the end. Eg:- If country code is "91", then -> 919876543210@s.whatsapp.net

`%is_from_myself` = If message was sent by yourself. Value is `1` if true, `0` if false.

`%is_group` = If message was sent in group. Value is `1` if true, `0` if false.

`%group_name` = Name of the Group. Only set if message was sent to group.

`%group_number` = Number of the Group. Only set if message was sent to group. Eg:- 919876543210-1234567890

`%group_jid` = The JID of the group. Only set if message was sent to group. Eg:- 919876543210-1234567890@g.us

`%time_stamp` = Time stamp of the message. Its of the format -> 2023-04-21 01:22:04 +0000 UTC

`%message_id` = Message ID of the received message. Used in advanced Task like Message Revoke, etc, to identify which message to revoke.

#### Variables specific to Text/Extended Messages:-

`%message` = The text message.

#### Variables specific to Button Response Messages:-

`%button_title` = Title of the Button Message.

`%button_body` = Body of the Button Message.

`%button_footer` = Footer of the Button Message.

`%button_selected_button` = Text of the selected Button.

`%origin_message_id` = The message id from which the Button Response Message originates from.  
(**Note:-** It is seperate from `%message_id`)

#### Variables specific to List Response Messages:-

`%list_title` = Title of the List Message.

`%list_body` = Body of the List Message.

`%list_footer` = Footer of the List Message.

`%list_header` = Header of the List Message.

`%list_button_text` = Text of the button of the List Message.

`%list_selected_title` = The text of the selected Title

`%list_selected_description` = The text of the  selected Description

`%origin_message_id` = The message id from which the List Response Message originates from.  
(**Note:-** It is seperate from `%message_id`)

#### Variables specific to Poll Response Messages:-

`%poll_question` = The Poll Question. Only set if the Poll Response Message was received when Mdtest was running. It will be written as old/outdated otherwise.

`%poll_selected_options()` = The array that contains the list of selected options. Only set if the Poll Response Message was received when Mdtest was running.
