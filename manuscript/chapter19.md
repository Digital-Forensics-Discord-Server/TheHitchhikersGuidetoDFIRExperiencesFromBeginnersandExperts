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

Linux was developed by Linus Torvalds at the University of Helsinki back
in the early 1990's.  It was, essentially, a "hobby" version of UNIX
created for PC hardware.

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

Linux is an operating system very similar to Unix, deriving most of its
functionality from the much older AT&T Unix originally developed in
1970.  This included a full TCP/IP stack and GNU development tools to
compile programs.  In short, Linux is mostly compliant with the Portable
Operating System Interface for Unix (POSIX).  
    
Despite the warnings of lack of architecture portability and limited
support mentioned by Torvalds in his postscript in the above quote,
Linux has grown to a fully functioning operating system that supports a
multitude of modern hardware.  Standard SATA hard drives through modern
M.2 and NVMe storage are now supported.  Drivers and software support
for newer motherboards and associated hardware are constantly improving
and growing.  The Linux kernel, where most of this support resides, has
a very fast production cycle and support for newer devices (where
specifications are available) is very rapidly added in most cases.

For the digital forensics practitioner, this hardware compatibility
issue can be exceedingly important.  Not only must we verify and _test_
that our hardware is properly supported and functioning as intended; we
also need to ensure that any subject hardware we might need to directly
attach to our system (which we might do for a variety of reasons) is
also properly detected and supported.  This is often done via direct
physical connection, or via boot media on a subject system.
       
While we have given a very general definition of what Linux is and where
it originated, we should also mention what Linux is _not_, particularly
where digital forensics is concerned.  We will cover _why_ you might
want to use Linux for digital forensics in a later section, but for now
a beginner forensics examiner should know that Linux is not a platform
well suited to "point and click", or what I like to refer to as
"nintendo forensics" techniques.  While there are graphical user
interface (GUI) tools available for Linux, it is not the strongest OS
for that approach.  More on that later.

Linux can be fairly easy to install, particularly given modern desktop
environments and GUI front ends for configuration and settings.
However, Linux is **NOT** a "better Windows".  Linux should not be
approached as a replacement to Microsoft Windows - one that acts like
Windows and is supposed to be familiar to someone who has been using
Windows (or MacOS for that matter) for years.  Linux works very
differently from some more mainstream operating systems. There is a
steep learning curve and trouble shooting problems can seem overwhelming
to someone used to running Windows on her computer. It is possible to
use Linux as a primary driver for digital forensics, and many digital
forensic practitioners have done this for years. But for most people new
to the field, Linux can be a fantastic learning tool and a great way to
access forensic and operating system utilities on an alternative
platform - but will still remain a secondary operating system.

Now that we have a very basic idea of what Linux is, and what it is not,
let's discuss *why* we might decide to add it to our digital forensic
tool box.

## Why Linux for Digital Forensics

There are any number of reasons for choosing to learn and run Linux for
use as a digital forensics platform.  We will cover the more important
ones here.

### Education

If you are a student of digital forensics, or a practitioner looking to
better understand a particular forensic process, Linux provides an
excellent environment for learning.

Particularly for students, the sheer number of free tools available for
Linux - not to mention the standard operating system utilities - makes
it very much accessible to all levels of income.  No need for expensive
licences or dongles to be able to do a full analysis or participate in
training.  While it is true that many open source digital forensics utilities
will compile and run natively on Windows, the ability to run multiple
copies of Linux, either on physical computers or virtual machines, still
makes it an attractive alternative for learning.

Many of the tools available for digital forensics on Linux are meant to
be used with the command line interface (CLI).  To a beginner it can
certainly appear to be daunting.  But learning at the CLI removes the
clutter of a GUI and all the menus and mouse clicks required to complete
a task.  Most Unix tools adhere to the philosophy that they should do
one thing, and do it well.  As you learn what each tool does and how it
works, you can string them together to accomplish a whole series of
steps with one command using multiple tools all at once.  This approach
allows you to concentrate on the results rather than an interface with
multiple windows and views to sort through. Again this is a benefit for
education specifically. There is no doubt that a forensic software suite
that ingests, analyzes evidence and presents the results in a single
step, is more *efficient*.  But learning from the CLI with specific and
very targeted output can be very powerful for students.

### Free(dom)!

Freedom and flexibility are just two of the many attributes that can
help make linux a useful addition to you tool box.  

First and formost of course, Linux is free.  As mentioned earlier, this
means we can install it as many times on as many computers (or virtual
machines) as we like.  You can use it as any sort of server while not
tying up valuable budget resources on licensing. This goes for the
forensic software as well.  You can install, copy, and share across
multiple platforms and users, again without breaking the bank.

For a practitioner learning the ins and outs of digital forensics, this
can be very powerful.  You can install multiple copies of Linux across
devices and virtual environments in a simple home lab 
XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXx

Linux provides unparralelled flexibility.  It will run on all forms of
hardware, for laptops and desktops, to mobile devices and development
hardware like the Raspberry pi, or 
    - lab setup

### Control
    - 
    - granular control over devices, drivers, etc.
    - not as exlusive as it once was
    
### Cross Verification - An Alternate OS Approach
    - Using Linux in conjuction with Windows

So how does one start a journey into using Linux for digital forensics?
We begin with a discussion of distributions and selecting you platform's
"flavor" of Linux.

### Distributions
    
In short, a "Linux Distribution" (or "distro" for short) is a
collection of Linux components and compiled open source programs that
come together to create an operating system.  These components can
include a packaged kernel; optional operating system utilities and
configurations; configured desktop environments and window managers;
and software management and utilities. These are all made tied
together with an installer that is usually specific to the given
distribution.

With the open source nature of the Linux environment, you could even
grab all the source code for the various components and build your
very own distribution, or at least running version of Linux. This is
often referred to as "Linux from Scratch" (LFS).  But the various
distro developers do all the heavy lifting for you. Packaging it all
up and making the entire operating system available to you for
install via a variety of methods.

Some popular distributions out there include (but are certainly not
limited to):
 - Ubuntu
 - Manjaro
 - Arch
 - Mint
 - SUSE
 - Red Hat
 - Slackware
 - and many others

So how does one choose a Linux distro? Particularly for use as a
digital forensics platform?
   
#### Choosing Your Platform

From the perspective of a digital forensics examiner, any distro
    - Requirements
    - baseline or Ready out of the box
    - Bootable vs installed
    - baremetal vs VM

#### Simple vs. Easy


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
