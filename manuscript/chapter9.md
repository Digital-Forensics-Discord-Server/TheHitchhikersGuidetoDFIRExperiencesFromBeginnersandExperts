# Chapter Nine

# Chapter Nine - Gamification of DFIR: Playing CTF's

<img src="https://user-images.githubusercontent.com/48143894/162533767-1d6eca8a-98c7-446b-a970-807bd3deb588.png" width="200" />

By [Kevin Pagano](https://twitter.com/KevinPagano3) | [Stark 4N6](https://startme.stark4n6.com)

## What is a CTF?

The origins of CTF or “Capture The Flag” were found on the playground. It was (still is?) an outdoor game where teams had to run into the other teams zones and physically capture a flag (typically a handkerchief) and return it back to their own base without getting tagged by the opposing team. In the information security realm it has come to mean a slightly different competition.

## Why am I qualified to talk about CTFs?

Humble brag time. I’ve played in dozens of CTF competitions and have done pretty well for myself. I am the proud recipient of 3 DFIR Lethal Forensicator coins from SANS, one Tournament of Champions coin (and trophy!), a 3-time winner of Magnet Forensics CTF competitions, a 4-time winner of the BloomCON CTF competition, and a few others. I’ve also assisted in the creation of questions for some CTF competitions as well as creating thorough analysis write-ups of events I’ve competed in on [my personal blog](https://ctf.stark4n6.com).

## Types of CTFs

Two of the most common information security types of CTF competitions are “**Jeopardy**” style and “**Attack and Defense**” style.

“**Jeopardy**” style typically is a list of questions with varying difficulty and set defined answers. The player or team is given some sort of file or evidence to analyze and then has to find the flag to the question and input it in the proper format to get points.

![](https://ctf.zone/img/jeopardy.png)

***Figure 1: Jeopardy style CTF (Image via ctf.zone)***

“**Attack and Defense**” is more common in Red and Blue team environments where the Red team has to hack or attack a Blue team server. The Blue team subsequently has to try and protect themselves from the attack. Points can be given for time held or for acquiring specific files from their adversary.

![](https://ctf.zone/img/attack_defense.png)

***Figure 2: Attack and Defense CTF (Image via ctf.zone)***

Depending on the CTF, you may see a combination of types with it being Jeopardy style and linear (story based) with some questions hidden or locked until a certain question is answered.

For this chapter, I will go more in-depth regarding the “Jeopardy” style competitions, more specifically, forensics geared CTF competitions.

## Evidence Aplenty

With forensics CTF’s, just like in real life, any type of device is game for being analyzed. In the ever growing landscape of data locations, it just provides us more places to look for clues to solve the problems. One of the more well known forensic CTF’s is the [SANS NetWars](https://www.sans.org/cyber-ranges/) tournaments. These are devised with 5 levels with each level being progressively harder than the last. In this competition you will have a chance to analysis evidence from:

 - Windows computer 
 - macOS computer 
 - Memory/RAM dump 
 - iOS dump 
 - Android dump
 - Network (PCAP/Netflow/Snort logs)
 - Malware samples

You can see from the above list that you get a well rounded variety of types of evidence that you most likely will see in the field on the job. In other competitions I’ve played you could also come across Chromebooks or even Google Takeout and other cloud resources as they become more common. I have also seen some where they are more crypto based so working with different ciphers and hashes to determine the answers.

## Who’s Hosting?

As previously mentioned, **SANS** is probably the most well known provider of a forensics CTF through their NetWars program. It isn’t cheap as a standalone, but is sometimes bundled with one of their training courses. You can sometimes see them hosted for free with other events such as OpenText’s enFuse conference.

As for others, **Magnet Forensics** has been hosting a CTF for the past 5 years in tandem with their user summit. This has been created by Jessica Hyde in collaboration with some students from Champlain College’s Digital Forensics Association. Some previous Magnet CTF’s were also created by Dave Cowen and Matthew Seyer for context.

Other software vendors have started to create their own as well to engage with the community. **Cellebrite** in the past 2 years has hosted virtual CTF competitions and **Belkasoft** has created and put out multiple CTFs the last 2 years. [**DFRWS**](https://dfrws.org/forensic-challenges/) hosts a yearly forensic challenge with past events covering evidence types such as Playstation 3 dumps, IoT (Internet of Things) acquisitions, mobile malware, and many others.

Another fantastic resource for finding other challenges is [**CyberDefenders**](https://cyberdefenders.org/blueteam-ctf-challenges/). They host hundreds of various different CTF challenges, from past events and other ones that people have uploaded. You can even contribute your own if you’d like as well as allow them to host your next live event. 

![enter image description here](https://i.ibb.co/SdqWtZw/blueyard.png)

***Figure 3: CyberDefenders website***

Another fairly exhaustive list of other past challenges and evidence can be found hosted on [**AboutDFIR**](https://aboutdfir.com/education/challenges-ctfs/).

## Why Play a CTF?

So at the end of the day, why should YOU (yes, YOU, the reader) play a CTF? Well, it depends on what you want to get out of it.

### For Sport

Growing up I’ve always been a competitive person, especially playing sports like baseball and basketball, CTF’s are no different. There is a rush of excitement (at least for me) competing against other like-minded practitioners or analysts to see how you stack up. You can even be anonymous while playing. Part of the fun is coming up with a creative handle / username to compete with. It also keeps the commentary and your competitors on their toes.

I personally like to problem solve and to be challenged which is part of the reason why I enjoy playing.

### For Profit

I put profit in quotations because many may construe that as a compensation type objective. While many CTF challenges do have prizes such as challenge coins or swag ( awesome branded clothing anyone?!) that’s not completely the profit I’m talking about here. The profit is the knowledge you gain from playing. I’ve done competitions where I never knew how to analyze memory dumps at all and I learned at least the basics of where to look for evidence and new techniques to try later on in real world scenarios.

> "Commit yourself to lifelong learning. The most valuable asset you'll
> ever have is your mind and what you put into it." - Albert Einstein

The knowledge you gain from the “practice” will inevitably help you in the future, it's just a matter of time. Seriously, you don't know what you don't know. Remember when I said you can be anonymous? It doesn't matter if you get 10 points or 1000 points, as long as you learn something new and have fun while doing so, that's all that matters.

## Toss a Coin in the Tip Jar

I get asked all the time, "what are your keys to success playing CTFs?". That's probably a loaded question because there are many factors that can lead to good results. Here I will break down into sections that I feel can at least get you started on a path forward to winning your first CTF.

### Tips for Playing - Prior

First and foremost is the preparation phase. Like any task in life, it always helps to be prepared for the battle ahead. Having a sense of what is to come will help with your plan of attack. Do your research! If you know that a specific person created the CTF then take a look at their social media profiles. Often times they will release hints in some form or fashion, whether it is webinars they have shared or research papers or blog posts they have recently published. Don't over do it though, there could be red herrings amuck. You can also look at past CTF's they have created, seeing how questions were formulated before and what sort of locations they tend to lean on for flags. This is part of the reason why I personally do write-ups of past CTF's for future reference.

Each CTF rules may be different but if teams are allowed reach out to colleagues or others to form a squad. Knowledge from multiple people well-versed in different topics can help in spreading out the workload especially if there are multiple forms of evidence to be analyzed. I would be remiss if I didn’t say that some of my winning efforts were with team members who helped pick up sections where I wasn't as strong. Your mileage may vary though, make sure to coordinate your efforts if you do join a team as to not waste time all working on the same questions.

If evidence is provided ahead of the competition make sure to spend some time getting familiar with it. Process the evidence ahead of time so you aren't wasting time during the live competition waiting on machine time. Some of these events only last 2-3 hours so time is of the essence. This segues right into building out your analysis machine and your toolkit. Make sure that all your system updates are completed prior. The last thing you need is an errant Windows update to take down your system while you watch the spinning.

![](https://3.bp.blogspot.com/-MXprM2uLx4Y/XZ0g4hImh6I/AAAAAAAAEVo/fVV_PHGlAqwS9rVkMf9KIVcSYPvB3TdwQCLcBGAsYHQ/s1600/update-faker-windows-update.jpg)

***Figure 4: "This will take a while"***

You may also consider making sure you have local admin access or at least the ability to turn of antivirus (if you are analyzing malware) to your computer. Always do so in a controlled environment if possible but you knew this already (I hope). If you are provided a toolkit or a trial of a commercial license, use it to your advantage, even if it's a secondary set of tools. There are times some vendors will make sure that the answer is formulated in a way that their tool will spit out from their own software. Also, commercial tools can potentially speed up your analysis compared to a bunch of free tools but that is personal preference.

### The Toolkit

I'm a Windows user through and through so I cannot offer much advise from a Mac or Linux perspective. With that said, I do have some tools that I use from a forensic perspective to analyze those types of evidence. Here are my favorite (free) tools that I use during CTF's:

**General Analysis**
- [Autopsy](https://www.autopsy.com/)
- [Bulk Extractor](https://github.com/simsong/bulk_extractor)
- [DB Browser for SQLite](https://sqlitebrowser.org/dl/)
- [FTK Imager](https://www.exterro.com/ftk-imager)
- [Hindsight](https://dfir.blog/hindsight/)

**Chromebook**
 - [cLEAPP](https://github.com/markmckinnon/cLeapp)

**Ciphers**
 - [CyberChef](https://gchq.github.io/CyberChef/)
 - [dcode.fr](https://www.dcode.fr/en)

**Google Takeout / Returns**
 - [RLEAPP](https://github.com/abrignoni/RLEAPP)

**Mac**
 - [mac_apt](https://github.com/ydkhatri/mac_apt)
 - [plist Editor - iCopyBot](http://www.icopybot.com/plist-editor.htm)

**Malware/PE**
 - [PEStudio](https://www.winitor.com/)
 - [PPEE (puppy)](https://www.mzrst.com/)

**Memory/RAM**
 - [MemProcFS](https://github.com/ufrisk/MemProcFS)
 - [Volatility](https://www.volatilityfoundation.org/releases)

**Mobile Devices**
 - [ALEAPP](https://github.com/abrignoni/ALEAPP)
 - [Andriller](https://github.com/den4uk/andriller)
 - [APOLLO](https://github.com/mac4n6/APOLLO)
 - [ArtEx](https://www.doubleblak.com/software.php?id=8)
 - [iBackupBot](http://www.icopybot.com/itunes-backup-manager.htm)
 - [iLEAPP](https://github.com/abrignoni/iLEAPP)

**Network**
 - [NetworkMiner](https://www.netresec.com/?page=NetworkMiner)
 - [Wireshark](https://www.wireshark.org/)

**Windows Analysis**
 - [Eric Zimmerman tools / KAPE](https://ericzimmerman.github.io/#!index.md)
 - [USB Detective](https://usbdetective.com/)

This whole list could be expanded way further but this is the majority of the go-to's in my toolkit.

### Tips for Playing - During

We've all been there, you get to a point in the middle of a CTF and you start to struggle. Here are some things to key in on while actually playing.

Read the titles of the questions carefully, often times they are riddled with hints about where to look. "*Fetch"* the run time of XXX application, maybe you should analyze those Prefetch files over there. Questions will often also tell you what format the answer should be in when submitting. This may tell you that that timestamp you're hunting could be incorrect, those pesky timezone offsets!

Did you find a flag that appears to be a password? It's almost guaranteed that that evidence was placed in such a way that it will be reused. Emails and notes can be a treasure trove for passwords to encrypted containers or files.

One thing that may seem silly but can help is to just ask questions. If you're stumped on a question, talk to the organizer if you can, they may lead you in a direction that you didn't think of when you set off on a path of destruction.

![](https://i.postimg.cc/3N8Ps9yF/Screenshot-2022-06-20-204105.png)

***Figure 5: "Don't Sweat It, Take the Hint"***

Some CTF competitions have a built in hint system. If they don't count against your overall store, take them! The chances of a tie breaker coming down to who used less hints is extremely small. If the hint system costs points you will need to weigh the pros and cons of not completing a certain high point question as opposed to loosing 5 points for buying that hint.

The last tip while playing is to write down your submissions, both the correct and incorrect ones. I can't tell you the amount of times I've entered the same answer wrongly into a question to eventually get points docked off my total. This will not only help you during the live CTF but afterwards if you are writing a blog on your walkthroughs.

### Strategies

There are multiple strategies that you could use for attacking the questions during the competition. Usually they will be broken out into different categories by type of evidence such as Mobile / Computer / Network / Hunt. Some people prefer to try and finish all questions in one section before jumping to the next one. If you're really good at mobile forensics that may be a good strategy if you are less experieinced than other areas.

Another potential strategy depends on how many points the questions are worth. Usually the more the points the harder the question. Some people prefer to try and get high point questions first to put large points on the scoreboard and put the pressure on other competitors. Others prefer to go for the lower point questions first and work their way up.

My personal strategy is a combination of them all. I will typically go more towards the easy points first and work my way up from there but I will jump from different evidence categories once I get stuck for a time period. Depending on how much prework analysis has been done, I may have inferred references to areas that need to be analyzed so I may look at questions that I may already have answers for.

And then there are the ones that are confident (sometimes too confident!). Some players knowing that they have the answers already will hold off on submitting for points until very late in the competition to mess with the other competitors. Some CTF competitions will freeze the board the last 15-30 minutes to make the final scores a surprise to all. I would advise against this tactic but if you're that confident then by all means. At the end of the day it is up the whatever suits the player the best.

>"You miss 100% of the shots you don't take – Wayne Gretzky" – Michael Scott

## Takeaways

What is it that you can takeaway from playing a CTF you ask? You may have different feelings on what you got out of playing CTF's but here are a few of my personal takeaways.

### Documentation

One of the things I enjoy doing after playing a CTF is to do blog writeups of solutions. If there are questions I didn't get to finish during the live competition I have a tendancy to go back and revisit to see if I can solve them properly. Once I have a majority of the answers I will start to write some blogs on how I solved the questions. Not only does this help me document my results for future usage but also helps with gaining experience in more technical writing. I can't tell you the many times that I've referenced my own posts in other competitions or in research as I go back to further dive into file system locations that I had never looked at before.

Documentation is critical in a lot of aspects of an investigation so it only makes sense to write down your notes in case you need to reference where a specific artifact came from. The best part is that not all questions will be solved the same so I thoroughly enjoy reading other solver's thought process to get to the end result.

### Challenge Yourself & Build Confidence

I'm going to stress it again, playing CTF's will help you learn. For those that don't get to work with some of the different evidence files like Linux or network files will give you plenty to take home from analyzing them. Before playing the SANS NetWars I had rarely touched PCAP files let alone knew how to utilize Wireshark to pull out files or specific packets. Learning about Google Takeout exports has given me a new appreciation for what potential evidence can be found in the cloud and what may not be found directly on a mobile device. This has lead to me doing my own research and contributing back to the community in tools like RLEAPP and other open-source projects. These are just a few examples of getting out of your comfort zone and challenging yourself to learn about new tools and techniques.

It's also important to build your confidence. Just because you don't place well the first time you play doesn't mean you can't get better. I know when I started out I struggled in competitions. I didn't know where to go to find answers or how to get to them. It all comes back to practice. Any sports athlete will tell you that repetitions of a task will only make you better at that specific task and this correlates with CTF's and examinations. If you see something often enough you'll start seeing patterns like Neo in the Matrix.

![](https://user-images.githubusercontent.com/48143894/179990282-aba4739c-9dc9-463d-9394-ed7c635b052f.png)

***Figure 6: "I know kung-fu!"***

### Have Fun!

The number one takeaway of playing CTF's is to have fun! These are meant to be a training exercise to stimulate the mind and to give you a break from your normal workload. Don't stress it, just keep learning. If you're in person, enjoy the comradery of other competitors and build your network. You never know who you may meet while playing and who you will harbour friendships with in the industry.

I hope this chapter breathes new life into you playing CTF competitions. Good luck and see you all out their on the digital battlefields!

