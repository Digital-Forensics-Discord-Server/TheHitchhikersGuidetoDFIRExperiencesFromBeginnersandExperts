#  Most Common Data Stores in Mobile Forensics

<img src="https://user-images.githubusercontent.com/28718987/161664557-e72d881c-b61b-427c-b8d3-26d8d7477763.png" width="100" height="100" />

By Alexis Brignoni

Online presence: [https://linqapp.com/abrignoni](https://linqapp.com/abrignoni)

## The Artisanal Approach

Most mobile forensic examinations involve the use of third party tools to extract and decode information stored whitin targeted devices. What happens when the tool presents little to nothing of what is expected? What to do when the targeted app seems to not exist as far as the tool is concerned?

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

Is is important to note that this chapter will touch on the most common locations and types of data needed for analysis. It is not an all encompassing guide to mobile forensics nor does it intend to be so. Without further ado let's dive in.

### Relevant Apps in Android
In Android devices the apps keep most user generated data in the following directory:

	/data/data/

As seen in figure 2.1 there are folders within the data directory for each app on the device. These folders are named in reverse URL format and are known as bundle identifiers (IDs.) For details on bundle IDs in Android see here: [https://developer.android.com/studio/build/configure-app-module ](https://developer.android.com/studio/build/configure-app-module)

<img width="365" alt="2.1" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot1.png"> 

Most mobile apps have bundle ID names that are easy to identify. Notice in the previous image how it is pretty obvious that com.android.chrome should be the bundle ID for the Chrome Browser, which it is. Another example would be how the bundle ID for Discord is com.Discord. Be aware that is not always the case. Not all bundle ID names are easy to reference back to the app name just by reading. One way of determining the budle ID of an app in Android is to look for the app in the Google Play store using a browser. 

<img width="913" alt="2.2" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot2.png">

The bundle ID is located in the URL at the top of the page.

	https://play.google.com/store/apps/details?id=com.discord&hl=en_US&gl=US

Let's look at TikTok.

<img width="920" alt="2.3" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot3.png">

Notice how the bundle ID for TikTok, com.zhiliaoapp.musically makes no obvious reference to TikTok at all. 

	https://play.google.com/store/apps/details?id=com.zhiliaoapp.musically&hl=en_US&gl=US
	
By changing the Google Play store URLs to the possibly unknown bundle IDs found on the target extraction one can determine the common app name for it.

It is of note that apps also save data to additional locations within the Android device. Look for targeted bundle ID directories in the following locations:

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

<img width="913" alt="2.4" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot4.png">

How can then we take these GUID named directories and linked them to the corresponding bundle IDs?

### Option 1: applicationState.db
This data store is a SQLite database that contains information for all currently installed applications. We will discuss SQLite databases in the next section. The database is located here:

	/private/var/mobile/Library/FrontBoard/applicationState.db
	
The exemplar data in the following image is from Josh Hickman's test iOS images. These can be found here: 
https://thebinaryhick.blog/public_images/

<img width="913" alt="2.5" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot5.png">

The tool used for this output is iLEAPP and can be found here: https://github.com/abrignoni/iLEAPP


Notice how the database can provide the bundle ID, the app name, and the corresponding GUID values within the paths.

### Option 2: iTunesMetadata.plist & BundleMetadata.plist
These data stores are property lists (plist) and will be discussed in the next section. The files reside in each /private/var/containers/Bundle/Application/\*GUID directory*/ folder per app. It contains a wealth of information regarding the app for each folder.

<img width="913" alt="2.6" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot6.png">

### Option3: .com.apple.mobile\_container_manager.metadata.plist
Like the previous option the data store is a plist. The plist is contained in the /private/var/mobile/Containers/Shared/AppGroup/\*GUID directory\*/ and /private/var/mobile/Containers/Data/PluginKitPlugin/\*GUID directory*/ folders. Notice the period at the start of the plist filename. If using a macOS for analisys make sure to enable the view hidden files options in order to not miss them.

<img width="913" alt="2.7" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot7.png">

As discussed previously bundle IDs might not be anywhere close to their commercial or well known app names. The following URL has a useful database of iOS bundle IDs and corresponding app names: 

	https://offcornerdev.com/bundleid.html
	
See the following output for Snapchat.

<img width="913" alt="2.8" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot8.png">

## Common Data Stores in Mobile Forensics

We have identified the locations where user generated data, by app, can be stored both in Android and iOS. Now we look at what file structures are involved. Let's start with the current king of mobile data storage.

### SQLite Relational Databases

SQLite is the most used database engine in the world. It is a relation database. A simple way of thinking about them is by imagining a set of spreadsheets that have things in common. For this example we will use DB Browser for SQLite as our tool to access SQLite databases. It can be downloaded here: [https://sqlitebrowser.org/](https://sqlitebrowser.org/)

SQLite databases usually have the .sqlite or .db extension but that might not always be the case. What is always the case is that if you open a suspected SQLite database with a hex or text editor you will see 'SQLite format 3' at the start of the file. This is known as the file header and it is a sure fire way of confirming you are dealing with a SQLite database.

Using DB Browser for SQLite we will open a database named test.db for analysis. It is a simple database consisting of two spredsheets of data, tables in SQLite parlance. By using the Browse Data the content of these tables can be seen.

Customers Table

<img width="913" alt="2.9" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot9.png">

Addresses Table

<img width="913" alt="2.10" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot10.png">

These tables record the customer's names and addresses. A customer can have one or more addresses in the addresses table. How to we know what addresses correspond to what customer? Notice how the customerID column in the Customers table identifies each customer uniquely. This is called a Primary Key. These same values can be found in the Addresses table under AddressID. When that is the case they are know as a Foreign Keys. The purpose of a foreign key is to identify that row of data as being part of (relational) to the primary key. We can match the customer with the correct address by finding tprimary key in the Customers table and match it with the same foreign key in the Addresses table.

To tell the database to match customers to addresses we use a set of commands called Structured Query Language (SQL). We will tell the database to gives us all columns from both tables where the CustomerID in the customer's table is the same as the AddressID in the addresses table.

`SELECT * 
FROM Customers, Addresses
where CustomerID = AddressID`

<img width="913" alt="2.11" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot11.png">

Each customer has been match with the proper address or addresses. Notice the asterisk after the SELECT command, it means we want all columns that are responsive to the query. SQL allows us to really narrow down how much data we want from the database. If I want obtain only the addresses that are related to Alexis Brignoni we would query the database the following way:

`SELECT *
FROM Addresses
INNER JOIN Customers
ON CustomerID = AddressID
WHERE CustomerID = 1`

<img width="913" alt="2.12" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot12.png">

The last query uses an inner join. These are the most common way of putting together data from two or more tables. An inner join will return rows from multiple tables when a condition is met. In our example we wanted all the data and only the data for CustomerID number 1.

SQLite databases can be pretty large with many tables and a multitude of primary and foreign keys to keep track of. Thankfully there are plenty of online resources on structured query language and with a little of patience and practice anyone can be able to pull relevant data out of these databases.

As we examine these databases we have to take into account temporary files SQLite uses as it works. These are write-ahead log and roll-back journal files. These files, if available, will have the same name as the database with either a -wal or -journal extension.

<img width="913" alt="2.13" src="https://raw.githubusercontent.com/Digital-Forensics-Discord-Server/CrowdsourcedDFIRBook/main/manuscript/resources/Ch2/Screenshot13.png">

These temporary files might contain data not found in the database and will require examination with tools that support their forensic review. An authoritative book on the subject can be found here: [SQLite Forensics by Paul Anderson](https://www.amazon.com/SQLite-Forensics-Paul-Sanderson/dp/1980293074)



### JSON - Java Script Object Notation
