---
title: Writing NES homebrew in 6502 assembly
layout: post
catagories: [Programming]
tags: [6502, NES]
---
So I came across this 6502 tutorial on Reddit yesterday. After I went through it I was left with an itch to put it to use. I decided that writing some NES homebrew would be a decent use. After google I the Nerdy Nights tutorial which is fantastic. I’ve only gone up to week 3 and I may or may not continue with them. The problem I faced though was that the tutorial was written for the nesasm assembler which from what I’ve read isn’t great and even worse is I couldn’t track down the source to compile it as all I could find were Windows binaries. After a bit of searching I decided to use asm6 which is much better. The problem now was just that I’d have to  learn one way but code it in another. It’s wasn’t a huge hassle since it was a learning experience. Here’s the code for the NN week 3 example written for asm6:

{% highlight gas %}
.db "NES", $1a
.db $01
.db $01
.db $00|%0001
.dsb 9, $00

.org $C000

Reset:
sei ; disable IRQs
cld ; disable decimal mode
- lda $2002
bpl -
- lda $2002
bpl -
;; clear memory
lda $00
ldx $00
- sta $000,x
sta $100,x
sta $200,x
sta $300,x
sta $400,x
sta $500,x
sta $600,x
sta $700,x
inx
bne -
lda #%10000000 ; intensify blues
sta $2001 ; write PPUMASK
- jmp – ; infinite loop

NMI:

IRQ:

.org $FFFA

.dw NMI
.dw Reset
.dw IRQ

.dsb $2000, $00 ; no CHR data so pad 8KB
{% endhighlight %}

Forgive the bad formatting from WordPress. If I do decide to go through more of them I’ll also post the code here as well.
