# Chapter 17: Forensic imaging in a nutshell



## What is a disk image?

A disk image is a representation of data contained within a disk. It contains the contents of the entire disk, including all files and folders. Dedicated forensic hardware appliances or software packages ensure a bit-by-bit copy is performed. In other words, the contents of the disk image will match the contents of the disk exactly. When an unexpected error has occured, this will be flagged and the forensicator will be notfied. It is possible to make a disk image from every data source, including desktop, computers, laptops and servers, a USB-drive, an SD-card or any other data carrier you can think of. 

While a complete discussion about file systems is outside the scope of this chapter, it is impossible to touch upon forensic imaging and not talk about file systems.  A file system entails the logical representation of files and folders on the disk. It allows an operating system to keep track of files as well as other important file properties such as its location, size, file format and any assosciated permissions. There are different files systems used accross operating systems. The NTFS file system is currently used by all supported versions of Microsoft Windows. APFS is used by devices created by Apple, it is used across a wide range of devices including phones, tablets, TV appliances and computers.  Lastly, there is the Linux operating system, which uses a variety of file systems, depending on the version which is installed. Common varieties include ext3/ext4 and btrfs. More specialized file systems for specific appliances are also in use. The exact intricaties and technical documentation of a file system are often not available outside of its vendor which means that software vendors have to reverse engineer a file system to a degree. Expect a forensic investigation suite to continually improve support for popular file systems.

Once a disk image has been created it is possible to calculate its checksum. A checksum can be used to verify the integrity of a disk image. This is of paramount importance during a forensic investigation. Evidence will always need to be retrieved from other systems. Calculating a checksum at both ends, the source and destination file(s), will ensure that no anomalies are present. When a checksum matches at both ends, this means that no anomalies are present, the contents of the file match exactly and can be used in a forensic investigation. In order to create a checksum, a hash is created.  A hash is a mathematical, one-way calculation, performed by a specific algorithm. The MD5 and SHA1 algorithms are commonly used in the forensic community although other algorithms can be used as well. 

After validation of the checksum, the created image will be ready to use in an investigation. Forensic investigation suites will use the disk image as a basis for the investigation, allowing an forensicator to browse the file system for pertinent files and other forensic artifacts. Post-processing will also occur in many forensic suites, automatically parsing popular artifacts, thereyby making investigation easier. 

## Creating a disk image

There are different ways to create a disk image, this section will discuss the most popular methods. Be aware that  different scenario's might require different imaging methods. The following subsections are not intended to be ranked in order of preference. 

### Using a forensic duplicator

Forensic duplicators come in many shapes and sizes, however it's most common variety is a portable hardware appliance that can be easily transported and can be used both in a lab environment or on-site at a client.  A forensic duplicator can be used to create disk images of various physical media types. In order to do this it distinguishes between source and destination drives. Source drives are generally connected to the left side of the device while destination drives are connected to the right side of the device. **Be sure to confirm this with individual duplicators as there might be deviations.** Forensic duplicators support a range of different connectivity methods such as SATA, IDE, and USB. The ports supported by a duplicator are mirrored on either side of the device. **Ensure that the correct drives are connected to the correct side of the device prior to imaging. Failure to do this might result in data erasure.** Specialized duplicators also support SAS or an Ethernet connection to image from a computer network. 

Duplicators are used to perform the following functions:

- Clone a disk to a different disk
- Clone a disk to an image
- Format or wipe a disk
- Calculate hashes and verify its integrity
- Detection of a HPA or DCO
- Blank disk detection, verifying whether a disk is entirely blank or contains data.

### Using a Live USB 

In scenario's in which it is not feasible to get access to phyical media, a Live USB might provide an alternative. A Live USB contains an operatiing system which can be booted during the boot phase of a computer. While it is still neccessary to take a server or service offline it is not required to open it up and take a hard drive. Similarily, continuous miniturization means that some SSD's can no longer be removed from a motherboard.

An example of a forensic Live USB environment is **Sumuri Paladin Edge**. This Live USB environment is available free of charge at their website. In addition to imaging the entire disk it also allows you to convert images, find specific files,extract unallocated space and interface with network shares.

<img src="/Users/guus/Desktop/Screen Shot 2022-06-06 at 14.27.05.png" style="zoom:50%;" />   



### Disk imaging on Windows and Linux 



### Creating a remote disk image



## Disk image formats







## Memory forensics 

### Background 

While the disk forensics focus on forensic artifacts from files and folders, more pertinent information can also be readily available on a computer's memory. A computer's memory, called Random Access Memory or RAM for short, is used to carry out all active tasks of a computer. 

%% What is in the computer;'s memory?



As such it contains a wealth of artifacts not readily available through other means. For instance:



- A list of active and (potentially) recently terminated processes
- Active network connections
- Entered system commands
- Open file handles

In order to collect this information an application will generally perform a memory dump. A memory dump is exactly what it sounds like, the contents of the RAM extracted to a disk. Be aware that as the size of the RAM increases, an equivalent amount of disk space should be readily available for storage. Furthermore, the RAM does not remain in stasis while the extraction takes place. It will continue to perform tasks and will continue to change for the duration of the RAM dump. 

### How to dump memory



The use of virtual machines has become commonplace in the IT industry and of course this impacts memory acquisition as well with its own advantages and disadvantages. One advantage is that memory collection has become easier. A virtual machine hypervisor allows a virtual machine to be suspended, hitting the pause button, and freezing all activity. During this process the contents of the RAM are written to disk, no additional tools are neccessary to perform an acquisition. Files from popular vendors like VMware and Virtualbox can be analyzed by memory analysis tools like Volatility. 



