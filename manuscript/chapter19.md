# Chapter 19 - Linux and Digital Forensics

## What is Linux?

There are a plenty of resources available on what Linux is, what role it
fills, and how it compares with other operating systems.  Here we will
discuss Linux from the perspective of digital forensics and incident
response.  

There have been many discussions of what defines Linux.  The classical
definition is that Linux is a kernel ("brains of the operating system")
augmented by user space drivers, utilities, and applications that allow
us to interact with a computer in a useful manner.  For the sake of
simplicity we extend the name "Linux" to encompass the entire operating
system, and even the applications that can be bundled and distributed.

On 25 August, 1991, Torvalds posted this to the Usenet group
comp.os.minix:
> Hello everybody out there using minix
> I'm doing a (free) operating system (just a hobby, won't be big and
> professional like gnu) for 386(486) AT clones.  This has been
> brewing since april, and is starting to get ready. I'd like any
> feedback on things people like/dislike in minix, as my OS resembles
> it somewhat (same physical layout of the file-system (due to
> practical reasons) among other things).
> 
> I've currently ported bash(1.08) and gcc(1.40), and
> things seem to work. This implies that I'll get something
> practical within a few months, and I'd like to know what features
> most people would want. Any suggestions are welcome, but I won't
> promise I'll implement them :-)
> 
> Linus (torvalds@kruuna.helsinki.fi)
> PS. Yes - it's free of any minix code, and it has a
> multi-threaded fs. It is NOT portable (uses 386 task switching
> etc), and it probably never will support anything other than
> AT-harddisks, as that's all I have :-(.
>        --Linus Torvalds  (quoted from Wikipedia)}
        
        
    - forensic perspective
    - what it's not

### Distributions
    - what are distributions
    
#### Simple vs. Easy
    - forensic perspective
   
#### Choosing Your Platform
    - Any distribution (within reason)
    - Requirements
    - baseline or Ready out of the box
    - Bootable vs installed
    - baremetal vs VM

## Why Linux for Digital Forensics

### Education
    - free tools
    - online support (non vendor)
    - cli teaches "bits and bytes"
     
### Free(dom)!
    - flexibility to install as many times as you like
    - lab setup

### Control
    - granular control over devices, drivers, etc.
    - not as exlusive as it once was
    
### Cross Verification - An Alternate OS Approach
    - Using Linux in conjuction with Windows

## Learning Linux
    - forensic perspecitve
    - Lots of resources
    - Be wary of non-forensic advice for forensic issues
    
## Learning Linux Forensics
    - What is your purpose for using linux?

#### Linux as a Platform
    - if it is for learning forensics, you can try the linuxleo guide
    - watch windows forensics videos and see how you can apply linux
    - use it!

#### Linux as a target
    - There are books available, and more to come as linux growth on the
      desktop grows and server use increases.
    - Analysing an OS generally requires knowledge of how it works.
        - This can be made difficult by distribution differences,
          configuration differences, file system selection, etc.
        - baseline knowledge is a good base.

### GNU Utilities and the Power of the Command Line

### External Forensic Software

## Closing
