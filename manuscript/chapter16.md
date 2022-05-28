# Chapter 16 - Artifacts as Evidence

## Forensic Science
Before learning about artifacts as digital evidence, I'll preface this chapter with the most fundamental definition of basic science. So what is Science? It is a field that follows a scientific process in any of its domain. That process is cyclical and goes something like this:

* We make observations in nature.
* We form an initial hypothesis about something.
* We look for things that confirm or deny the formed hypothesis.
* If we find something that denies it, we form a new hypothesis and go back to making observations.
* If we find something that confirms it, we continue making new observations to extend our dataset and verify the hypothesis until the dataset is substantial in confirming it precisely and accurately. If we further find something that denies the original hypothesis, we form a new one repeating the process.

We never pollute this scientific process with biases or opinions. It is only credible as far as the fact finder's neutralness go. All scientists, trust observations and verified prior research, discarding all speculation.

![Law vs Theory](https://upload.wikimedia.org/wikipedia/commons/7/7f/Scientific_law_versus_Scientific_theories.png)

Ultimately, the goal of any science is not to state things in absolutes, but in observations, experiment, procedure and conclusions. Even the fundamental laws of science begin with a basic foundation laid of assumptions.

Much like any scientific field, forensics or criminalistics is a branch of science that deals with identifying, collecting and preserving evidence of a crime. It is not just identifying, collecting and preserving but doing so in a forensically sound manner. What that means is that evidence should not be changed or stray away from its true form.

Digital Forensics is a six phase process including Preparation, Identification, Collection, Preservation, Analysis and Reporting.

## Types of Artifacts

Analysis is a major phase where in forensicators discover different types of artifacts ranging from plain metadata to complex evidence of execution and residual traces. The vast gap between the difficulty to retrieve or reconstruct evidence determines the fine line between E-discovery and Digital Forensics.

User data such as internet history, images, videos, emails, messages etc fall under E-discovery. It is relatively easy to reconstruct even from the unallocated space. 

However, System Data like artifacts that help support some view of truth, or determine how closely a transpired event is to the evidence, are not that simple to manually parse with forensic soundess, which is why oftentimes forensicators rely on well-known parsing tools either commercial or opensource.

![EDvsDF](https://raw.githubusercontent.com/Nisarg12/CrowdsourcedDFIRBook/main/manuscript/resources/Ch16/EDvsDF.png)

And that is the main difference between E-Discovery & Digital Forensics depending on the categorization of data alone. Both follow different procedures and have different scope of execution. Generally, E-Discovery can be contained to only the logical partitions and the unallocated region whereas Digital Forensics operates in a much wider scope solely due to the necessity of dealing with complex data structures.

## What is Parsing?
Which brings us to parsing. We often go around throwing the term  while working with a variety of artifacts;
"Parse this, parse that", but what does it mean in the real sense? To understand the parsing methodology, tools & techniques, we must be familiar with the origin of the handling of the data being parsed. What I mean by that is how was the data originally meant to be handled. What was its structure by design. How can it be replicated.

Generally, it is some feature or underlying mechanism of the main operating system installed on the device. Parsing tools are written to accurately mimic those functions of the operating system which make the raw data stored on the hardware, human readable.

<img width="500" alt="Computer_Structure" src="https://upload.wikimedia.org/wikipedia/commons/b/b7/Role_of_an_Operating_System.svg">

Understand the operating system as an abstraction level between the end-user and the intricacies of raw data. It provides an interface to the user which hides all the complexities of  computer data and how it is being presented.

Before parsing the artifacts and diving deep into analysis, you must fully understand how files are generally handled by an operating system. As mentioned earlier, an operating system is just a very sophisticated piece of software written by the manufacturers to provide an abstraction level between the complexities of hardware interactions and the user.

In the context of file handling, operating systems either *store* files or *execute* files. Both of which requires different types of memory. Also note that *storing* files requires access to a storage media such as HDDs, SSDs and Flash drives, whereas *executing* files requires access to the microprocessor. Both are handled by the operating system.

As you might already know, computers or any electronic computing device for that matter, primarily utilize two types of memory:
1. **RAM (Random Access Memory):**
	* Volatile memory, only works for the time power is supplied.
	* Used for assisting execution of applications/software by the processor of the device.
2. **ROM (Read Only Memory):**
	* Non-volatile memory, retains data even when not in use.
	* Used for storing the application files for a larger period of time.

There are many sub-types of both RAM & ROM but only the fundamental difference between them is concerned here.
Now let's quickly look at the timeline of an application lifecycle in two stages:

1. **Production Cycle:**
> An application is a set of *programs*. A program is a set of *code* written by a programmer, generally in higher levelled languages that do not interact directly with machine level entities such as registers, buses, channels etc. That piece of code is written to the disk. The code is then compiled to assembly, which is a lower levelled language which can interact directly with machine level entities. Finally the assembly is converted to the machine code consisting of 1s and 0s (also known as binary or executable file), which is now ready for its execution cycle.
2. **Execution Cycle:**
> Now that the program is sitting on the disk, waiting to be executed, it is first loaded into the RAM. The operating system instructs the processor about the arrival of this program and allocates the resources when they're made available by the processor. The processor's job is to execute the program one instruction at a time. Now the program can execute successfully if the processor is not required to be assigned another task with a higher priority. If so, the program is sent to the ready queue. The program can also terminate if it fails for some reason. However, finally it is discarded from the RAM.

You can easily remember both of these cycles by drawing an analogy between electronic memory and the human memory. Here, I use chess as an example. Our brains, much like a computer, uses two types of memory:
1. **Short-term (Working memory):**
	* For a game of chess, we calculate the moves deeply in a vertical manner for a specific line based on the current position.
	* This is calculative in nature. Calculation comes from present situation.
2. **Long-term (Recalling memory):**
	* At the opening stage in a game of chess, we consider the candidate moves widely in a horizontal manner for many lines.
	* This is instinctive in nature. Instinct comes from past experiences.

Understanding how an operating system parses the data from different sources, rather it be on-disk or in memory; will help you identify, locate and efficiently retrieve different types of artifacts necessary for an investigation.

## Artifact-Evidence Relation
You will come across an ocean of different artifacts in your investigations, but artifacts have a very strange relationship with what might potentially be considered evidence. Artifacts alone do not give you the absolute truth of an event. They provide you tiny peepholes through which you can reconstruct and observe a part of the truth. In fact, one can never be sure if what they have is indeed the truth in its entirety.

<img width="500" alt="Truth" src="https://raw.githubusercontent.com/Nisarg12/CrowdsourcedDFIRBook/main/manuscript/resources/Ch16/Truth.jpg">

I always love to draw an analogy between the artifacts and the pieces of a puzzle, of which you're not certain to have the edge or the corner pieces. You gather what you can collect, and try to paint the picture as unbiased and complete as possible.

<img width="500" alt="Puzzle" src="https://raw.githubusercontent.com/Nisarg12/CrowdsourcedDFIRBook/main/manuscript/resources/Ch16/Puzzle.png">

That being said, if you apply the additional knowledge from metadata, OSINT and HUMINT to the parsed artifacts, you might have something to work with. For instance, say you were assigned an employee policy violation case, where the employee was using their work device for illegally torrenting movies. Parsing the artifacts alone will give you information around the crime, but not as evidence. You would still need to prove that the face behind the keyboard at the time of the crime, was indeed the one that your artifacts claim. So you would then look for CCTV camera footage around the premises, going back to the Identification phase in the digital forensics lifecycle, and so forth and so on.

As a result of a codependency of the artifacts on drawing correlations to some external factor, they form a direct non-equivalence relation with evidence.

However, note that this "rule", if you will, is only applicaple to a more broad scope of the investigation and will generally be handled by the lawyers. In the more narrow scope as a forensicator, and for the scope of your final forensic report, artifacts are most critical. Just keep it in the back of your mind that encountering an artifact alone does not mean its admissible evidence. Parse the artifact, make notes and document everything. Being forensically sound is more important than worrying about completing the entire puzzle. Because there will be no edge or corner pieces to it.

## Examples
This section will cover how some of the more uncommon artifacts can play into a case from a bird's eye view. We won't be getting into the technical specifics on the parsing or extraction, but the significance of those artifacts at a much higher level. Such as what does it offer, prove and deny. And what is its forensic value. I suggest the readers to use these brief bits to spark their curiosity about these important artifacts, and research on their own about locating and parsing them.

### Registry
___About:___
* Windows registry is a heirarchical database used by the Windows operating system to store its settings and configurations. Additionally, it also stores some user data pertaining to user applications, activities and other residual traces.

* Registry is structured with what are called Hives or Hive Keys (HK) at the top-most level. Each hive contains numerous keys. A key can contain multiple sub-keys. And sub-keys contain fields with their values.

There are mainly two types of hive files:
1. **System Hive Files:**
	* SAM (Security Account Manager) - User account information such as hashed passwords, account metadata including last login timestamp, login counts, account creation timestamp, group information etc.
	* SYSTEM - File execution times (Evidence of Execution), USB devices connected (Evidence of Removable Media), local timezone, last shutdown time etc.
	* SOFTWARE - Information about both user and system software. Operating System information such as version, build, name & install timestamp. Last logged on user, network connections, IP addresses, IO devices etc
	* SECURITY - Information about security measures and policies in place for the system.
2. **User Specific Hive Files:**
	* Amcache.hve - Information about application executables (Evidence of Execution), full path, size, last write timestamp, last modification timestamp and SHA-1 hashes.
	* ntuser.dat - Information about autostart applications, searched terms used in windows explorer or internet explorer, recently accessed files, run queries, last execution times of applications etc.
	* UsrClass.dat - Information about user specific shellbags, covered in the next section.

___Significance:___
* Identifying malware persistence which can lead to the discovery of IOCs.
* Proving the presence of removable media in a particular time frame, which can further help with acquisition of the same.
* Retrieving crackable user password hashes from the SAM and SYSTEM hives, which might help access the encrypted partitions if the password was reused.

### Shellbags
___About:___
* Shellbags were introduced in Windows 7. It is a convenience feature that allows the operating system to remember Windows Explorer configuration for user folders and a folder's tree structure.
* Whenever a folder is created, selected, right-clicked, deleted, copied, renamed or opened, shellbag information will be generated.
* Depending on the Windows version, shellbag information can be stored in either ntuser.dat, UsrClass.dat or both.

___Significance:___
* Reconstructing the tree structure for deleted folders. Helpful in providing an idea of the files that used to exist when they cannot be carved from the unallocated space.
* Disproving denial of content awareness. If a subject claims that they were simply not aware of something existent on their system, shellbags can disprove their claims with an obvious given that an exclusive usage of the machine was proven.
* Getting partial information about the contents of removable media that were once mounted on the system.

### Prefetch
___About:___

* Prefetch was first introduced in Windows XP. It is a memory management feature which optimizes loading speeds for files that are frequently executed. Originally it was meant for faster booting times, but since has been developed for applications too. Hence, this artifact is a direct evidence of execution.
* We looked at the lifecycle of an application earlier, the prefetcher in Windows works in the same way. It studies the first \~10 seconds of an application launched and creates/updates the corresponding prefetch file, for faster loading speeds on the next execution.
* Starting from Windows 10, prefetch files are compressed by default to save considerable disk space. It uses the Xpress algorithm with Huffman encoding. For validation purposes, forensicators must decrypt their prefetch files first. Thank you [Eric](https://twitter.com/ericrzimmerman), for this handy [python script](https://gist.github.com/EricZimmerman/95be73f6cd04882e57e6) for the same.

![Working of Windows Prefetcher](https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch16/Prefetch.png)

It has three working modes:
| Value | Description |
| :---: | :--- |
| 0 | Disabled |
| 1 | Application prefetching enabled |
| 2 | Boot prefetching enabled |
| 3 | Application & Boot prefetching enabled |

This value is set from the registry key:
`HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters`
Forensicators can refer to this key to check if prefetching is disabled.

___Significance:___
* Since it is evidence of execution, it is helpful in identifying anti-forensic attempts at bypassing detection. Any automated anti-forensic tools ran would in turn result in its own prefetch file being generated.
* Useful in identifying and hunting ransomware executed. Once identified, analysts can look for publicly available decryptors to retrieve encrypted files.
* By studying files and directories referenced by an executable, analysts can identify malware families.
* Application execution from removable media or deleted partitions can be identified from the volume information parsed.
* Timestamps for last eight executions and the run counter is useful for frequency analysis of malicious executables. Worms which would result into multiple prefetch files referencing the exact same resources is a prime example of this.

### Jumplists & LNK files
___About:___
* LNK files, or link files are the shortcuts that a user or an application creates for quick access to a file. LNK files themselves are rich in file metadata such as timestamps, file path, file hash, MAC address, volume information and volume serial numbers.
* However, apart from the Recent Items and Start Menu folders, these LNK files are also found embedded in jumplists.
* Jumplists were first introduced in Windows 7. It is a convenience feature of the Windows Taskbar, that allows a user to have a quick access to recently used files in or by different applications. It automatically creates these 'lists' in the right click context menu which can be used to 'jump' to a induce a frequently used action.
* There are two types of jumplists; automatic and custom. Automatic jumplists are those created automatically by Windows, based on the MRU and MFU items. Custom jumplists are those explicitly created by the user, like bookmarks in a browser or pinning files for instance.
* Both categories of these jumplists provide rich information like modified, accessed and created timestamps and absolute file path of the original file.

___Significance:___
* Useful to gain information on uninstalled applications and deleted files from the system & also applications ran and files opened from removable media.
* Again, being a direct evidence of execution, it can be useful in timelining executed applications and opened files.
* Useful to discover partial user history including URLs and bookmarks.

### SRUDB.dat
___About:___
* SRUDB.dat is an artifact resulting from a new feature introduced in Windows 8, called SRUM (System Resource Usage Monitor) which tracks and monitors different usage statistics of OS resources such as network data sent & received, process ownership, power management information, push notifications data and even applications which were in focus at times along with keyboard and mouse events as per a new [research](https://aboutdfir.com/app-timeline-provider-srum-database/).
* It is capable of holding 30-60 days worth of tracking data at a time.
* So far, we haven't looked at an artifact that has been able to indoubtedly map a particular process executed to a user. SRUDB.dat offers us this critical information directly. It is one of the most valuable artifacts due to the multidimensional applications of SRUM by the OS itself.

___Significance:___
* Useful in mapping process to a user account. Especially useful in the scenarios of restricted scope of acquisition.
* Useful in mapping a process to network activity such as bytes sent & received. Helpful in identifying data exfiltration incidents.
* Useful in timelining and distinguishing network interfaces connected to, and hence potentially estimate the whereabouts of the machine if those networks were distanced farther away from one another.
* Useful in analyzing power management information such as battery charge & discharge level.
* Useful in stating awareness or lack thereof, of an application that would've been visible on screen at one point in time, and the interaction with it by the means of input devices.

### hiberfil.sys
___About:___
* hiberfil.sys was first introduced in Windows 2000. It is a file used by Windows for memory paging, at the time of hibernations or sleep cycles. It is also used in case of power failures.
* Paging is a mechanism to store the current contents of the memory to disk, for later retrieving them and continue from the same stage. This prevents additional processing by applications and optimizes resource allocation by the operating system. Windows also enhanced this to allow faster startup times from a sleep states.
* It uses the Xpress algorithm for compression. Volatility's imagecopy plugin can be used to convert this artifact to a raw memory image.

___Significance:___
* This is one of those artifacts which hops around its categorical type, and so this extra memory content can provide more information to your investigation.
* To tackle accepting unfortunate shutdowns of locked devices in an investigation, one can retrieve this file at the time of disk forensics and get additional information by performing memory forensics on the converted file. This way we can retain partial volatile memory data.
* May contain NTFS records, browsing history, index records, registry data and other useful information.

### pagefile.sys
___About:___
* Similar to hiberfil.sys, pagefile.sys is a swapping file used by Windows to temporarily store new contents that were supposed to be loaded in the memory but could not due to insufficient space. When required amount of memory is freed, contents are transferred from this artifact back to the memory.
* The only known methods to get some information from this artifact is using the string utility, a hex editor, and filtering using regex.
* It can store chunks of data capping at 4kb in size.

___Significance:___
* Useful in hunting IOCs in malware cases.
* Useful in carving smaller files that were meant to be loaded in the memory. Meaning it is evidence of access. If an image was successfully carved from this artifact, it means that it was opened, as it would have meant to be eventually loaded in the working memory of that device.
* May contain NTFS records, browsing history, index records, registry data and other useful information.

### $MFT
___About:___

___Significance:___

### $I30
___About:___

___Significance:___

### $LogFile
___About:___

___Significance:___

### $UsnJrnl
___About:___

___Significance:___