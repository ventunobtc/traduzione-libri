## What is Bitcoin?

Bitcoin is a *peer to peer electronic cash*, a new form of digital money that can be transferred between people or computers without any trusted middleman (such as a bank), and whose issuance is not under the control of any single party. 

Think of a paper dollar or physical metal coin. When you give that money to another person, they don't need to know who you are. They just need to trust that the cash they get from you is not a forgery. Typically people do this with physical money using just their eyes and fingers, or using special testing equipment for larger amounts.

As we've shifted to a digital society, the majority of our payments are now made over the Internet by means of a middleman service: a credit card company like Visa, a digital payment provider such as PayPal or Apple Pay, or an online platform like WeChat in China.

The movement toward digital payments brings with it the reliance on a central actor that has to approve and verify every payment. This is because the nature of money has changed from a physical thing you can carry, transfer, and verify yourself, to digital bits that have to be stored and verified by a third party that controls their transfer.

As we give up our cash for convenient digital payments, we also create a system where we give extraordinary powers to those who would seek to oppress us. Digital payment platforms have become the basis of dystopian authoritarian systems of control such as those used by the Chinese government in order to monitor dissidents and prevent citizens whose behavior they don't like from purchasing goods and services.

Bitcoin offers an alternative to centrally controlled digital money with a system that gives us back the person to person nature of cash, but in a digital form:

1.  A digital asset (typically *bitcoin* with a lowercase *b)* whose supply is limited, known in advance, and unchangeable. This stands in stark contrast to the paper notes and digital versions thereof issued by governments and central banks, whose supply expands at an unpredictable rate.
2.  A bunch of interconnected computers (the *Bitcoin network)*, which anyone can join by running a piece of software. This network serves to issue bitcoins, track their ownership, and transfer them between participants without relying on any middlemen such as banks, payment companies, and government entities.
3.  The Bitcoin client software, a piece of code that anyone can run on their computer to become a participant in the network. This software is open source, which means that anyone can see how it works, as well as contribute new features and bug fixes to it.

![Bitcoin network](images/Bitcoin-capital-B.png)

*Bitcoin is a network of computers running the Bitcoin client software.*


We'll get into the motivations behind Bitcoin in the next section.

### Where Did It Come From?

Bitcoin was invented by a person or group known by the pseudonym of [Satoshi Nakamoto](https://en.wikipedia.org/wiki/Satoshi_Nakamoto) around 2008. No one knows the identity of this person or group, and as far as we know, they've disappeared and haven't been heard from for years.

On Feb 11, 2009, Satoshi wrote about an early version of Bitcoin on an online forum for *cypherpunks*, people who work on cryptography technology and are concerned with individual privacy and freedom. Though this isn't the first official release announcement of Bitcoin, it does contain a good summary of Satoshi's motivations, so we'll use it to lay the ground work for our discussion.

The relevant bits are extracted below. In the next section, we'll walk through some of these statements and try to understand what problems of the current financial system Satoshi was solving:

> *I\'ve developed a new open source P2P* *e-cash system called Bitcoin. It\'s completely decentralized, with no central server or trusted parties, because everything is based on crypto proof instead of trust. \[...\]*
>
> *The root problem with conventional currency is all the trust that\'s required to make it work. The central bank must be trusted not to debase the currency, but the history of fiat currencies is full of breaches of that trust. Banks must be trusted to hold our money and transfer it electronically, but they lend it out in waves of credit bubbles with barely a fraction in reserve. We have to trust them with our privacy, trust them not to let identity thieves drain our accounts. Their massive overhead costs make micropayments impossible.*
>
> *A generation ago, multi-user time-sharing computer systems had a similar problem. Before strong encryption, users had to rely on password protection to secure their files \[...\]*
>
> *Then strong encryption became available to the masses, and trust was no longer required. Data could be secured in a way that was physically impossible for others to access, no matter for what reason, no matter how good the excuse, no matter what.*
>
> *It\'s time we had the same thing for money. With e-currency based on cryptographic proof, without the need to trust a third party middleman, money can be secure and transactions effortless. \[...\]*
>
> *Bitcoin\'s solution is to use a peer-to-peer network to check for double-spending. In a nutshell, the network works like a distributed timestamp server, stamping the first transaction to spend a coin. It takes advantage of the nature of information being easy to spread but hard to stifle. For details on how it works, see the design paper at [[http://www.bitcoin.org/bitcoin.pdf]](http://www.bitcoin.org/bitcoin.pdf)*
>
> Satoshi Nakamoto

### What Problems Does it Solve?

Let's break down some of Satoshi's post. Throughout the book, we will cover how these concepts are actually implemented. Don't worry if something feels unfamiliar in this section, as we'll cover it in depth later. The idea here is to see Satoshi's goals so that we can aim to achieve them as we go through the exercise of *Inventing Bitcoin.*



> *I've developed a new open source P2P e-cash system*

P2P stands for *peer to peer* and indicates a system where one person can interact with another without anyone in the middle, as equal peers. You may recall P2P file sharing technologies like Napster, Kazaa, and BitTorrent, which first enabled people to share music and movies with each other without a middleman. Satoshi designed Bitcoin to allow people to exchange *e-cash*, electronic cash, without going through a middleman in much the same way.

The software is *open source*, which means that anyone can see how it works and contribute to it. This is important as it removes the requirement to trust Satoshi. We don't need to believe anything Satoshi wrote in his post about how the software works. We can look at the code and verify how it works for ourselves. Furthermore, we can evolve the functionality of the system by changing the code.



> *It\'s completely decentralized, with no central server or trusted parties...*

Satoshi mentions that the system is *decentralized* to distinguish it from systems that do have central control. Prior attempts to create digital cash such as DigiCash by David Chaum were backed by a *central server*, a computer or set of computers that was responsible for issuance and payment verification, under the control of one corporation.

Such centrally controlled private money schemes were doomed to failure; people can't rely on a money that can disappear when the company goes out of business, gets hacked, suffers a server crash, or is shut down by the government.

Bitcoin, on the other hand, is not run and controlled by a single company, but rather by a network of individuals and companies all over the world. To shut down Bitcoin would require shutting down tens to hundreds of thousands of computers around the world, many in undisclosed locations. It would be a hopeless game of wack-a-mole as any attack of this nature would simply encourage the creation of new Bitcoin *nodes,* or computers on the network.



> *...everything is based on crypto proof instead of trust*

The Internet, and indeed most modern computer systems, are built on cryptography, a method of obscuring information so that only the recipient of the information can decode it. How does Bitcoin get rid of the requirement of *trust?* We'll dive into this later in the book, but the basic idea is that instead of trusting someone that says "I am Alice" or "I have \$10 in my account," we can use cryptographic math to state the same facts in a way that is very easy to verify by the recipient of the proof but impossible to forge. Bitcoin uses cryptographic math throughout its design to allow participants to check the behavior of everyone else without trusting any central party.



> *We have to trust \[the banks\] with our privacy, trust them not to let identity thieves drain our accounts*

Unlike using your bank account, digital payment system, or credit card, Bitcoin allows two parties to transact without giving up any personally identifying information. Centralized repositories of consumer data stored at banks, credit card companies, payment processors, and governments are giant honeypots for hackers. As if to prove Satoshi's point, Equifax was massively compromised in 2017, leaking the identities and financial data of more than 140 million people to hackers.

Bitcoin decouples financial transactions from real world identities. After all, when we give physical cash to someone, they don't need to know who we are, nor do we need to worry that after our exchange they can use some information we gave them to steal more of our money. Why shouldn't we expect the same, or better, from digital money?



> *The central bank must be trusted not to debase the currency, but the history of fiat currencies is full of breaches of that trust*


*Fiat*, which is Latin for "let it be done," refers to government and central-bank issued currency which is decreed as legal tender by the government. Historically, money was created from things that were hard to produce, easy to verify, and easy to transport, such as seashells, glass beads, silver, and gold. Any time something was used as money, there was a temptation to create more of it. If someone came along with superior technology for quickly creating lots of something, that thing lost value. This is how European settlers were able to strip the African continent of its wealth, by trading easy for them to produce glass beads for hard to produce human slaves. This is why gold was considered such a good money for so long---it was hard to produce more of it quickly.[^1]

We slowly shifted from a world economy that used gold as money to one where paper certificates were issued as a claim on that gold. Eventually, the paper was entirely separated from any physical backing by Nixon, who ended the international convertibility of the US dollar to gold in 1971.

The end of the gold standard allowed governments and central banks full permission to increase the money supply at will, diluting the value of each note in circulation, known as *debasement*. Although government-issued, redeemable for nothing, pure fiat currency is the money we all know and use day to day, it is actually a relatively new experiment in the scope of world history.

We must trust our governments not to abuse their printing press, but we don't need to look far for examples of *breaches of that trust*. In autocratic and centrally planned regimes where the government has their finger directly on the money machine, such as Venezuela, the currency has become nearly worthless. The Venezuelan Bolivar went from 2 Bolivar to the U.S. dollar in 2009 to 250,000 Bolivar to the U.S. dollar in 2019. As I write this book, Venezuela is in the process of collapse due to the terrible mismanagement of its economy by its government.

Satoshi wanted to offer an alternative to *fiat* currency whose supply is always expanding unpredictably. In order to prevent *debasement*, Satoshi designed a system of money where the supply was fixed and issued at a predictable and unchangeable rate. There will only ever be 21 million bitcoins, though each bitcoin can be divided into 100 million units now called satoshis, producing a final total of 2.1 quadrillion satoshis in circulation around the year 2140.

Prior to Bitcoin, it was not possible to prevent a digital asset from being infinitely reproduced. It is cheap and easy to copy a digital book, audio file, or video and send it to your friend. The only exceptions to this are digital assets controlled by middlemen. For example, when you rent a movie from iTunes, you can watch it on your device only because iTunes controls the delivery of the movie and can stop it after your rental period. Similarly, your digital money is controlled by your bank. It is the bank's job to keep a record of how much money you have, and if you transfer it to someone else, they can authorize or deny such a transfer.

Bitcoin is the first digital system which enforces scarcity without any middlemen and is the first asset known to humanity whose unchangeable supply and schedule of issuance is known completely in advance. Not even precious metals like gold have this property, since we can always mine more and more gold if it is profitable to do so. Imagine discovering an asteroid containing ten times as much gold as we have on earth. What would happen to the price of gold given such abundant supply? Bitcoin is immune to such discoveries and supply manipulations. It is simply impossible to produce more of it, and we'll explain why in later chapters.

The nature of money and the workings of the existing monetary system are intricate, and this book will not cover them in depth. If you would like to know more about the fundamentals of money as they apply to Bitcoin, I would recommend *The Bitcoin Standard* by Saifedean Ammous as a starting point.

> *Data could be secured in a way that was physically impossible for others to access, no matter for what reason, no matter how good the excuse, no matter what. \[...\] It\'s time we had the same thing for money*

Our current systems of securing money, such as putting it in a bank, rely on trusting someone else to do the job. Trusting such a middleman not only requires confidence that they won't do something malicious or foolish, but also that the government won't seize or freeze your funds by exerting pressure on this middleman. However, it has been demonstrated time and time again, that governments can and do shut down access to money when they feel threatened.

It might sound silly to someone living in the United States, or another highly regulated economy, to contemplate waking up with your money gone, but it happens all the time. I've had my funds frozen by PayPal simply because I hadn't used my account in months. It took me over a week to get restored access to "my" money. I'm lucky to live in the United States, where at least I could hope to seek some legal relief if PayPal froze my funds, and where I have basic trust that my government and bank won't steal my money.

Much worse things have happened, and are currently happening, in countries with less freedom, such as [banks shutting down during currency collapses](https://www.nbcnews.com/business/business-news/greece-crisis-banks-shut-week-restrictions-imposed-atms-n383606) in Greece, banks in Cyprus proposing bail-ins to confiscate funds from their customers, or [the government declaring certain bank notes worthless](https://www.washingtonpost.com/world/asia_pacific/india-invalidates-large-bank-notes-in-crackdown-on-crime/2016/11/08/cc705ee2-a5c6-11e6-ba46-53db57f0e351_story.html?utm_term=.7951cf519c00) in India.

The former USSR, where I grew up, had a government controlled economy leading to massive shortages of goods. It was illegal to own foreign currencies such as the US dollar. When we wanted to leave, we could only exchange a limited amount of money per person to US dollars under an official government mandated exchange rate that was vastly divorced from the true free market rate. Effectively, the government stripped us of what little wealth we had by keeping an iron grip on the economy and the movement of capital.

Autocratic countries tend to implement strict economic controls, preventing people from withdrawing their money from banks, carrying it out of the country, or exchanging it for not-yet-worthless currencies like the US dollar on the free market. This allows the government free reign to implement insane economic experiments such as the socialist system of the USSR.

Bitcoin does not rely on trust in a third party to secure your money. Instead Bitcoin makes your coins *impossible for others to access* without a special key that only you hold, *no matter for what reason, no matter how good the excuse, no matter what*. By holding Bitcoin, you hold the keys to your own financial freedom. Bitcoin separates money and state

> *Bitcoin\'s solution is to use a peer-to-peer network to check for double-spending \[...\] like a distributed timestamp server, stamping the first transaction to spend a coin*

A *network* refers to the idea that a bunch of computers are connected and can send messages to each other. The word *distributed* means that there is not a central party in control, but rather that all the participants coordinate to make the network successful.

In a system without central control, it's important to know that nobody is cheating. The idea of *double-spending* refers to the ability to spend the same money twice. This is not a problem with physical money as it leaves your hand when you spend it. Digital transactions, however, can be copied just like music or movies. When you send money through a bank, they make sure that you can't move the same money twice. In a system without central control, we need a way to prevent this kind of *double-spending*, which is effectively the same as forging money.

Satoshi is describing that the participants of the Bitcoin network work together to *timestamp* (put in order) transactions so that we know what came first, and therefore we can reject any future attempts to spend the same money. In the next few chapters, we will build this system from the ground up. It will enable us to detect forgery without relying on any central issuer or transaction validator.

***

Bitcoin was not an invention made in a vacuum. In his paper, Satoshi cited several important attempts at implementing similar systems including Wei Dai's b-money, and Adam Back's Hashcash. The invention of Bitcoin stood on the shoulders of giants, but no one prior had put all the right pieces together, creating the first system for issuing and transferring a truly scarce digital money without central control. 

Satoshi tackled a number of interesting technical problems in order to address the issues of privacy, debasement, and central control in current monetary systems:

1.  How to create a peer to peer network that allows anyone to voluntarily join and participate.
2.  How a group of people that don't have to reveal their identities or trust each other can maintain a shared ledger of value, even if some of them are dishonest.
3.  How to allow people to issue their own unforgeable currency without relying on a central issuer while maintaining the scarcity of that currency so that production of new units isn't a free-for-all.

When Bitcoin was launched, only a handful of people used it and ran the Bitcoin software on their computer *nodes* to power the Bitcoin network. Most people at the time thought it was a joke, or that the system would reveal serious design flaws that would make it unworkable.

Over time, more people joined the network, using their computers to add security to the network and reinforcing that it had value by exchanging other currencies for it, or accepting it for goods and services. Today, ten years later, it is used by millions of people with tens to hundreds of thousands of nodes running the free Bitcoin software, which is developed by hundreds of volunteers and companies worldwide.

Let's figure out how we can build this system!

***
[^1]: For a great overview of monetary history, I recommend the essay *Shelling Out* by Nick Szabo: <https://nakamotoinstitute.org/shelling-out/>

