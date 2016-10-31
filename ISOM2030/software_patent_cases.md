#Software Protection Patents, Copyright, Licenses, and Discussion of Software Business Cases

###Lotus vs Borland Case:
Lotus earlier, Borland made Quattro, a new spreadsheet editor (like excel)
that is much better than Lotus 1-2-3. A lot of new innovations as argued by
Quattro.

Court favored Lotus, they agreed that the menu part (which Quattro copied) is 
a copyrightable expression due to the **look and feel** of the menu. 

Mode of operation which Quattro debated that they are allowed to copy, is copyable.
However Quattro copied the appearance of this, which is not allowed.

The menu command hierarchy cannot be copyrighted as it functional in nature. However
different names of calling it is allowed to be copyrighted. 

As in they can make something be able to do the same thing as
the copyrighted spreadsheet program, but in a different way. 
If they copy it exactly however, is not allowed and they can get sued.

#####Implication of this case:
- APIs : maybe protected by copyright
- Operational aspects versus artistic expression: is the thing that you
are accused of a violation an industry standard? 
- Basis for litigation for infringement: this case used as an example
to help judge other cases similar to this
- Basis for defenses too

#####Common defenses to such litigation: 
- External Factors: such as compatibility
- Industry Standard: a lot of companies in the industry use the
same commands to do the same thing. Implies not unique to you.

###Altai Test of Copyright Infringement
**_Non-literal_** copying of "literary works" by paraphrasing the part that is being copied.
Rather than exact word for word copying, they copy the **essence** of the work.

Checking done on whether the overlaps is because of the sharing of the same
underlying idea behind the work, or is it exactly that the second author
copied the first author.

So at what level do we allow copyright? Still debated by court

Thus, comes the **Three Step Test in Altai Case** :
- Step 1 : Abstraction
    - Take the allegedly violating program 
    - Identify each level of abstraction (identify the words of code, find
    the higher level design, step by step till reach the overall theme of the program or book) 
    - And then for each level, find the overlaps (find the same parts). 
- Step 2 : Filtration
    - Separating the protected and non-protected elements, i.e. : people's names, 
    what is artistic and what is not, etc.
- Step 3 : Comparison
    - Were the protected parts copied? If it is too close, and the infringer has access to
    the whatever is being copied, it most likely will be decided that it is a copyright infringement.

#####Court Ruling:
Altai was guilty. Because the employee was from the old company (which is now suing Altai)
and he was approaching and solving the same problem with the same methods that he used
for his old company. Resulting in virtual duplication that was clearly apparent.

Thus Altai had to rewrite the whole application with a fresh team, removing anyone who
had been exposed to that employee and his code, and remove all the code that isn't constrained
by external factors or doesn't belong in the public domain.

#####Implications:
- On Screen Displays: Don't copy the display exactly, change how it looks
- Data Structures / Tables : 
- Subroutine structure and number
- Substantive equivalency : Solving the same problem in the same way, can get you sued
very well.
- Functional equivalency : Solving the same problem, should not get you sued because you can't
copy the way something work. Should be okay if you call it something different. i.e. Microsoft calls
it SAM, we need to call it differently. Unless it is an industrial standard.
- Non-literal copying : paraphrasing something while still actually doing the same
thing is copying
- Prohibited functionality for copyright : no problem, cannot be copyrighted

Basically cannot copy the structure!!

###Game Genie Business Case
A lot of suing on the software field is mostly done in the field of 
video games. Why?

People say that in business software, it is harder to get sued to copying because
it is more factual. However in games, its purpose is mostly entertainment. Resulting in 
it mostly is an **artistic expression**, something which copyright laws are mostly 
created to do.

In the Game Genie Case, they created an add-on or extension that you can stick
to change some values in the game cartridge before sending it to the CPU. Changing the
behaviour of the game. 

Nintendo doesn't like this. Thus they sued the Game Genie creators for copyright infringement claiming that
it is a derivative work.

Company defends themselves, saying that it is Fair Use. Thus we check step by step :
- Nature of the work : fiction (bad)
- Purpose of the copying : profit (bad)
- First Amendment : doesn't apply
- Motive of the defendant : profit (bad)
- Percentage of the work taken : Nintendo could argue, that the Game Genie
copied the whole work and added a little bit of modifications. But Game Genie could
argue, that they didn't do that, they passed the data through and only changed a little bit.
- Commercial Implications : Game Genie: because to be able to use Game Genie, you have to buy
a Nintendo device to use Game Genie. Nintendo: loss of opportunity. 

However, there are a lot of proof internally that Nintendo actually hates this 
Game Genie technology. Which would contradict what they said about opportunity loss.
If they don't like it, why would they make it?

Why does Nintendo hate this technology anyway? Because Game Genie is 
something like a cheat code. And it means that it takes away the challenge, it
becomes boring. So Nintendo's concern is that it makes the games too easy. Thus making
it less attractive to buy the game or even the console.

Game Genie's counterargument:  We don't make it extremely too easy, we just give the users
a little edge / a modest advantage. Because if it is too easy then Game Genie would also not
be able to sell anything.

Which appeals to the user because it might make it easier for them to play 
games that are too hard for them.

Judge doesn't know who to rule for, too many conflicting arguments.

Other defenses that maybe claimed by Game Genie:
- Parody: maybe, if the game has funny elements
- First Sale Doctrine: Allows someone who has bought something to modify
what they own, i.e. you buy a book you can write on it. Also applies to programs!
First Sale Doctrine allows modification for ease of use. Argument from Game Genie
is that here in this case, the person doing the modification is the user, they
were simply giving them some tools to help them modify. 

From fair use POV only, it is hard for the judge to decide, but with the
first sale doctrine defense, it strengthens their argument a lot. 

###Stern Electronics vs Kaufman
Scramble game, made in Japan, copyrighted in Japan, and licensed to US
market through Stern.

Omni alleged that only code is copyrighted, and that they didn't do any copying
of the code itself. Only copied the appearance of the game on the screen.

Court Ruling : Look and feel is copyrightable, Stern wins.

Thus further reinforcing the findings from Lotus case that **look and feel** is copyrightable.

###Data East USA vs Epxy
The two companies had a similar Karate Championship Fighting Game. 

The question was that whether copyright was violated by the 2nd company. Result:
- District court said yes
- Appeals court said no!

Issues? 
- Most of what was overlapping were based on Karate as a sport, (interesting note
you can copyright a sport, example: Rugby) but Karate was not copyrightable because it is too old
to be copyrighted, already in the public domain. Or they were limitations, inherent to the computer systems
implementation (external factors).
- The parts of the game itself or the simulation of the game is an artistic 
expression, the copyrighted part, is not the same.
    - Colors, floor mats outfits, etc different (Minor diff)
    - Characters included, one company used Asians as fighters, 
    other used Americans (Major diff).
    
Meaning that if you manage to make it look differently wherever possible,
you can still get away with it.

###MAI Systems vs Peak Computer
This case changed the law!

Simply loading an OS into the RAM is making a copy, violating
a strict interpretation of copyright law.
- RAM is a "fixed" medium of expression, loading code is like photocopying a book
- Peak argued RAM is not fixed, court disagreed.

People debated this. Thus as a response to this, US congress passed a modification
to copyright law due to this case. The extension is to allow some "copies" of computer
programs when necessary for use (if owned).

Thus, legal to make copies if :
- Copy created is part of an essential to the effective utilization of
the software with a machine and is used in no other manner.
- Copy created is for archival or backup purposes only.

All copies must be destroyed when the work is sold to a new owner.

###Midway Manufacturing vs Artic
Creation of a speeded up version of a video game by replacing the circuit board
which allows for a faster and more exciting game.

Claim by Midway is that this is a derivative work.

Two judges debated that whether this is an actual derivative work or not.

Case is on the borderline of copyright law.

Derivative work is a lot broader than what it was before. Meaning that
software is becoming more protected over time.
