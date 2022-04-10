#  Most Common Data Stores in Mobile Forensics

<img src="https://user-images.githubusercontent.com/28718987/161664557-e72d881c-b61b-427c-b8d3-26d8d7477763.png" width="100" height="100" />

By Alexis Brignoni

Online presence: [https://linqapp.com/abrignoni](https://linqapp.com/abrignoni)

## The Artisanal Approach

Most mobile forenisc examinations involve the use of third party tools to extract and decode information stored whitin targeted devices. What happens when the tool presents little to nothing of what is expected? What to do when the targeted app seems to not exist as far as the tool is concerned?

A big part of digital forensics involves what I call The Artisanal Approach. The Oxford Languages dictionary defines artisanal as: 
		
		ar·ti·san·al
		/ärˈtēzən(ə)l/
		adjective
		- relating to or characteristic of an artisan.
		"artisanal skills"
		- (of a product, especially food or drink) made in a traditional or non-mechanized way.
		"artisanal cheeses"
		
This is just a long way of saying that we will rely have to manually identify the relevant data stores. The approach has 3 steps.

1. Locate the relevant apps.
2. Identify the data stores for the app and extract meaningful items.
3. Report generation.

On this chapter we will focus mostly on step number two. We will discuss what type of data stores are mostly seen in mobile forensics and suggest cost effective (i.e. cheap) solutions to traige these sources. Let's dive in.

## Locate Relevant Apps

The mobile forensics world is divided, mainly, between two dominant operating systems. These are Google's Android and Apple's iOS operating systems. As such both will organize things in vastly different ways within their file systems. This chapter will present examples from a full file system extraction view of Android and iOS devices. Even when working from a different type of extraction the main concepts, and the handling of data stores, will be the same. For details on mobile extraction types and their differences see here: [https://privacyinternational.org/long-read/3256/technical-look-phone-extraction](https://privacyinternational.org/long-read/3256/technical-look-phone-extraction)

Is is important to note that this chapter will touch on the most common locations and types of data needed for analysis. It is not an all encompasing guide to mobile forensics nor does it intend to be so. Without further ado let's dive in.

### Relevant Apps in Android
In Android devices the apps keep most user generated data in the following directory:

	/data/data/

As seen in figure 1 there are folders within the data directory for each app on the device. These folders are named in reverse URL format and are known as bundle identifiers (IDs.) For details on bundle IDs in Android see here: [https://developer.android.com/studio/build/configure-app-module ](https://developer.android.com/studio/build/configure-app-module)

<img width="365" alt="figure 1" src="https://github.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/blob/main/manuscript/resources/Chapter%202/Screen%20Shot%202022-04-06%20at%202.41.50%20PM.png?raw=true"> 

Most mobile apps have bundle ID names that are easy to identify. Notice in the previous image how it is pretty obvious that com.android.chrome should be the bundle ID for the Chrome Browser, which it is. Another example would be how the bundle ID for Discord is com.Discord. Be aware that is not always the case. Not all bundle ID names are easy to reference back to the app name just by reading. One way of determining the budle ID of an app in Android is to look for the app in the Google Play store using a browser. 

<img width="913" alt="Screen Shot 2022-04-06 at 2 23 04 PM" src="https://github.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/blob/main/manuscript/resources/Chapter%202/Screen%20Shot%202022-04-06%20at%202.23.04%20PM.png?raw=true">

The bundle ID is located in the URL at the top of the page.

	https://play.google.com/store/apps/details?id=com.discord&hl=en_US&gl=US

Let's look at TikTok.

<img width="920" alt="Screen Shot 2022-04-06 at 2 21 53 PM" src="https://github.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/blob/main/manuscript/resources/Chapter%202/Screen%20Shot%202022-04-06%20at%202.21.53%20PM.png?raw=true">

Notice how the bundle ID for TikTok, com.zhiliaoapp.musically makes no obvious reference to TikTok at all. 

	https://play.google.com/store/apps/details?id=com.zhiliaoapp.musically&hl=en_US&gl=US
	
By changing the Google Play store URLs to the possibly unknown bundle IDs found on the target extraction one can determine the common app name for it.

It is of note that apps also save data to additional locations within the Android device. Look for targeted bundle ID direcotries in the following locations:

	/data/media/
	/MNT/ or /NONAME/

As you navigate the contents of these directories you will find relevant stores that can contain user generated data. 

### Relevant apps in iOS

In iOS devices user generated data can be found in the following directories:

	/private/var/containers/Bundle/Application/*GUID directory*/
	/private/var/mobile/Containers/Shared/AppGroup/*GUID directory*/
	/private/var/mobile/Containers/Data/PluginKitPlugin/*GUID directory*/

Notice the \*GUID directory* at the end of the paths. These will be subsituted with a corresponding global unique identifier. See the following example: 

	A72DDBEE-8EEE-4868-9E5A-769B078781EA
	
These values can change constantly due to app installs, updates, and uninstalls. Unlike Android devices iOS bundle IDs are not part of the application directory paths therefore it is impossible to identify applications of interest visually by bundle ID names.

<img width="913" alt="Screen Shot 2022-04-06 at 2 23 04 PM" src="https://github.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/blob/main/manuscript/resources/Chapter%202/Screen%20Shot%202022-04-10%20at%204.58.01%20PM.png?raw=true">

How can then we take these GUID named directories and linked them to the corresponding bundle IDs?

###Option 1: applicationState.db
This data store is a SQLite database that contains information for all currently installed appications. We will discuss SQLite databases in the next section. The database is located here:

	/private/var/mobile/Library/FrontBoard/applicationState.db
	
The exemplar data in the following image is from Josh Hickman's test iOS images. These can be found here: 
https://thebinaryhick.blog/public_images/

<img width="913" alt="Screen Shot 2022-04-06 at 2 23 04 PM" src="https://github.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/blob/main/manuscript/resources/Chapter%202/Screen%20Shot%202022-04-10%20at%205.11.30%20PM.png?raw=true">

The tool used for this output is iLEAPP and can be found here: https://github.com/abrignoni/iLEAPP


Notice how the database can provide the bundle ID, the app name, and the corresponding GUID values within the paths.

###Option 2: iTunesMetadata.plist & BundleMetadata.plist
These data stores are property lists (plist) and will be discussed in the next section. The files reside in each /private/var/containers/Bundle/Application/\*GUID directory*/ folder per app. It contains a wealth of information regarding the app for each folder.

<img width="913" alt="Screen Shot 2022-04-06 at 2 23 04 PM" src="https://github.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/blob/main/manuscript/resources/Chapter%202/Screen%20Shot%202022-04-10%20at%205.24.01%20PM.png?raw=true">

###Option3: .com.apple.mobile\_container_manager.metadata.plist
Like the previous option the data store is a plist. The plist is contained in the /private/var/mobile/Containers/Shared/AppGroup/\*GUID directory\*/ and /private/var/mobile/Containers/Data/PluginKitPlugin/\*GUID directory*/ folders. Notice the period at the start of the plist filename. If using a macOS for analisys make sure to enable the view hidden files options in order to not miss them.

<img width="913" alt="Screen Shot 2022-04-06 at 2 23 04 PM" src="https://github.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/blob/main/manuscript/resources/Chapter%202/Screen%20Shot%202022-04-10%20at%205.35.52%20PM.png?raw=true">

As discussed previously bundle IDs might not be anywhere close to their commercial or well known app names. The following URL has a useful database of iOS bundle IDs and corresponding app names: 

	https://offcornerdev.com/bundleid.html
	
See the following output for Snapchat.

<img width="913" alt="Screen Shot 2022-04-06 at 2 23 04 PM" src="https://github.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/blob/main/manuscript/resources/Chapter%202/Screen%20Shot%202022-04-10%20at%205.40.22%20PM.png?raw=true">

## Common Data Stores in Mobile Forensics

We have identified the locations where user generated data, by app, can be stored both in Android and iOS. Now we look at what file structures are involved. Let's start with the current king of mobile data storage.

### SQLite Relational Databases