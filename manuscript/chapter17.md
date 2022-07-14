# Chapter 17: Forensic imaging in a nutshell



## What is a disk image?

A disk image is a representation of data contained within a disk. It contains the contents of the entire disk, including all files and folders. Dedicated forensic hardware appliances or software packages ensure a bit-by-bit copy is performed. In other words, the contents of the disk image will match the contents of the disk exactly. When an unexpected error has occured, this will be flagged and the forensicator will be notfied. It is possible to make a disk image from every data source, including desktop, computers, laptops and servers, a USB-drive, an SD-card or any other data carrier you can think of. 

While a complete discussion about file systems is outside the scope of this chapter, it is impossible to touch upon forensic imaging and not talk about file systems.  A file system entails the logical representation of files and folders on the disk. It allows an operating system to keep track of files as well as other important file properties such as its location, size, file format and any assosciated permissions. There are different files systems used accross operating systems. The NTFS file system is currently used by all supported versions of Microsoft Windows. APFS is used by devices created by Apple, it is used across a wide range of devices including phones, tablets, TV appliances and computers.  Lastly, there is the Linux operating system, which uses a variety of file systems, depending on the version which is installed. Common varieties include ext3/ext4 and btrfs. More specialized file systems for specific appliances are also in use. The exact intricaties and technical documentation of a file system are often not available outside of its vendor which means that software vendors have to reverse engineer a file system to a degree. Expect a forensic investigation suite to continually improve support for popular file systems.

Once a disk image has been created it is possible to calculate its checksum. A checksum can be used to verify the integrity of a disk image. This is of paramount importance during a forensic investigation. Evidence will always need to be retrieved from other systems. Calculating a checksum at both ends, the source and destination file(s), will ensure that no anomalies are present. When a checksum matches at both ends, this means that no anomalies are present, the contents of the file match exactly and can be used in a forensic investigation. In order to create a checksum, a hash is created.  A hash is a mathematical, one-way calculation, performed by a specific algorithm. The MD5 and SHA1 algorithms are commonly used in the forensic community although other algorithms can be used as well. 

After validation of the checksum, the created image will be ready to use in an investigation. Forensic investigation suites will use the disk image as a basis for the investigation, allowing an forensicator to browse the file system for pertinent files and other forensic artifacts. Post-processing will also occur in many forensic suites, automatically parsing popular artifacts, thereby making investigation easier. 

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

In scenario's in which it is not feasible to get access to phyical media, a Live USB might provide an alternative. A Live USB contains an operating system which can be booted during the boot phase of a computer. In order for a live USB to function it is required to interupt the boot cycle of a computer and select the boot from USB option. Manufactuers have different hotkeys to access this functionality. Note that it is also possible to boot from a CD/DVD in a similar manner, in that case, select the CD/DVD option.  While it is still neccessary to take a server or service offline it is not required to open it up and take a hard drive. Similarily, continuous miniturization means that some SSD's can no longer be removed from a motherboard. 

Luckily there are a number of free Live USB tools that can be used to circumvent these limitations and acquire forensic images. One of the most well known tools is **CAINE** (Computer Aided Investigative Environment)  (www.caine-live.net). CAINE is a Linux live environment and mounts any discovered drives as read-only by default to ensure the forensic integrity of the disks. It provides GUI-based tools for the following operations:



- Imaging of a disk (Guymager)
- Disk Image Mounter (Xmount)
- DDrescue 
- Enabling write operations
- Mounting remote file systems across a network



In addition to its disk imaging tools, it provides a forensic environment which can be used to perform most forensic operations including accessing various filesystems, recover data, performing memory analysis and other operations.


Another example of a forensic Live USB environment is **Sumuri Paladin Edge**. This Live USB environment is available free of charge at their website (www.sumuri.com). In addition to imaging the entire disk it also allows you to convert images, find specific files,extract unallocated space and interface with network shares.

 It is recommended to have a Live USB option within your lab at all times and to equip your forensicators with USB drives in case of onsite client emergencies. 



### Disk imaging on Windows and Linux 

Situations might occur when a particular system cannot be turned off. There are various ways to perform a forensic acquisition depending on the operating system. 

#### Windows 

**FTK Imager** (https://www.exterro.com/forensic-toolkit) is a well-known tool to perform disk acquisitions on a Windows host. It is part of the FTK forensic suite developed by Exterro. However the imager is also available free of charge. FTK Imager can either be installed on the host operating system or it can be used in a "lite" mode. Lite mode is prefferable as no changes are performed on the disk, however be aware that it affects RAM memory.

FTK Imager can be used to perform the following operations:

- Disk acquisitions (both physical and logical)
- Memory acquisitions
- Acquisitions of the Windows Registry
- Browse the filesystem and select relevant files/folders

The following steps can be used  to create a "Lite" version which runs in memory. These steps are based on the official guide provided by Exterro to the forensic community:

- Install FTK Imager on another workstation
- Insert a USB drive
- Copy the installation folder to the USB-drive
- Perform a hashing operation to ensure file integrity is in order

#### Linux


Linux historically has an integrated utility capable of copying files called **dd**. dd can also be used for disk imaging, however it was not build with forensics in mind. A duo of utilities is available to perform forensic disk imaging, the tools are called **dcfldd** and **dc3dd**. Both tools can be used to perform disk imaging, their main advantage over dd is integrated hashing support for various hashing algorithms. 

All three utilities utilize the available Linux block devices in /dev/ to perform a physical disk image capture. A few examples are included below. **Be warned that these tools can and will destroy evidence if used incorrectly**



### Virtual machines

Virtual machines have become commonplace in the IT industry, in short allowing an organization to scale resources without purchasing additional hardware. The use of virtual machines is also advantageous for imaging purposes. A client can offer to send the virtual hard drive files for forensic investigation. After performing the customary hashing procedures these files can then be converted if necessary . FTK Imager supports conversion of VMDK files to any other FTK image format, which in turn can be used by a forensic program or forensic suite. 

**qemu-img** can be used to convert various hard drive image formats to raw dd format. An example covering the conversion of a vmdk file is included below. 

‘’’

qemu-img convert -f vmdk -O raw image.vmdk image.img
‘’’


## Memory forensics 

### Background 

While the disk forensics focus on forensic artifacts from files and folders, more pertinent information can also be readily available within a computer's memory. A computer's memory, called Random Access Memory or RAM for short, is used to carry out all active tasks of a computer. As such it contains a wealth of artifacts not available through other means. For instance:

- A list of active and (potentially) recently terminated processes
- Active network connections
- Entered system commands
- Open file handles

In order to collect this information an application will  perform a memory dump. A memory dump is exactly what it sounds like, the contents of the RAM extracted to a disk. Be aware that as the size of the RAM increases, an equivalent amount of disk space should be readily available for storage. Furthermore, the RAM does not remain in stasis while the extraction takes place. It will continue to perform tasks and will continue to change for the duration of the RAM dump. 

### Windows


Performing a memory dump on Windows can be performed by multiple tools. FTK Imager was already mentioned in the previous section. An alternative to FTK Imager in this regard is the utility **DumpIt** (https://github.com/thimbleweed/All-In-USB/tree/master/utilities/DumpIt). DumpIt can be used without installation on the host system. The directory it is launched from also doubles as the destination directory. Take this into consideration before performing a memory dump. 

### Linux

There is no single version of Linux, every single distribution has its own intricacies and (minor) differences. A tool was needed that can perform a memory dump independent of installed kernels, packages or other dependencies. Microsoft actively develops **AVML** (https://github.com/microsoft/avml). AVML can be used to perform a memory dump and also has a few tricks of its own. AVML supports compression of memory dumps to decrease the amount of required disk space as well as uploads to a Microsoft Azure Blob store

The standard usage of AVML is shown below:

‘’’
avml output.lime
‘’’

It is possible to generate a compressed image with the following command:

‘’’
avml —compress output.lime.compressed
‘’’

For a full set of commands please refer to the GitHub development page. 


### Virtual Machines

The use of virtual machines has become commonplace in the IT industry and of course this impacts memory acquisition as well with its own advantages and disadvantages. One advantage is that memory collection has become easier. A virtual machine hypervisor allows a virtual machine to be suspended, hitting the pause button, and freezing all activity. During this process the contents of the RAM are written to disk, no additional tools are neccessary to perform an acquisition. Files from popular vendors like VMware and Virtualbox can be analyzed by memory analysis tools like Volatility. 


