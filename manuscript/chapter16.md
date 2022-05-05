# Chapter 16 - Artifacts as Evidence
---
## Types of Artifacts
Digital Forensics is a six phase process including Preparation, Identification, Collection, Preservation, Analysis and Reporting.

Analysis is a major phase where in forensicators discover different types of artifacts ranging from plain metadata to complex evidence of execution and residual traces. The vast gap between the difficulty to retrieve or reconstruct evidence determines the fine line between E-discovery and Digital Forensics.

User data such as internet history, images, videos, emails, messages etc fall under E-discovery. It is relatively easy to reconstruct even from the unallocated space. 

However, System Data like artifacts that help support some view of truth, or determine how closely a transpired event is to the evidence, are not that simple to manually parse with forensic soundess, which is why oftentimes forensicators rely on well-known parsing tools either commercial or opensource.

![EDvsDF](https://user-images.githubusercontent.com/28131554/166871681-24cfd09a-76e6-48d0-9487-b968f38a5af9.jpg)

And that is the main difference between E-Discovery & Digital Forensics depending on the categorization of data alone. Both follow different procedures and have different scope of execution. Generally, E-Discovery can be contained to only the logical partitions and the unallocated region whereas Digital Forensics operates in a much wider scope solely due to the necessity of dealing with complex data structures.

---
## What is Parsing?
Which brings us to parsing. We often go around throwing the term  while working with a variety of artifacts;
"Parse this, parse that", but what does it mean in the real sense? To understand the parsing methodology, tools & techniques, we must be familiar with the origin of the handling of the data being parsed. What I mean by that is how was the data originally meant to be handled. What was it's structure by design. How can it be replicated.

Generally, it is some feature or underlying mechanism of the main operating system installed on the device. Parsing tools are written to accurately mimic those functions of the operating system which make the raw data stored on the hardware, human readable.

<img width="503" alt="Computer_Structure" src="https://user-images.githubusercontent.com/28131554/166871680-d302e610-3775-4ff9-99a2-f70b610ad795.png">

Understand the operating system as an abstraction level between the end-user and the intricacies of raw data. It provides an interface to the user which hides all the complexities of  computer data and how it is being presented.

---
## Artifact-Evidence Relation
You will come across an ocean of different artifacts in your investigations, but artifacts have a very strange relationship with what might potentially be considered evidence. Artifacts alone do not give you the absolute truth of an event. They provide you tiny peepholes through which you can reconstruct and observe a part of the truth. In fact, one can never be sure if what they have is indeed the truth in it's entirety.

![Truth](https://user-images.githubusercontent.com/28131554/166871678-2bd07780-ceaa-4fbd-bd44-b3685076f4a4.jpg)

I always love to draw an analogy between the artifacts and the pieces of a puzzle, of which you're not certain to have the edge or the corner pieces. You gather what you can collect, and try to paint the picture as unbiased and complete as possible.

![Puzzle](https://user-images.githubusercontent.com/28131554/166871682-7dfe4e29-8d76-45b2-b5cd-62b7ce7a60d6.png)

That being said, if you apply the additional knowledge from metadata, OSINT and HUMINT to the parsed artifacts, you might have something to work with. For instance, say you were assigned an employee policy violation case, where the employee was using their work device for illegally torrenting movies. Parsing the artifacts alone will give you information around the crime, but not as evidence. You would still need to prove that the face behind the keyboard at the time of the crime, was indeed the one that your artifacts claim. So you would then look for CCTV camera footage around the premises, going back to the Identification phase in the digital forensics lifecycle, and so forth and so on.

As a result of a codependency of the artifacts on drawing correlations to some external factor, they form a direct non-equivalence relation with evidence.

However, note that this "rule", if you will, is only applicaple to a more broad scope of the investigation and will generally be handled by the lawyers. In the more narrow scope as a forensicator, and for the scope of your final forensic report, artifacts are most critical. Just keep it in the back of your mind that encountering an artifact alone does not mean it's admissible evidence. Parse the artifact, make notes and document everything. Being forensically sound is more important than worrying about completing the entire puzzle. Because there will be no edge or corner pieces of the puzzle.

---
## Examples
This section will cover how some of the more uncommon artifacts can play into a case from the bird's eye view.

### Registry
### Prefetch
### Shellbags
### Jumplists & LNK files
### SRUM
### $MFT
### $130
### \$LogFile
### hiberfil.sys


