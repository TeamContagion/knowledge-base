So you want to work on a crypto challenge. Now what? Here are some steps for approaching a crypto chalenge:
1. Read the challenge description and title
2. Download and analyze the related files
3. Identify the challenge task
4. Research the challenge
5. Attempt solutions

## Read the challenge description and title
The first step in approaching any challenge is reading the challenge. This step is fairly basic, but important nonetheless.
When giving a challenge description an initial read, it's helpful to identify several things:
- What encryption scheme are they using? Is it a standard, or custom?
- What language is it written in?

## Download and analyze the related files
Pretty self explanatory. Download the challenge files, then read the code and familiarize yourself with it. 
You don't necessarily need to understand exactly how it works, just get a feel for what each function does.
For example, you don't need to understand how exactly some function called `F` works, but figure out that it's used to encrypt data.
You should also probably run the file locally.
Crypto challenges are generally pretty safe and won't brick your machine, but always understand code before you run it and a VM is still recommended.
Pro tip: If it's python, you can import the file in an interpretter and call the functions one at a time with varying parameters to get a feel for what they do.

## Identify the challenge task
Now that you have a general idea of how the file works, identify what it is the challenge is asking you to do. 
Are you trying to break the encryption given a set of parameters?
Are you trying to break the encryption given an arbitrary set of parameters?
Do you simply have to reverse engineer the custom encryption scheme?
Usually in cryptography challenges you can find a clear goal to work towards and identifying what exactly that is will help you in the next steps.

## Research the challenge
If you know how to solve the challenge you can skip this step, but usually challenges involve things we don't know or don't understand.
So the next step is to understand.
The first step in general is to understand the crypto system. Even custom crypto systems are typically based in real crypto system. 
Next, you probably will have to attack the system. Research known attacks for the system.
Usually the attacks only work under certain conditions, so make sure you understand what makes the attack work or not work.
And what's the first step in researching any challenge?
**Google the challenge name**. It uses some custom scheme called the "Ravin Crypto System"? A quick google finds a real scheme called the Rabin Crypto System.
Sometimes the challenge name refers to an attack. 
The challenge is about buying poodles through a command line? Google the crypto system and "poodle" and you'll find information on the POODLE attack.

## Attempt solutions
The final step is to start throwing things at the challenge. 
By this point, hopefully you understand what the challenge wants, what crypto system it uses, and some possible attacks to achieve what it wants.
Write up some code and perform those attacks!
Some tips for when you're trying an attack:
- If it's a brute force attack, add a progress bar that updates every 50 attempts or so. Challenges won't require you to run a brute force for hours, so if you're making slow progress, you probably need to fine tune your attack or find a different approach.
- Try your attack with a trivial example (something easy to solve) to make sure that your attack works before throwing it at the challenge
- Document your attacks and why they failed as you go. Not only will this help when making a write up (please do write ups), but it will also help if you really do need to use that attack. Sometime you just need a bit more info and the attack actually will work and it will help you explain your work so far if you get someone else to help.
