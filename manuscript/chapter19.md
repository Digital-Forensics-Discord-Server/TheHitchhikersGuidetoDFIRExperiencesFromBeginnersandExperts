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

Modern Linux is an operating system very similar to Unix, deriving most of its
functionality from the much older AT&T Unix originally developed in
in the 1970's.  This included a full TCP/IP stack and GNU development tools to
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
well suited to "point and click", or what some might refer to as
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
very targeted output can be immensely powerful for students.

### Free(dom)!

Freedom and flexibility are just two of the many attributes that can
help make Linux a useful addition to you tool box.  

First and foremost of course, Linux is free.  As mentioned earlier, this
means we can install it as many times on as many computers (or virtual
machines) as we like.  You can use it as any sort of server while not
tying up valuable budget resources on licensing. This goes for the
forensic software as well.  You can install, copy, and share across
multiple platforms and users, again without breaking the bank.

For a practitioner learning the ins and outs of digital forensics, this
can be very powerful.  You can install multiple copies of Linux across
devices and virtual environments in a simple home lab, deleting,
reinstalling and repurposing computer resources along the way.
Installing and running Linux is a great way to re-purpose old hardware,
which brings us to our next point.

Linux provides unparalleled flexibility.  It will run on all forms of
hardware, from laptop and desktop computers, to mobile devices and
single board computers (SBC). It will run in a variety of virtualisation
environments, up to and including Microsoft Windows own Windows
Subsystem for Linux (WSL/WSL2).  You can chose to run a Linux
distribution on a workstation, on a $50 Raspberry Pi setup, in a virtual
machine, or natively in Windows using WSL.  These all have their
benefits and drawbacks, including cost; direct hardware access;
convenience; and resource requirements.

Another facet of Linux flexibility lies in the number of choices, freely
available, that users have over their working environment.  Desktop
environments like Plasma, Gnome and XFCE provide a wide range of choices
that a user can customize for aesthetics or workflow efficiency.  These
desktop environments don't change the underlying operating system, but
only the way one interacts with the system.  Paired with a separate
*window manager*, there are hundreds of possibilities for customization.
While it may sound trivial, we are not discussing wallpaper and icon
themes here - we are talking about the flexibility to decide exactly
*how* you interact with the system.

For example, you can set up a Linux environment that focuses on
primarily CLI usage where the keyboard is the primary interface and the
mouse is rarely needed.  This can be done with a wide selection of
"tiling" window managers that open new windows in a pre-determined
arrangement and allows for window manipulation, multiple workspaces and
program access all through customizable keystrokes and little or no use
for a mouse.  Certainly not an configuration that will appeal to
everyone, but that is one of the joys of Linux - the ability to
completely customize it to match your particular workflow.

### Control

Another traditional benefit of Linux over other operating systems has
historically been the control in provides over the entire device
environment. This has always been one of the more important factors when
adopting Linux in the context of a forensic workstation.  Most operating
systems are designed to isolate the user from the inner workings of
hardware.  Linux, on the other hand, has traditionally allowed for much
more granular control over attached devices and the associated drivers.
This has blurred somewhat in recent years with a number of popular Linux
versions becoming more desktop oriented and relying more and more on
automation and ease of operation.  While this approach does hide some of
the control options from the user, they are generally still available.

And again, with changes in recent years, this level of hardware control
is not as exclusive to Linux as it once was.  
    
### Cross Verification - An Alternate OS Approach

All of the preceding might come across as pushing Linux as a superior
operating system for digital forensics.  That is most certainly not the
intention. Rather, an effort has been made to point out the strengths of
Linux in comparison to other platforms.  In reality, having Linux in your
digital forensics arsenal is simply having access to a particularly
powerful alternative tool.

It is absolutely possible to utilize Linux as a primary digital forensic
platform in today's laboratory environment. It is also a reality that
providing timely and usable information for non-technical investigators
and managers often means utilizing the reporting and data sharing
functionalities available in modern forensic software suites that most
often run under mainstream operating systems and not Linux.

So where does Linux fit into a modern laboratory where reality and case
load dictates the use of software suites with automated functionality?

As an alternative operating system, Linux is often used to troubleshoot
hardware issues where one platform either cannot detect or cannot access
particular media.  Linux is well known for its ability to provide better
diagnostic information and sometimes better detection for damaged or
otherwise misbehaving devices.  When dealing with difficulties accessing
a hard drive, for example, you will often hear the advice "connect it to
a Linux box". Being able to directly monitor the kernel buffer and view
the interactions between hardware and the kernel can be a great help in
solving hardware issues.

There is also the benefit of having a completely different operating
system utilizing a different tool set to do cross verification of
findings.  In some organizations, the cross verification of significant
analysis results is a requirement.  Depending on the situation, it can
make good sense even if not explicitly required.  Cross verification
means that if a practitioner finds an artifact or draws a particular
conclusion on a given piece of evidence then there needs to be a
"confirmation" of that finding using a different tool or technique.
Consider the following simplified example:

1. A forensic examiner extracts the "user created contents" (documents,
   emails, etc.) from computer media and provides the data to an
   investigator using a common Windows forensic software suite.
2. The investigator identifies a particular document that can be
   considered valuable to the case being investigated and requests a
   report specific to that document.
3. The forensic examiner provides a targeted report detailing the
   document's properties - timestamps, ownership, where or how it
   might have originated on the media, etc.
4. The forensic examiner re-analyzes the specific document using a
   completely different tool perhaps on a completely different operating
   system (Linux in this case). Does the alternate tool identify the same
   location (physical disk location)?  Are the time stamps the same?  Is
   the document meta data the same? Differences, if any, are
   investigated and explained.  
   
The cross verification outlined above is somewhat overly simplified, but it
provides an outline of how Linux can be commonly employed in a
laboratory environment dominated by Windows software and the need for
efficient reporting.  Using a completely alternative operating system
and unique open source tools to cross verify specific findings can help
eliminate questions over automated processes and protects the veracity
of the report.

Another benefit of using Linux to cross verify findings it that it
allows you to fit Linux into your workflow, thereby  giving you reason
to actually use it rather than simply installing it and trying to make
time to learn.  

## Choosing Linux

So how does one start a journey into using Linux for digital forensics?
We begin with a discussion of distributions and selecting you platform's
"flavor" of Linux.

### Distributions

A "Linux Distribution" (or "distro" for short) is a
collection of Linux components and compiled open source programs that
come together to create an operating system.  These components can
include a packaged kernel; optional operating system utilities and
configurations; configured desktop environments and window managers;
and software management and utilities. These are all tied
together with an installer that is usually specific to the given
distribution.

With the open source nature of the Linux environment, you could 
grab all the source code for the various components and build your
very own distribution, or at least running version of Linux. This is
often referred to as "Linux from Scratch" (LFS).  On the other hand, the various
distro developers do all the heavy lifting for you. Packaging it 
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
   
### Choosing Your Platform

From the perspective of a digital forensics examiner, any distro will
work within reason.  The simplest answer is to download any popular
distribution and just install it.  In the long run just about any
flavor of Linux can be made to act and "feel" like any other.  

If you want to do some research first, consider looking at what is
already in use.  Does your lab or agency already use Linux in the
enterprise? It may be a good idea to use a Linux system that closely
matches what your organization already has deployed.  If part of your
job is to respond to company or agency incidents, a more intimate
knowledge of the systems involved would be helpful.  

Another legitimate answer to the question of "which distro?" is simply
to see what others around you are running.  If you have co-workers or
lab mates that are running a specific version of Linux, then it makes
sense to do the same.  Being able to consult with co-workers and friends
makes getting support much easier.  

There are, however other points that might warrant scrutiny.  Ubuntu, as
popular as it is, has drifted toward a more desktop oriented operating
system. Configuration options and system settings have been made much
easier through a number of GUI utilities and enhancements that make the
distribution more focused on ease of use - the end user still has
access to in-depth control of the operating system, but there might be
some work involved in disabling some of the automation that might hamper
forensic work.

Other Linux distributions offer a far more simple approach - minimally
configured "out of the box", leaving it completely up to the user to
configure the bells and whistles often considered normal features for
modern operating systems.  Distributions like Slackware , Void Linux and
Gentoo fall into this category. With these distributions, rather than
making systemic changes to a healiy desktop oriented configuration, you can start with
a more streamlined workstation and work up, building a more efficient
system.

The last consideration one might want to consider is selecting between a
rolling release and incremental release distro.  Normally we think of
numbered releases for an operating system.  Version X realeased on a
given date, often with security updates and bug fixes in between major
version realeases.  Eventually another release, let's call it version Y
is made available and so on. Distributions like Slackware, Debian and
(generally) Ubuntu fall ito this category. For the most part these are
considered more stable, where components of the desktop and operating
system are updated and tested together before release.  For the forensic
examiner, this approach provides not only the aforementioned stability,
but also fewer mass changes to kernel components and sofware libraries
that might affect the forensic environment and unexpected behaviors that
can impact evidence integrity or the interpretation of examination
results.

A rolling release, on the other hand continually updates software as new
versions become available for everything from the the kernel to base
libraries. This has the benefit of always keeping up with the "latest
and greatest".  Changes to upstream software are often immediately
supported.  One obvious negative effect of this, aside from being more
prone to instability, is that wholesale changes to the operating system
should probably trigger some testing on part of the forensic examiner.
There should be no dobut that a digital forensics platform is operating
exactly as expected. Constant mass upgrades can interfre with this by
possibly breaking or chaning expected output or hardware behavior.
Examples of rolling releases include Arch , Manjaro, Void, and Ubuntu
Rolling Rhino.

Another option, of course, is a ready made distribution specifically
designed for digital forensics.  Kali Linux, Caine and Tsrugi Linux are
common examples.  These are generally used as bootable operating systems
for live investigations, but can also be installed directly on hardware
to use in a Lab.  The benefit is obviously that the system is ready to
go with just about all the forensic software one might need to conduct
digtal forensics, incident response, or even Open Source Intelligence
(OSINT). From an education perspecitve, ready made forensic
distributions have you up and running quickly, ready to learn the tools.
What you might miss however is actually setting up, finding and
installing the tools yourself - all part of the education process.

If there are no organizational considerations, then consider using a
popular distribution with wide acceptance in the community.  Ubuntu is
the first distribution that comes to mind here.  Much of the forensic
software available today for Linux is developed and tested on Ubuntu.
There is a huge support community for Ubuntu, and just about any
question you might have has already been answered and is readily
available. While this can be said for other distributions (Arch Linux
comes to mind), Ubuntu is most certainly the most ubiquitous.  

Or you can take the opposite view and install a distribution along the
lines of Slackware or Gentoo.  Start with a very 'vanilla'
installation and learn the ins and outs of configuration, sysetem setup,
and administration without a lot of helpful automation.  Choices and
customization options are abundant.

## Learning Linux Forensics

There are a copious amount of resources available to help learn linux.
From distribution specific tutorials and Wiki pages, to command line
oriented blogs and websites.  You can take an online course from any one
of the many providers out there from Udemy, Edx or even Youtube.  There
is no shortage of learning material.

Here we are concentrating on a digital forensic perspective.  There are
still numerous resources for digital forensics and Linux, including
books and websites, but the material is not quite as widespread.

"Learning Linux forensics" can also have a couple of different meanings.
We could be talking about using Linux as a forensic platform - using
tools and techniques within the Linux operating system to analyze
digital evidence, regardless of source.   It's also possible that you
might only be interested in *investigating* Linux - learning Linux as a
potential target of an analysis.

### Linux as a Platform

Most of what we have covered so far assumes an interest in choosing and
installing Linux for use as a platform to perform forensics, either as a
primary operating system, or as an augment for cross verification.

Learning to use Linux in this way has several facets.  First is actually
learning the operating system - the installation, configuration, network
environment, and interface.  This is common to all users, whether the
system will be used for digital forensics or not.  We do, however, need
to account for "out of the box" configuration or automation that might
hamper or interfer with evidnce integrity.  Something most other Linux
users are not generally concerned with.

Second, there are the tools we need to learn.  These fall into a number
of categories:

 - Evidence Acquisition
 - Volume analysis
 - File system analysis
 - Application analsys
 - Memory analysis
 - Network enumeration and analysis
 - Data parsing
 
There are specific tools (with some crossover) for each of these
categories, which we'll cover in the next sections.

The Law Enforcement and Forensic Examiner's Introduction to Linux, the
LinuxLEO guide, is available for free.  Written by the same author as
this chapter, the guide was produced as a complete guide to installing
Linux, learning the operating system, and using forensic tools to
conduct hands on exercises using sample practice files.  The
materials are freely available at https://www.linuxleo.com.

### Linux as a target

Perhaps you have no specific desire to use Linux as a day to day
forensic platform.  There is, however, something to be said for knowing
how Linux works and where to look for evidence should you be assigned an
analysis where the subject device runs a version of Linux.

For years now, Linux has been a popular server operating sysetm,
utilized in enterprise environments across the world.  In the past few
years there has been a steady growth of "desktop" Linux, particualary
with the emergence of user oriented distributions like Ubuntu, Mint and
derivations based on them. A growth in Linux compatible software for specialized
tasks such as video editing, publishing, and even gaming has resulted in
Linux being more widely adopted.  Alwasy strong in academia, the growth
of Linux destop applications has resulted in a much wider user base.

Given the popularity of the Android operating system, which is (in
simple terms) based on Linux, there has always been a stronger need for
familiarity with Linux in the analisys of mobile devices.  But Android
is not the same as Linux on desktop computers.  Similar for sure, but
file system differences and application analysis are widely divergent.

One of the biggest issues that arises when examining a Linux system as
the target of an examination is the breadth of possible options
available to a user in a customized desktop (or server for that matter).
For example, an examiner must be at least somewhat familiar with a
subject computer's *init* system. Most modern distributions use
*systemd* to control processes and logging.  Other distributions rely on
the older text based *BSD init* or *System V* process scripts.  In
either case and depending on the nature of the investigation, knowing
how processes are started, and how they are started might be an
important part of the forensic puzzle.

Tracking and identifying *user activity* is often another important
piece of the puzzle.  With Linux, regardless of distribution, users
have a wide range of choices for desktop environments, window managers,
file managers, and many other desktop components.  All of these
components, some used in combination, store configuration and user
activity in different formats and locations which makes having intimate
knowledge of every possible iteration very difficult.  

Event the very low level components of a Linux installation can differ,
even within a single distribution.  Users can choose a different boot loader
(which loads the operating sysetm) and even a different file system
format.  Most Linux distributions will use the Ext4 file system by
default, but it's a simple matter to select and install any number of
others depeding on perference:  btrFS, XFS, ZFS, JFS are all examples of
file systems.  Should an examiner come across one of these,
consideration would need to be givent to file recovery, allocation
strategies to help determine file activity, and perhaps forensic
software support.

All of these are challenges with examining any of the myriad
permutations of Linux. There are a few books covering the basics of Linux
examinations. Much of the information available from a forensic
perspective can be found in a few videos or seminars.  For anyone
looking for a challenging focus for research or  a subject for an academic 
project, Linux as a forensic target provides ample subject matter for
unique content.

## Linux Forensics in Action

All of the information covered so far gives a overall view of Linux and
where it might fit in with a digital forensic workflow.  For those just
starting out, or for those that have never seen Linux in action before,
it might be useful to actually see a very simple command line session
from acquistion through artifact recovery and interpretation.

There are far too many tools to cover in a single chapter.  Again,
documents like the previously mentioned [LinuxLEO guide](https://linuxleo.com)
will cover a great number of tools with hands on opportunities.  Here we
will select just a few tools to do a quick analysis of a Microsoft
Windows Registry file.

First, let's map a quick outline of what we wish to accomplish, and the
tools we will use:

 1. Define the goal of the examination (scope)
 2. Acquire the evidence 
 3. Map the storage media and find a volume of interest
 4. Identify the file system format within that volume
 5. Identify artifacts (e.g. files) of interest
 6. Extract / Examine the artifacts
 7. Parse data from each artifact

### Define the Goal of the Examination

An important part of every digital forensic analysis is planning the
goal or at least the scope of your examination. Helping to focus on a
goal gives an idea of the tools requried and the methods to be used.  In
many cases, when providing forensic support to other investigators, the
goal of the examination is defined by the support request.  In other
cases, the elements of the crime or known inicators (in the case of
network compromise) provide the goals.

In this particular exercise, we will go back to our premise of cross
verification.  Covering every step in exact detail is outside the scope
of this chapter. This is an illustration of what a simple cross
verification of results might look like.  

Let us assume we have the output from a Windows Forensic suite that
shows a particular user last login date of an enterprise workstation at
a given time.  This was done through the examination of the SAM registry
file. The specific time the user logged in is imperitive to the case
and we want to cross verify the results.  Our original output shows
this:

![Original Registry Output](resources/Ch19/regripout.png)

The goal for this examination is to verify the above *Last Login Date*
with a separate tool under Linux.

### Acquire the Evidence



### Map the Storage Volumes

### Identify the File System

### Identify the File(s) of Interest

### Extract and Parse the data



## Closing
