---
layout: blog
---
# C64 ASM Clearing the screen

Clearing the screen is one of those things that is so trivial on the C64 that you can do it by pressing Shift + CLR or in basic by typing :-

    PRINT CHR$(147)

It's not much more difficult to do it in assembly either thanks to the [built in kernal routines](https://www.pagetable.com/c64ref/kernal/) of the C64.

I'll show you how to clear the screen that way and then I'll show you another method which doesn't rely on the built in routines.

Why wouldn't we always use the built in ones? They're BUILT IN! That's kind of the point of them right? No extra cost, no extra effort.

Well, they're actually the BASIC routines that we're simply calling directly from assembly. If we have to overwrite basic in memory, we won't be able to use them anymore. (Need to confirm this. I'm sure there is a reason why you can't always use kernal routines.... but I could be wrong)

OK, here is the code for the first method

    *=$1000         ;load into $1000 (4096)

    jsr $e544       ;jump to clear screen routine
    rts             ;ReTurn from Subroutine (End)

Now I shall go over each line and explain how the code works.\
*=$1000 tells the assembler where to place our assembled code.
This is our programs entry point.

jsr $e544 This line tells the C64 to jump to memory address $e544.
This memory address contains the kernal routines pointer.

rts ends the program.

Easy isn't it.

Here is the code for the non-kernal method :-

    *=$1000         ;load into $1000 (4096)
    ldx #$00        ;load 0 into x register 
    lda #$20        ;load $20(space char) into a register
    loop
    sta $0400,x     ;store contents of a ($20) into screen location $0400 + value of x
    sta $0500,x     ;store contents of a ($20) into screen location $0500 + value of x
    sta $0600,x     ;store contents of a ($20) into screen location $0600 + value of x
    sta $0700,x     ;store contents of a ($20) into screen location $0700 + value of x
    inx             ;increment x
    bne loop        ;while x doesn't equal 0, jump to loop
    rts             ;ReTurn from Subroutine (End)

*=$1000 tells the assembler where to place our assembled code.
This is our programs entry point.

ldx #$00 loads 0 directly into the x register

lda #$20 loads the hex number 20 into the a register. $20 happens to be the character code for the space character. We're going to write this "character" into every memory address for the screen to wipe it.

loop - a label to show the start of our loop. We can call this anything.

sta $0400,x This is the first line we'll use to write to the screen. $0400 is the memory address for the top left corner of the screen. The ",x" after the memory address tells the computer to add the value of the x register to the $0400 number.
On the first run, x is 0 so the data ($20) is written to memory location $0400 + 0. As the program loops, x will have 1 added to it so will continue to increase until it rolls back to 0.

The next few lines do the same function but at different screen locations (I will explain later).

inx - increment x, Add 1 to whatever is in the x register.

bne loop - While x doesn't equal 0, go back to the loop.

rts ends the program.

The C64 screen is 1000 characters in size but our loop only allows us to count to 255 before it flips back to zero.

This is why we have those 4 similar lines, each one points to the screen location 255 bytes after the first.

If we were to slow the C64 down enough, we would see that our program writes 4 characters to the screen each time it loops until 4 sets of 255 characters have been written.

I hope that someone finds this useful and please get in touch if I have made any mistakes.
