# RakNet: Removal of the authorization requirement
Guide created by Raymond, with lots of help by Yakov

<hr>

This was made for users who are having trouble connecting to their `RCCService` due to invalid RakNet keys.<br>
This is *technically* more secure than setting the FFlag, but it *could* cause issues down the line (you'll probably be fine.)

We're jumping around a function inside of RakPeer.cpp,<br>
essentially we're just guiding the program around the code that'll check if it's a valid key and shooting right towards the `return true`.

Pattern used: `6A016A088D45` (This was created from a 2017L build, it may have been changed in newer builds, but that's unlikely.)

You'll know when it's the correct set of instructions when a few lines above there's a `mov` ending in `5`.

![Image taken by Yakov. Thank you!!](https://user-images.githubusercontent.com/101374892/215641057-b20482f4-7d20-46e4-8d78-531ad7658d05.png)

Instructions to modify, starting from the first `nop` above the `push 1 & push 8`:<br>
	1. First `je`, simply change it to `jmp`<br>
	2. First `jne`, should be the **same instruction** as the `je` we just changed *(make sure the address to jump is modified too.)*<br>
	3. And the first `jne` above the `nop`, of which was mentioned earlier.

Save the patches, and try launching RCC.<br>
It should be able to connect without having to authorize your client passwords.
