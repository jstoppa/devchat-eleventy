---
layout: layouts/post.njk
title: >
  265 RR Timely Dataflow with Frank McSherry
date: 2016-06-22 07:00:39
episode_number: 265
duration: 01:03:12
audio_url: https://media.devchat.tv/ruby-rogues/RR265DataFrankMcSherry.mp3
podcast: ruby-rogues
tags:
  - ruby_rogues
  - podcast
---

02:33 - Frank McSherry Introduction

- [Twitter](https://twitter.com/frankmcsherry)
- [GitHub](https://github.com/frankmcsherry/)
  03:06 - Computation03:48 - When are more computers needed?04:28 - [Scalability! But at what COST?](https://www.frankmcsherry.org/assets/COST.pdf)
- Experimentation
  08:03 - Data Format and Pipelines
- [Hilbert Curve](https://en.wikipedia.org/wiki/Hilbert_curve)
  - [github.com/frankmcsherry/blog/blob/master/posts/2015-02-04.md](https://github.com/frankmcsherry/blog/blob/master/posts/2015-02-04.md)
    14:06 - Code That Could Grow
- [Hadoop](https://hadoop.apache.org/)
- [summingbird](https://github.com/twitter/summingbird)
  20:38 - Languages and Performance23:14 - “For Loops Unrolled”
- [Rust](https://www.rust-lang.org/)
  28:01 - Scaling
- [helix](https://github.com/rustbridge/helix)
  35:42 - Functional vs Procedural Language37:47 - Dataflow (Timely; Differential)
- Around, Epic
- [Vector Clock](https://en.wikipedia.org/wiki/Vector_clock)
- Introductory Blog Posts:
  - [github.com/frankmcsherry/blog/blob/master/posts/2015-09-14.md](https://github.com/frankmcsherry/blog/blob/master/posts/2015-09-14.md)
  - [github.com/frankmcsherry/blog/blob/master/posts/2015-09-18.md](https://github.com/frankmcsherry/blog/blob/master/posts/2015-09-18.md)
  - [github.com/frankmcsherry/blog/blob/master/posts/2015-09-21.md](https://github.com/frankmcsherry/blog/blob/master/posts/2015-09-21.md)
    &nbsp;Picks
- [Go-Ped Know Ped Scooter](https://goped.com/scooters/push/know-ped/) (Sam)
- [2015 State of the Software Supply Chain Report](https://www.sonatype.com/state-of-the-software-supply-chain) (Jessica)
- [The Screwtape Letters](https://en.wikipedia.org/wiki/The_Screwtape_Letters) (Jessica)
- [Start with Why: How Great Leaders Inspire Everyone to Take Action by Simon Sinek](https://www.amazon.com/Start-Why-Leaders-Inspire-Everyone/dp/1591846447/ref=sr_1_1?ie=UTF8&qid=1464715065&sr=8-1&keywords=start+with+why) (Chuck)
- [RIF6 Cube 2-inch Mobile Projector](https://www.amazon.com/RIF6-Projector-120-inch-Portable-Rechargeable/dp/B00QXS8L6I?ie=UTF8&psc=1&redirect=true&ref_=oh_aui_detailpage_o00_s00) (Chuck)
- [The Night Circus by Erin Morgenstern](https://www.amazon.com/Night-Circus-Erin-Morgenstern/dp/0307744434) (Frank)
- [PrAna](https://www.prana.com/men/bottoms/pants.html) (Frank)
- [Rust](https://www.rust-lang.org/) (Frank)
- [Big Data Analytics with Datalog Queries on Spark](https://yellowstone.cs.ucla.edu/~yang/paper/sigmod2016-p958.pdf) (Frank)

### Transcript

**JESSICA:&nbsp;** Three is a nice number of panelists.

**CHUCK:&nbsp;** Yeah.

**JESSICA:&nbsp;** Three is my favorite number.

[Laughter]

**_[This episode is sponsored by Hired.com. Every week on hired they run an auction where over a thousand tech companies in San Francisco, New York, and L.A. bid on Ruby developers providing them with salary and equity upfront. The average Ruby developer gets an average of 5 to 15 introductory offers and an average salary offer of $130,000 a year. Users can either accept an offer and go right into interviewing with a company or deny them without any continuing obligations. It's totally free for users. And when you're hired, they give you a $1,000 signing bonus as a thank you for using them. But if you use the Ruby Rogues link, you'll get a $2,000 instead. Finally, if you're not looking for a job but know someone who is, you can refer them to Hired and get a $1,337 bonus if they accept the job. Go sign up at Hired.com/RubyRogues.]_**

**_[I'm excited to tell you about a new sponsor to the show, Rollbar. One of the frustrating things about being a developer is dealing with errors. Ugh. Relying on users to report errors, digging through log files to debug issues, or a million alerts flooding your inbox ruining your day. With Rollbar's full-stack error monitoring, you get the context and insights and control you need to find and fix bugs faster. It's easy to install. You could start tracking production errors and deployments in eight minutes or less, or automatically create new issues in GitHub, JIRA, Pivotal Tracker, et cetera. They have a special offer for Ruby Rogues listeners. Go to Rollbar.com/RubyRogues to sign up and get the bootstrap plan free for 90 days. That's 300,000 errors tracked free. Give Rollbar a try today. Go to Rollbar.com/RubyRogues.]_**

**_[This episode is sponsored by Shippo. Shippo is a shipping API that connects you with over 15 different shipping carriers such as FedEx, UPS, USPS, Canada Post, and UberRUSH in one integration. You can use Shippo's APIs to compare shipping rates across carriers, print discounted labels, validate shipping addresses, track packages, and power your shipping in many different ways. You can connect directly to the API or use the provided Shippo Ruby gem to print your first label in a few minutes. The Shippo API is free to use. You only pay for the actual shipping label and a five-cent label fee. Sign up by going to GoShippo, that's G-O-S-H-I-P-P-O dot com slash Ruby Rogue to get six months with zero label fees.]_**

**CHUCK:&nbsp;** Hey everybody and welcome to episode 265 of the Ruby Rogues Podcast. This week on our panel we have Jessica Kerr.

**JESSICA:&nbsp;** Good morning.

**CHUCK:** Sam Livingston-Gray.

**SAM:&nbsp;** Now with 13% less sleep.

**CHUCK:&nbsp;** I'm Charles Max Wood from DevChat.tv and this week we have a special guest and that's Frank McSherry.

**FRANK:&nbsp;** Yeah, hello.

**CHUCK:&nbsp;** Do you want to introduce yourself, Frank?

**FRANK:&nbsp;** Yeah, sure. I'm a researcher basically. Formerly at Microsoft's research facilities in Silicon Valley where I did a lot of work on privacy, data privacy, and more recently on programming big systems like large distributed systems and computations. And I've been playing recently with some more modern programming, just trying to make that easy for people, get some of the fancy big compute cluster power behind relatively simple programs.

**JESSICA:&nbsp;** When you talk about computation you're talking about at a large scale?

**FRANK:&nbsp;** Yeah. We're thinking normally these big data, big analytics type things that people get a little bit excited about in the data science space. So yeah, you have a large pile of data that you hypothetically collected, depending on who you are, from your customers or from maybe you were doing open science type stuff. Maybe this is data that the government has pulled together about people out there and you're trying to sort through it. But there's a lot of it. And maybe it's a bit too much for your simple scopes to go through and munch. And you really want to figure out, how do I make this go fast? How do I bring in a lot of computers if needed to speed things along and get to the insights as quickly as possible to turnover ideas quickly and try out new things?

**SAM:&nbsp;** Well, you said bring in more computers if needed. How do we know if they're needed?

**FRANK:&nbsp;** Typically you start running it and it's really slow and you're like, “Oh wow. I wish I had more computers.” And at this moment, they are now needed. It's not obviously something you can see ahead of time. But typically if you guys sit down with maybe a hundred gigabytes of text data from [inaudible], you got the exciting Panama papers, you know ahead of time, “Well, I'm going to need a little bit of help here.” So, you sort of know that maybe your laptop isn't going to be beefy enough and you'd like to enough [other] resources you can. Or just at least write your program in a way that if you need to bring in more resources then it's not a painful sort of thing. You can start small starting in your laptop and then as you need more stuff, scale up and hopefully smoothly and pleasantly.

**JESSICA:&nbsp;** There was a piece of work that we read of yours in our paper reading group at Stripe. And it was about 'Scalability! But at what COST?' And this paper questions the part that, “Do we really need these super complicated data systems in order to crunch this data?” Can you talk about what you found there?

**FRANK:&nbsp;** Yeah, sure. This is a really fun paper. It's very therapeutic and cathartic. We've been doing all this work on the big data systems and hitting our heads against lots of things building really complicated and esoteric components. And we sort of scratched our head for a bit and looked at some of the performance numbers that other people were reporting with their big data systems. There are systems like Spark and Hadoop and Giraffe for graph processing and stuff like that. And you look at the numbers that they're reporting. You're like, “Well, hold on” and you do some little [back of the envelope] calculations for how long you think it really should take to do something. Some of the tests that they were doing. And these were, in this case it is mostly graph processing. If you have a large dataset of relationships you might want to ask questions about who's influential in that graph of relationships or who can communicate with whom.

We found that the numbers were up by a few orders of magnitude that yeah, if you just write, and I'm not even joking, just a simple for loop on your laptop in an appropriately performant language (like you don't want to be doing this in Perl necessarily but if you had something like C# or I was using Rust actually which I love) you could outperform these multiple, tens of machines, compute clusters, with just literally the 10 lines of code that's a for loop over the data. So, this was for us. And what I really liked about it is it's sort of a wakeup call we hope, that if you're going to be in this space, if you're going to be doing the big data, the “Let's be powerful with our computations stuff,” you really want to pay attention to performance. You don't want to be doing this, just screwing around and writing in a high-level fluffy language where you lose 10x and you have to pay it back in machines that you didn't have to begin with.

**CHUCK:&nbsp;** I want to jump in on this really quickly because I know that some people, especially people with large sets of data, they'll look at something like this and they'll say, “Okay, well that is the case on your data. But not necessarily the case on my data.” So, how do people run a similar experiment on their data to figure out if this is the way they want to move ahead?

**FRANK:&nbsp;** Yeah, it's a really good question. And it's definitely, we weren't trying, when we wrote the paper we weren't trying to tell people, “Yeah, there's never any good reason anymore to use any of these sorts of systems.” That's obviously not correct. There are some things that they are good at. It's a bit more of a different approach which is why not try it at least on your laptop first. Give it a whirl. See if that might work. If you take out all of the weird moving parts that these big systems have, it might work out okay. If it doesn't work out okay, absolutely. [Inaudible] have a conversation about where you go next. But again, it was just a little bit of a wakeup call in terms of there's a lot of fluff in a lot of these systems that you could hope to try to remove.

And that's sort of the second direction of work at least, is can we take those insights from making the [single] machines go fast and try to make the big machines go just as fast. They should be going faster by a lot than my laptop, and how do we do that, too? But I think yeah, it's mostly just, it's making the position that you should try it out. Try to run the stuff on your laptop. You got a billion records. That's not necessarily all that many. It sounds like a really big number but it's not even necessarily a lot of data.

**JESSICA:&nbsp;** Right. And memory is a lot cheaper these days. So, we can put an amazing amount of data on one computer. And you mentioned a couple of things. One was that it's not very many lines of code but you do need to use a language that's trying to go fast rather than a scripting language. Another thing that came up in some of your articles was the format of the data, that a terabyte of data in text format might not be a terabyte if you organized it in the right way.

**FRANK:&nbsp;** Yeah, that is totally actually one of my favorite take-aways. We followed up this cost paper. Some people came back and said, “Oh it's not really a lot of data if it fits on your laptop,” which is fair enough. So, we went and we grabbed the biggest dataset, graph dataset we could find, which is this Common Crawl dataset. It's about 128 billion edges. It's..,

**CHUCK:&nbsp;** Wow.

**FRANK:&nbsp;** Yeah, it's… I don't, I may not [inaudible] this anymore but it's a terabyte in binary. You don't get it in binary. You get it in compressed text which is decompressed would be enormous. And processing the entire dataset, so grabbing it, pulling it down, parsing all the integers, all this nonsense, 85% of the time spent there was in parsing text into binary numbers. So, if someone had just handed you the binary numbers in the first place, admittedly it's a less portable format, binary numbers. Text is nice and robust and you'd be able to read it 20 years from now.

But it was surprising to see that basically all but 1/6th of our time was spent just pushing characters around trying to figure out what number they were actually talking about. Turning it into binary so that we could process it. So, it's the sort of thing that yeah, if you [swing] the data around the right way first, if you're grinding over these enormous logs that you're producing that you wrote out in text to try to make all your friends happy. You wrote them out in JSON and you wrote all sorts of [hilarious] stuff there that comes out as several kilobytes when it could have just been 10 or 20 bytes written down in binary, this can be a huge, huge distinction in performance.

**JESSICA:&nbsp;** That's something I've noticed about functional programming in general is now I try to… I'm like, “Okay, I've got this data. First put it in the format that's most convenient to work on then do the work. Then convert back if necessary.” When we think about data pipelines that becomes such a difference. And this was a great example of how stuff that wasn't even possible in this low-overhead single laptop way became possible with some careful thought into arranging the data beforehand.

**FRANK:** Yeah, that's absolutely true. It's the sort of… I think you get some time to think about this. If you start with the text format and you start running over a terabyte of text you're going to have a lot of time to think about how you really wished you converted it to binary.

[Laughter]

**FRANK:&nbsp;** So, it does depend. Like if you're pulling in just a megabyte or so and it takes a fraction of a second as opposed to a fraction of a fraction of a second, who really cares? But if it's getting in your way, if it's the sort of thing that you're sitting there watching over and over again about all these strings that you're pulling down and hash maps that you're populating with strings and of horribleness, yeah at that point you say, “You know, maybe it matters [inaudible] for this point and I'll clean things up a bit.” So again, it depends totally on your environment. There are lots of situations where you don't need to worry about being complicated like this.

But with this data, yeah the 128 billion edges, it's something that you write it down the right way and it gets compressed down to about 40 gigabytes, which is pretty cool. You do the math on that and it ends up being less than three bits per edge or so. And you know, it's just sitting on my laptop right now because I don't need to get rid of it because I got plenty of space left. And it's sort of surprising that you can fit the largest web dataset that's currently out there on the internet. It fits on my iPhone, so that's interesting.

**SAM:&nbsp;** Yeah, I was reading through some of the links that you sent us beforehand. And it sounds like you were able to exploit some patterns in that data. I remember you used the phrase Hilbert Curve in there a couple of times which I don't know what that is. I haven't had that math. But it sounds like you have to be a little bit clever if you're going to approach problems in this way.

**FRANK:&nbsp;** Being clever helps. Yeah. There are simpler things than the Hilbert Curve. The Hilbert Curve is just a really cool way of, imagine you have a pen and you got a piece of paper in front of you and you want to draw all over the piece. You want to cover the paper in ink without lifting the pen and without crossing any lines at any point. It's just a way of filling in the paper where you sort of, you fill in the upper left corner first then you fill in the upper right corner and then the lower right and the lower left. And in each other's square's you start to pull the same trick. It's just a cute way of putting graph data I guess, two-dimensional points on your piece of paper into a straight line that has some nice properties.

And yeah, it's a little clever. That's true. It's the sort of thing that you pick up in a database class when you take one of those. But it's not the only thing out there. You get some similar though not quite as good performance if you use some off-the-shelf compression stuff. So, graph compression for example, there's this group doing research in Italy on graph compression. And they have a collection of standard tools that they put out that you can pull off the shelf. And you don't have to go and get a bunch of weird bits of math out. [Inaudible] use weird bits of math that other people have wrapped up for you which is always nice.

**JESSICA:&nbsp;** You do have to kind of treat each data input individually sometimes and not just generically “It's all JSON. It doesn't matter.”

**FRANK:&nbsp;** Yeah. It's definitely the case that the stuff that I was doing here was definitely bespoke Computer Science. This wasn't… I was sitting down and I know a lot about this type of data and you wouldn't want to have to pull me out every time you need to look at some graph data. So, it's the sort of thing… and you know, if it had been text instead I would have done something different. But you're right. It's definitely different approaches for different sorts of problems.

**JESSICA:&nbsp;** Which also, that's the whole NoSQL database options. It's the idea that different storage solutions solve different problems well.

**FRANK:&nbsp;** Completely, yeah. No, I totally agree. This is one of my favorite things about the whole… I don't know NoSQL from other sorts of… the thing people are pushing away from in a lot of ways when they're talking about NoSQL is that the database really wanted to have control over how they worked with their data. They wanted to tell them, “We've already figured out for you the smart things you can do with your data and [there are] choices.” And people said, “I have a slightly better idea about something I'd like to do.” And yeah, the NoSQL crowd basically just showed bunch of other really cool things that you could do, which was fun.

**JESSICA:&nbsp;** You mentioned something about code that could grow from something that could run on your laptop to something that could bring in other computers if needed. That's something that the system you're working on right now can do, eh?

**FRANK:&nbsp;** Yeah. I want to be clear. It's not just stuff that I do. There's a class of programming patterns or types of algorithms that have this property. So, if you look at things just like Hadoop or Spark, things that people know a bit more about, there are ways of writing computer programs that are meant to organically scale if you need to. And you when you write your program in one of these languages you can re-run it with twice as many computers if you want and it might go about twice as fast. Maybe not.

**JESSICA:&nbsp;** Maybe.

**FRANK:&nbsp;** Yeah. I mean, you know, we can negotiate on that. But these ways of writing programs, it's a bit like writing SQL in a database. Except SQL I think of as a bit restrictive. But you start writing against collections of data instead of trying to write one element at a time. Instead of writing your for loops unrolled you say, “I'd like to take these billion elements. I want to do the following thing. I want to take a join with my billion elements and these other billion elements over here.” And if you do that, if you just say, “I want to do a join,” the system underneath, it can go and figure out, “Well, how do I map that down to one computer or to ten computers or a hundred computers?” in the same way that a database is in principle smart enough to do this. These existing systems can do it.

I think that the difference arguably with I guess what I'm working on at the moment is a lot of these systems, these other systems that exist, the [inaudible], the Hadoops, are fairly low-level. They're sort of like, I feel a bit saying this, but like the Assembly language of parallel programming. You sort of give them fairly atomic instructions. You say, “Pick up this pile of data. Do a thing with it and then put it back down,” which is nice. It's nice that you can get a hundred computers to help you do that. But at the same time, it's not really a program yet. It's more like a shell script for big data [inaudible]. So, it's missing things like control structures, like you want to have a collection of a billion elements that you work on for a while, you iterate over them and do things repeatedly. These are the sorts of things that we're looking into I guess in this new project.

**JESSICA:&nbsp;** At Stripe we use Hadoop for batch processing. We've got Scalding on top of Hadoop for the batch processing every day. But then we also have a whole other system with umpteen more computers and Redis and S3 is involved and HDFS is involved. And yeah, we have the other system which is Summingbird, a whole other Scala framework, and this is to do real-time processing so we can have numbers that are like within five minutes. But then we have to combine those with yesterday's batch results. There are a lot of moving parts just to count things.

**FRANK:&nbsp;** Yes. That's totally true. The whole reason I truly started doing this work, a lot of this work, the science behind it started back at Microsoft research. And we were looking into could we not possibly unify a bunch of these things? And a lot of the principles that they work on are pretty similar. They take large collections of data and they spread them out to a bunch of computers and they get each of the computers to help out doing basically the same sort of computation. Then they bring the results back together. Surely we don't need yeah, a hundred different systems doing each of these thing separately that you then have to stick together with a bunch of scripts and post-it notes about how each of these systems actually work so that you can remember when it's actually safe to collect the results or not.

And the research, the work that we're doing, was basically going into what's a common, what's a language, like a common set of idioms that each of these systems use so that they could interact if they needed to? Which we compile them down to, in some sense. We wanted to just talk about what Summingbird does, what Storm does, what Spark does, what each of these systems do in a common language. A common, again sorry, not programming language but common idioms and whatnot. What do they need to say about how they work with data, how they consume it, how they produce it, and what it means for them to be done or partially done. And yeah, our goal is absolutely, can we not thin down this herd a little bit so that instead of having to install a whole bunch of different systems that register themselves with various, ZooKeeper [inaudible] and how know how they're configured.

You just have, I don't want to say one system because that seems a bit hopeful. But you have a substantially fewer systems out there and there's a much higher barrier to inventing a new one, right? All of these things came into existence for good reasons. They came into existence, Summingbird came into existence because they weren't getting the latency and performance that they needed out of things like Hadoop. So, it's there for a reason. It's maybe about time to sort of bring a bunch of these things together and unify them up.

**JESSICA:** You mentioned that Hadoop enabled you to run the same calculation on one computer or on many computers. But the thing is to get anything to run in Hadoop at all is a big deal.

**FRANK:&nbsp;** Yeah. Sorry, I'm trained as a science-y person not to make restrictive statements about other people's systems.

[Laughter]

**SAM:&nbsp;** We'll make them for you.

**FRANK:&nbsp;** Yeah. [Chuckles] So, absolutely. I think there's a huge cognitive overhead when you're taking the leap into one of these, some of the distributed systems where they ask you to write a second program and maybe write separate programs for each of the stages in Hadoop or something.

There was a cool project out of Microsoft Research that I was adjacent to. I wasn't directly involved in but it's this project called DryadLINQ which was really neat. And it took the LINQ programming idioms from C# and these are sort of collection-oriented SQL like statements where you could have a vector or something like that and you could say 'dot group by' and it would go and do some grouping stuff. Their interest was can we interact with databases a little bit better? But these DryadLINQ guys took LINQ queries and mapped them to these clustered backends. But the experience is still you're writing your C# program. You don't cognitively have to switch out at all. You're not even using a DSL. You're just using C#. And it had a great experience. Your programs, you could see the entire program logic in front of you. You didn't have to have a few different windows open and a few different programming languages and all sorts of weird stuff going on in your brain at the same time. And super pleasant to use. It was sort of, I've aspired to keep the look and feel, so much of that as possible.

Spark gives a similar look and feel. You don't have to dip in and out of Scala too often when you're writing Spark style programs. So, I think that's maybe a good example of how to keep your brain under control at least. And other people's brains. The real problem here is you can put this thing together but then when you go on holiday for a month someone else has to figure out why it doesn't work anymore. And if your entire office is covered in sticky notes explaining what the hell things actually do, it's horrible. There's lots of room to improve here, I think.

**JESSICA:&nbsp;** Yeah, agree. Because the complicated systems like Spark and Hadoop, they introduce so much overhead. And also you mentioned in some of your articles about the high-level languages, having more corner cases and it actually takes way more code to get something that's high-performance in a language even as good as C# compared to something lower-level like Rust?

**FRANK:&nbsp;** Yeah. So for example, the Spark folks have just announced Spark 2.0 which is [sort of] cool. And it sounds like they're reporting very good performance numbers there. Though at the same time, they've sort of rewritten the compiler on top of Spark. So, this is… they're now taking all of your Scala and Java fragments. They're doing a whole bunch of compiler style analysis on fusing [operators] together, doing code generation, things that you sort of thought the compiler was probably supposed to do. And they're probably getting help from the compiler. But this is five or six years after Spark originally came out. They're at this point now because it's a lot of work to fight against these systems that we're trying to keep you safely away from the low-levels. They're realizing they have to paddle upstream basically to regain that ground. And you can do it but it just takes a lot of time and a lot of work and it's sort of painful.

**JESSICA:&nbsp;** You mentioned earlier that if you can just write a 10-line for loop in a language like Rust on your laptop, that this is usually the fastest thing. If that works, it's going to be fast because there's no overhead. So, as we write these systems that are coordinating between processes and between machines and spreading the work out, are we aiming to compile them down to these 10-line for loops eventually?

**FRANK:&nbsp;** Yeah. The fastest thing out there is not the 10-line for loop thing. It's a 10-line for loop thing distributed across a bunch of computers where they just, data magically moves between the computers and everything goes real fast. But you are hoping. You're crossing your fingers and you're hoping real hard that when you write your program, whatever big data [sort of program] it is, the code that gets compiled looks a lot like the for loops. That's the sort of thing that you're hoping for. You really don't want to have to write the for loops yourself, because that's annoying especially because when it is multiple machines involved it's not just for loops. It's also some networking and some horrible stuff like that, that you'd prefer not to have to write manually each time. But you would really like, absolutely, to have the generated code be as close to that as possible.

And it's the sort of thing that Rust does a pretty good job at. This is my language of choice I guess. But they do a great job I think of giving you high-level idioms like iterators and closures and stuff like that but still compiling down to approximately what you would have written by hand if you had been given the choice. Possibly something better than what you would have written by hand if you're sort of lazy like I am.

**JESSICA:&nbsp;** I have a deviation. Let's see if this goes anywhere. You mentioned something about for loops unrolled earlier. Could you define that?

**FRANK:&nbsp;** Oh dear. I saw you ask about that and I realized that I had just sort of said something awkward at the time.

**JESSICA:&nbsp;** [Laughs]

**FRANK:&nbsp;** If you want to process a billion records, there are a few ways you could think to do that. You could try the laptop approach which is 'for i equals 1 up to a billion' or sorry, 'zero up to a billion' depending on what flavor of programmer you are. 'for i equals zero, let's say up to a billion, do something'. And as soon as you write that program you're in a little bit of trouble because you've written that program and you can't, no one can automatically look at that program and say, “Oh, I see. I see. I see. You said ‘for i equals one to a billion’ but I'm just going to break that into a thousand different pieces and put that on different computers and run it independently for you.” Because you might have changed the meaning of the program.

So, although it's very easy for the programmer to say, “Yeah, yeah. I'll just write a big for loop,” if you can trick them into explaining a bit more about their computation, if you can trick them for example into explaining each of those billion things that they're planning on doing, they don't have to happen one after the other. They could happen at the same time perhaps, if you can trick them into explaining that. And this is the sort of thing that these Hadoop and Spark and other higher level functional collection-oriented languages do. If you can get someone to write in a functional fold or map, that's great because then you know, I know the semantics of the program and I can make that happen in a lot of different ways. In particular you can go and shove it onto a lot of different machines and do stuff in parallel.

Now, if you make things complicated like folds and maps and stuff like that, the person who had their head wrapped around unrolled for loops is going to get a little antsy. Because they thought they knew how that worked. They drive their machine sort of one through a billion. They've got their head wrapped around that and now you're asking them to think a little bit harder and a little bit weirder. But you know, it's worth doing and it's worth trying to figure out how to trick people basically into revealing the actual structure of their program, if they can be so encouraged. This is what I had meant at the time about these unrolled for loops is that as soon as you unroll them, it's a little tricky to see that they could have been executed differently. They could have been distributed across lots of computers and run independently.

**JESSICA:&nbsp;** Oh. So, unrolled is like do things one at a time?

**FRANK:&nbsp;** Yeah. If you take… so, if you look at a piece of code that says 'for i equals zero up to a billion, do something' we still have a chance at this moment to try to lift that up and say, “Oh, that's just a billion totally independent bits of computation we can run. Cool.” But as soon as someone starts to, someone being the compiler, maybe the programmer starts to unroll that and say, “Do zero first, then do one, then do two, then do three,” at that point we have a very sequential program where if we want to really respect the programmer's wishes, well the other computers aren't super helpful anymore because they all have to wait for zero to finish and then for one to finish, and for two to finish, and so on. So, a lot of these…

**JESSICA:&nbsp;** So like, unrolled into a sequence of instructions.

**FRANK:&nbsp;** Yeah, or each of the steps unrolled one after the other. So, if you think of the for loop as that hunk of code's going to happen a billion times and if someone just copy-pasted it one after the other, they definitely done us a disservice in trying to help them make their code go faster. So you see it like yeah, in a lot of these systems you have these higher-level constructs, again things like fold and map. In Rust you have all these nice iterators which there's some cool work on concurrency in Rust where they'll automatically take your iterators and parallelize them if that's appropriate. Now, if that's appropriate is of course a little sticky but subject, but they're pretty good at figuring out when it's actually safe to do this.

**JESSICA:&nbsp;** Oh, because in Rust you have to declare whether you could possibly update a variable.

**FRANK:** There are several cool things about Rust. One of them is yeah, whether you could update a variable. There are others. Certain types are known to be transmittable between threads. So, there are certain types which you can't move between threads. Some of them you can move between threads. And it helps to clarify a lot the concurrency story, the data race safety which is something that Rust guarantees that you won't have, basically data races that is.

One of the things that Aaron Turon, one of the folks behind Rust, likes to say in a lot of his talks is that you have fearless concurrency. That you can write concurrent code without being scared. And it's surprising but it's pretty accurate actually. You write this code that you're like, “Oh wow. I'm feeling horrible things. I really am. I've got threads everywhere and shared data structures all over the place.” But the type system is actually preventing you from writing code that is ever going to mutate something without having acquired a lock if it has multiple people referencing it. And it will let you not bother to acquire locks if it can confirm that you're, the data is not actually shared with another thread for example. So, it's sort of neat that yeah, Rust gives you a lot of structure I guess about your program to let you understand when is it okay or not okay to play around with other bits of data that might be shared with other people. Where if those people see the data in an inconsistent state horrible, horrible things might happen. It will basically make sure that at least one class of things don't happen.

**SAM:&nbsp;** So, going back to something you said a little bit earlier, you were talking about starting out with a simple program that you run on your laptop maybe wanting to be able to scale that up. It sounds like one of the benefits of being able to scale up is machine performance, being able to get your answer in a reasonable amount of time. But the human cost of that of course is that in many cases, I have to go from something that I've written on my laptop in one language using one set of idioms to, I have to cross this sort of phase transition into a big data system and write my code in a way that this other system understands it. And it seems like it would be another nice advantage for me as a human being to be able to take that thing that I wrote and not throw away all that knowledge that I've accumulated in just playing with the data locally and to be able to take code in that same language and then just ship it out to multiple machines. Is that something that's going to be feasible? Like to what extent is that going to work?

**FRANK:&nbsp;** So, it's a good question. I think… let me sort of answer it partially.

**SAM:&nbsp;** Sure.

**FRANK:&nbsp;** I think partially the answer is yes, partially the answer is no. there's absolutely no reason you shouldn't expect in the glorious future be able to take hunks of code that you've written in pretty much any language and have them run hosted in very much any other programming language, little fragments. So, if you've written in Ruby some fun parsing [inaudible] manipulation stuff that gets the data into the structure that you're familiar with and you've written a bunch of [inaudible] functions associated with this particular structure, absolutely. You shouldn't have to or even want to throw those sorts of things away. There are a few stories with respect to foreign function. So, if you want to call into or out of C, you know how to do this, you may know how to do this sorry, with Ruby and such. And calling between various other programming languages is something that you'd like to support. Rust has a pretty good story here.

And there's actually, there's a cool link that let me throw at you guys, that is this project called Helix which is actually, it's meant to bridge Rust and Ruby in particular to allow you to automatically get the Ruby implementations written in something like Rust. Where hopefully yeah, you take a lot of the code that you put together in one language, you can reuse it in other settings. Now that being said, there are restrictions. There's not a little magic wand that will, you wave over your weird pile of spaghetti code that you might have and it makes it magically scalable or something like this. But if you do have your pieces of code compartmentalized so that this is the bit of code that gets called once on each record and we now want to map this across a billion records, that's the sort of thing you absolutely should be able to do for sure.

At the same time, there's definitely a little bit of some friction I guess if you've written things in a language that was maybe [inaudible] easy to use but a bit more casual in terms of its implementation. Running a billion copies of that… you know, it might scale in the sense that it will go faster the more machines you had. But it might also have gotten 10 or a hundred times faster if you had recompiled it down to one of the more performant languages. And actually, this Helix project, this is by skylight, they have a talk about it. And they were seeing 100x performance improvements in various little small components that they re-implemented essentially in Rust. Now, you like to keep the code as close as possible when you move between these two things so that you can take your ideas from one language to the other.

But at some point it's also worth thinking, “Should I maybe restructure, or not restructure so much as translate maybe the methods so that the new system can take full advantage of it?” But I think of course that's, I think you want to be able to do it incrementally. [Inaudible] works fine on your laptop at the moment. You want to try getting a second core involved for example. Hopefully that's easy and at some point if you need to bring in a hundred computers, maybe you put off the complicated porting until that point.

**JESSICA:&nbsp;** So, maybe translating into Rust and running it is something that you could experiment with in a few hours.

**FRANK:&nbsp;** Yeah. I think it's the sort of thing that, this is the ideal story. You're absolutely right, is if you can look at a big pile of code that you have, some components of which you think might be a bit slow and you can just try out. Let me take this method here which is a real time sink. Let me try to render this down to something that's meant to be a bit performant. Let me see how that works. Does it feel good? If it's a horrible, painful disaster and I only get a 2% performance bump, well nothing good has happened here. On the other hand, the intent of course right, is that you start doing this and like, “Well, that wasn't so bad at all. I'll do a little bit more of this. I'll do a little bit more.” And maybe then you have your higher-level language more as your orchestration language that thinks a little about which parts go where. And you have your more performant [inaudible] in a different language.

So, this is sort of a dichotomy that Ousterhout, John Ousterhout, proposed at one point which was there's room in the world approximately for two languages. A high level called scripting or orchestration language and a low-level C style surrogate for, “I really want the computer to do this specific thing right now.” And you put these two together and it's this… not that much room for other things. You can just go down to the metal when you really need it and otherwise stay in whatever is comfortable and productive. Ideally, yeah the boundary between the two is friendly and porous and you can move between them as appropriate. But it's still, it still remains to be seen which systems do that best. The Rust folks are definitely aware of this type of thing and working to make this pleasant. But hopefully so is every other language out there.

**JESSICA:&nbsp;** That's a good recommendation of no one high-level language and one high-performance language. I don't know a high-performance one yet. Oh, and JavaScript. Everybody needs JavaScript.

**FRANK:&nbsp;** [Chuckles]

**CHUCK:&nbsp;** [Laughs]

**SAM:&nbsp;** No!

**FRANK:&nbsp;** Yeah, I [inaudible] JavaScript. Ugh. That's too bad. [Chuckles]

**JESSICA:&nbsp;** [Laughs]

**FRANK:&nbsp;** I personally… so, I've obviously, you can tell with how my creds are but I absolutely recommend everyone, if you don't know a low-level language… sorry, low-level might be the wrong word you know, actually. But a high-performance language, check out Rust. I went into using it thinking I was pretty clever. And I definitely had a pretty good impression of myself.

[Chuckles]

**FRANK:&nbsp;** And I learned a lot from it. It teaches you a lot not just by making you suffer or anything like that. But really the…

**SAM:&nbsp;** Not [JavaScript].

[Laughter]

**FRANK:&nbsp;** Well, [inaudible], yeah. But it's like exercise, right? You struggle a bit and then you realize it's actually good for you. Not the struggle specifically but what it's taught you. And a lot of what Rust ends up teaching or taught me at least was you've organized your program badly. Maybe if you organize it a little bit better it will be clearer to me, Rust, why it's safe to run. And along the way I realized yeah, that's actually, that's a good point. And this is a much clearer organization now not only for the compiler but also for other humans who might want to read it. I don't know. I picked up a lot from learning Rust. And at the same time, you learn how to write programs that are pretty nice high-level that go magically fast, which just feels great. And I love it.

**JESSICA:&nbsp;** I found that same effect from writing functional programming with immutable data structures and data in/data out functions that it forces me to organize my code in a way that turned out to be clearer for reading it as well.

**FRANK:&nbsp;** Absolutely. It's the same sort of thing that you put a constraint on. It's a very helpful constraint from a sanity point of view, functional programming, that you should describe the outputs of your computation in terms of the inputs, not change the inputs but think about how to reconstruct them. And you get lots of really cool, magical things from that. You write stuff in functional languages that can automatically distribute the computation. It can automatically… crazy stuff like incrementalized re-computation so that as your inputs change, [inaudible] re-run the computation for you because you were so clear about how do I go from my input to my output without mucking up the input on the way? And again, programming with this sort of constraint, you learn quite a bit of, how can I make this program simpler and clearer? Maybe not the first way you would have thought to write it, but I don't know. I find that I write code a lot better now.

**JESSICA:&nbsp;** Awesome.

**CHUCK:&nbsp;** So that being said, I do want to ask a question here and that is generally, it's kind of a loaded question, but it sounds like functional programming does have a lot of things going for it in this particular area. So, are you causing yourself extra pain by using a language that's more object-oriented? Or are you… I guess another way of asking that is are you generally better of using a functional or procedural language?

**FRANK:&nbsp;** Yeah, good question and answer right there. [Chuckles] No yeah, it really does depend on what you need to do at some level. So, let me give an example. That's a brilliant segue, thank you. So a lot of the, for example a lot of the low-level stuff in the project I'm working on, this timely dataflow project, are written in Rust that's very much a procedural language. You can mutate things. There's some immutability in there. But absolutely, you can mutate things which is very helpful for me implementing things in a way that my brain works at least.

But you [pop up] a level, there's a layer that I've written on top of timely dataflow that follows some other work we've done at Microsoft, this layer called differential dataflow. Because you put dataflow at the end of everything and it sounds good. But it's a very functional programming language for people using it up top. It's this collection-oriented functional programming language that automatically does a lot of really cool things for you. The things actually I just sort of suggested [that], the automatic distribution, automatic incrementalization. So, if you can write your computations as a bunch of folds and maps and essentially fixed-point combinators over large collections of data, we can spill it out to lots of computers for you. We can automatically correct all of the computations when the inputs change. So, you get essentially real-time big data computation over these gigabytes of data. I want to say for free, but basically for free.

[Chuckles]

**FRANK:&nbsp;** You wrote your [program] in a very friendly way. You wrote it with very clear explanations about what needs to… well basically, with respect to how your output is defined in terms of your input. And that lets us go back and fix the output when the input changes, which is great. So you know, at that point it's great to be using a functional language at that high level because we can take advantages [of] these features. At the lower level or if I needed to have a conversation with the kernel about the status of the network, absolutely, I'm sure you can use functional languages for this. I don't want to say otherwise. I'm not a master of that at the moment though.

**JESSICA:&nbsp;** So, timely dataflow and on top of that differential dataflow. Is it a DSL in Rust?

**FRANK:&nbsp;** It's actually, it's just a library. So, way back when I was a much younger scientist we wrote a paper and we announced that what would get done was a new language. And we were proud and the reviews came back for out paper and said, “No, no. It's just a library.” And we were very depressed.

**CHUCK:&nbsp;** [Laughs]

**JESSICA:&nbsp;** Oh.

**FRANK:&nbsp;** But the more I think about it, the more I actually… the other way around I really like. I think if you take the exact same functionality and encapsulate it as a library and sort of as a DSL, even better. If people don't have to even switch idioms when they start using your library… so in timely dataflow you have these things that are streams. They support a lot of the same methods that iterators in Rust support. So, you have a parallel stream, basically distributed stream of data, and you can say map. You can say filter. You can say a bunch of these sorts of [inspect], things that people are used to saying. And yeah, it's got exactly the same look and feel. It's not a different language at all. But it just turns out that it's running on lots of computers when you do this. So, it's not, yeah, not even DSL. It's a library and it's meant to be… yeah, we can have a long discussion about is it successful enough, but meant to be pretty ergonomic. If you know how to write stuff in Rust you pretty quickly are up and writing stuff in timely dataflow.

The main idioms I guess you would say, there's channels basically, these channels between… for example you put data in, data comes out the other end, but because of the magic of distributed computing, sometimes you put data in and different data comes out because this different computer was involved. But that's okay. That's usually, in a lot of these programs, is totally fine. If you want to do a map you just pull the data out of whatever your source of data is. You apply your function to it. You push them into the next channel. It's not particularly weird that you only saw half the data instead of all of the data.

**JESSICA:&nbsp;** In this system you can ask it for the current value or the latest value of the data and then keep going and keep counting?

**FRANK:&nbsp;** So, what typically happens in these sorts of things, dataflow systems in particular, you don't usually have the opportunity to ask it, “Tell me what's happening right now.” You set up a computation, sort of in the same way you write a functional program. At the end of it you can see what the answer is. When you're finally done writing your program you can ask, “Okay, what actually happened?” And dataflow is pretty similar. You describe the computation and you wait to see what happens. You don't have as much imperative control because in particular other computers might be involved. You might say, “Ooh, I really want to see the answer right now for a thing.” But the correct answer actually requires hanging out for a moment until the computer next door finishes up whatever it's doing and hands you the result. So, the typical approach that you, you end up writing things which is a little bit more like, I don't want to say callbacks but basically callbacks.

[Chuckles]

**FRANK:&nbsp;** You write these closures that when the answers finally do arrive what should you do with them. And often, you put them in a channel and then you look at the channel later. But, sorry. Go ahead with your question.

**JESSICA:&nbsp;** When the answers finally arrive, including the intermediate answers? Like at the end of an epoch or something?

**FRANK:&nbsp;** Yeah, it depends how you set up your computation. At the timely dataflow level you're sending data around and you see what you see. You write these operators that get streams of records that come in and you get to act on them, update some state if you'd like, and then send some more records out the other end of the operator. And yeah, you see what you see. You wrote the code that produces it so you get to see exactly those sorts of things. In the differential layer higher up it works very hard to only show you the correct answer and to only show you differences in particular between the correct answer now and the correct answer just a moment ago. So, it doesn't want to distract you with transient things. It believes in, maybe wrongly, but it believes that's a feature. If you have your dataflow connected to the, “Should we fire the missiles?” button you don't want to necessarily get the answer that's “Oh yeah, yes. Oh no. yes. No.”

[Chuckles]

**FRANK:&nbsp;** And at the end you learn the answer was no. but in the meantime you've already made a few bad choices.

**JESSICA:&nbsp;** Darn side effects.

[Laughter]

**FRANK:&nbsp;** Yeah, right. So, it depends. You can write different code if you like, different lower-level timely dataflow code that absolutely reveals everything as it goes along. And we've chosen as we built the higher levels not to do that. But the option's [still] there if you'd like it to fix that.

**JESSICA:&nbsp;** I used the word epoch a minute ago and this is a concept that I found, well okay, I first found it in Naiad and timely dataflow in your work. So, one of the problems with this real-time data processing is, “What is done? Is there such a thing as done?” In Hadoop jobs, they're batched. There is done and then there's a 'data dump dot HDFS'. But when you're talking about what's going on as recently as we can really figure it out, there's not this idea of done. But timely dataflow has this concept of around or an epoch.

**FRANK:&nbsp;** Yeah. It's actually, it's the same concept that exists in a few of these other systems as well. So, it shows up in streaming platforms as you as get there because it's a pervasive question. And if you're constantly firing data at a computation what can you really say about the output? You'd like the output to tell you something like, “We have properly processed everything we've received in the past five minutes,” something like that. Or, “There's at most 10 seconds worth of outstanding records that we haven't processed.” You need something from the system to give you some clarity on the answers that you're getting. And there's a few different ways that you can do this. A lot of the systems use wall clock time. They'll tell you, you stamped each record with the wall clock as it arrived at the system. And on the other end of the system where the results are coming out they'll tell you we're now showing you the results live with respect to whatever time it was that they showed up. So, it might take about five or 10 seconds through the pipeline. You're seeing data that's now aggregate totals that are five or 10 seconds old coming out the other end.

And it's very… typically the systems, stream processing systems are very clear about this. They'll tell you, “This number corresponds to a little while ago.” And that's good. It's very good to be clear about these things. You don't want to… it's rare that you want to get inconsistent results out. There are situations where you might want that but it'd be a little weird if you're computing the average something or other and you're doing a much better job computing the denominator than you're computing the numerator. You're going to get consistently skewed statistics. Like if your count of the number of things you have gets updated super-fast but the sum of all of the features that you're trying to add up pretty slow, then you're always going to have a weirdly larger denominator than you have sum of features. And your averages are going to look consistently a bit lower than they should. Which would be disappointing. You'd really like to get the correct answer for some moment in time, even if that moment in time was a little further back and doesn't use everything that you're currently sitting on in terms of your input data.

So, what Naiad and timely dataflow do actually which is a bit different and maybe a bit cooler, cooler is too much but it's empowering, is they totally decouple the data plane and this control plane. So, they moved it around as fast as they possibly can. Data go everywhere, basically as fast as they can figure out how to get computers to move them around. And then we leave a little bit of communication, the sort of exhaust or backscatter from the data moving round that tells the system how far we actually made it in the computation. One of these timestamps that came in or these epochs, rounds of data coming in, how far have they actually gotten? Which of these do we still expect to see in our output? And this gives us a lot of power. It allows you to do a lot of out of order processing, if that makes sense. You can see earlier results back in a system, something like timely dataflow, if you write the code to do that of course.

And it's generally just really helpful. It gives you a lot more concurrency in your system. You keep things moving a lot faster if you break apart the movement of data and these notifications of progress essentially. How much of the data have we processed for sure, for a hundred percent guaranteed processing? Break those two apart, move the data as fast as you can, and just get notes basically telling you, “Oh now is the moment when we've actually finished with everything from five seconds ago.”

**JESSICA:&nbsp;** So, you can be explicit about the increments to divide messages and therefore computation in two and also about how there was something in the examples about you being able to specify that you can lump five of them together.

**FRANK:&nbsp;** Hmm, lumping five together. So, I think… let me describe a few alternate ways you could do things. One of them that people used to do which wasn't very good was they basically require, the data itself tells you how fast are we moving through the computation. It's like, “Don't tell anyone what the average is until we've actually computed the right average. And don't do any other work in particular until we've actually computed the right average.” And it's sort of, if you have one slow machine that blocks up the computation, everyone else is waiting on that person before they can do any more productive work. A different strategy is everyone keeps firing on all cylinders. They keep sending as much data as thy can as fast as they can. But if someone falls behind, a worker falls behind for some reason, you end up with a little bit of a tangle of information. Like, is this data that I'm currently getting from my numerator current with respect to this denominator? I don't know. It's all confusing.

And we think the right thing to do and other people do this so it's not a revolutionary thing is you send the data around as fast as possible but you annotate each piece of data very clearly with what logical moment in time does it correspond to. So, it lets you send the data out of order if you want because you left notes on the record saying, “Yeah, you might be getting this right now but actually it corresponds to something that you probably shouldn't be seeing for another few seconds.”

**SAM:&nbsp;** Sorry, is this something that people might now as a vector clock or is that something else?

**FRANK:&nbsp;** A vector clock is absolutely different, unfortunately.

**SAM:&nbsp;** Okay.

**FRANK:&nbsp;** No, it comes up a lot because syntactically they match really strongly. And vector clocks are more about if you have multiple different computing folks who have different clocks and you want to figure out how can they even sanely talk about some common notion of time, you can use the vector clock as a way for them to sanely talk about, “Could I possibly have influenced your data?” or so. In this world, we're stipulating by fiat that there's one global notion of time. It's this number that counts up. [Inaudible] it is. And for some other reason, for some reason, this person over on the side is a bit slower than we are. So, when they say that they're working on epoch 100 and we're on 105, they're just slow. Their 105 is going to be the same as our 105 in the future. We don't need to worry about whose vector clock is which or what [or] unifying the fact that their 105 could influence our 105, anything like that. We're going to let it play out as appropriate because we're trying to follow the intended semantics of the program.

**JESSICA:** But in the meantime if you're the average emitter, the average calculator, and you have the epoch 100 of how many dollars we've sold and the epoch 105 of how many transactions we've processed, then you could take the… you also have the 100 epoch of transaction we've processed and you can combine that with the 100 of how much money we've processed and output the average as of 100?

**FRANK:&nbsp;** Absolutely. So yeah, you have enough information on hand to get the correct answer for 100. As long as you left enough notes behind to remember that I had 100 at one point and 101, 102, 103 flew by. I shouldn't have erased 100. I should make sure to keep it there. But as soon as you get both the numerator and the denominator for epoch 100 you're ready to ship epoch 100 and proudly announce downstream, “We got the right answer. If anyone was waiting for me to be finished with epoch 100, we're good to go.” And you could also in principle tell people downstream about the total counts up to epoch 105 but they should be clear that maybe they shouldn't run with these numbers yet because they're not final. But you're welcome to show them to people.

And sometimes, there are good things that they can do. So, with these numerous numerators you can do lots of good pre-aggregation before it's time to process them. So, if we're trying to aggregate up, we're seeing all sorts of sales reports fly by, if we're seeing stuff at 104, 105 even though we're still blocked on time 100, we can still do this aggregation. We can count them still. We can count everything at 105 and just record that one number. We don't have to hold the data back and say, “Please don't show me this data. It's not time yet.” So, it's good to be able to process, be able to process things at least out of order because you could still do some meaningful stuff in the meantime, which fills up your time. It gives you something to do while you're waiting for the other folks and means that once they're ready to go you can respond that much faster.

**JESSICA:&nbsp;** So Frank, in the introduction to timely dataflow post, you mentioned that you're trying to prevent people from having to continually re-implement things from scratch in mutually incompatible frameworks, these things being like [inaudible] coordination between processes and probably the, correct me if I'm wrong here, the effectively compilation of declarative computation steps into efficient code. But you also…

**FRANK:&nbsp;** Everything, actually. Yeah. I mean, more than that even. The people who write their distributed systems from scratch have to write their networking [inaudible] deserialization. They've got to write all sorts of stuff typically from scratch. And it felt a little silly to have them redo that over and over again. And they should just all team up and build one version that does a really good job, was my [inaudible].

**JESSICA:&nbsp;** That would make our lives easier, especially when we have to pick one. But then you said many of the people re-implementing those have strong incentives to do so. What are those?

**FRANK:&nbsp;** That's me being cheeky. [Chuckles] So, it's very possible, from a research point of view it's very possible that the same thing will happen with timely dataflow that happened with the previous project I worked on the privacy space which factored out a lot of really cool ideas into a common reusable substrate. And unfortunately in the research space, you don't get points for having a 10-line implementation using someone else's platform. You get points for building a new platform from scratch and announcing that you're a super powerful system builder. So, although it might be 10 lines of code to run [inaudible] on something like timely dataflow, if you want to write a paper and get your PhD and stuff like that, you're not going to get it by writing 10 lines of code. You're going to get it by building another system from scratch.

So a lot of, to be fair a lot of what people are doing in the research space for sure is learning. They're building these things so that they can learn. And that's cool. People obviously should keep learning. But it's not clear if your goal is learning fundamentally that you should, that you're going to get as much learning done by pulling down a library and just getting something that works really fast. Yeah.

**JESSICA:&nbsp;** On the other hand in industry, we totally get credit for writing 10 lines of code that does a ton of stuff using some library that we downloaded from the internet.

[Laughter]

**SAM:&nbsp;** Or better yet deleting 20 lines of code that somebody else wrote.

**JESSICA:** [Laughs]

**CHUCK:&nbsp;** Yeah.

**FRANK:&nbsp;** That comment was definitely sort of a slightly snarky comment about what we're pushing back [inaudible]. Absolutely, it's great when people tell us, “This is wonderful. I can do my graph processing at the same time as I can do my SQL processing and I don't have to have two systems. Thank you so much,” which is great. And then the next paper someone writes ignores that that's possible and builds another thing from scratch. And you're a little sad and depressed but, well you get over it.

**JESSICA:&nbsp;** Yeah, what we want is one system that does it and does it beautifully and does it really well. Unfortunately one dissertation and one research paper doesn't get it to beautiful.

**FRANK:&nbsp;** No. And that's actually another… a very good [inaudible] point that a lot of the systems that people build certainly, my background is in research and most of these comments are about research. But the system goes far enough that you can write a paper which usually means writing something that runs with the graduate student holding its hand as the system runs along to the measurements that you want.

[Laughter]

**SAM:&nbsp;** Yup.

**FRANK:&nbsp;** Which is cool, if that's what you want to do. Cool, but you go and you try to grab the code that people put out there. Sometimes, it just doesn't work. And that's too bad. Again, it's hard to see what the incentives are here because if you ask the student, “Why aren't you responding to my bug reports?” and the student's [inaudible] graduate, “I don't get paid to fix code. I get paid to get out of here,” pretty much. And some of the incentives are not brilliantly aligned to putting out industrial-grade code, which is too bad. It'd be cool to figure out how to do that. But it's always been a tricky question. How do you take fun research that is interesting and neat and turn it into a reliable, supportable product that doesn't break every five minutes?

**JESSICA:&nbsp;** Which is probably at least 10 times as much work as the original creation of it. Maybe a thousand.

**SAM:&nbsp;** Right. Maybe, my guess would be that it's the approach is wait 10 years and hope.

[Chuckles]

**FRANK:&nbsp;** It's not the sort of thing that's I think magically going to happen anytime soon. I'm happily in a position where I can do some of this myself. I'm definitely not an industrial-grade programmer. But I've been having a lot of fun. I actually try and deal with some of these issues of does the code continue to work in lots of cases? Is it nicely documented? Does it not explode? Rust is pretty good at making code that doesn't explode, so that makes my life a lot simpler. But no, it raises a lot of really interesting questions of maybe the most exotic solution is not the best solution. Maybe trading in a bit of the exotic performance for simplicity so that people can actually understand if it doesn't work, what should I do? How can I fix it? Can I do anything other than call up the grad student who wrote it?

**JESSICA:&nbsp;** Yeah, and at work it's, “Oh, I hit a problem in the system. I found a workaround. Maybe it was out deployment system.” And if I can encode my workaround into that system then it helps everybody after me. And fortunately we have a culture that promotes that, which is yeah, harder to achieve in research.

**FRANK:&nbsp;** Yeah, they're different worlds. It's cool when they can work together and I think it's the sort of thing that everyone gets smarter when they collaborate. The industry side you have [inaudible] but papers we love and stuff like that that gets some of the research ideas out there. And taking researchers and shoving them into industrial environments so they can actually learn about what the real problems are is I think super healthy. Occasionally it's a little frustrating because people don't get to shine. But the skills that they've really been developing we get to learn a bit and refocus you attention on maybe, I don't want to say what matters more, but what matters to other people.

**JESSICA:&nbsp;** Sweet. I think that's a good point for picks.

**CHUCK:&nbsp;** Yeah.

**JESSICA:&nbsp;** I bet we'll have some papers.

**CHUCK:&nbsp;** Papers. Alright, Sam what are your picks?

**SAM:&nbsp;** Well, if you were hoping for a paper I'm going to disappoint you. This pick is for those of you with urban commutes that might involve maybe a mile or two of walking. I have a kick scooter by a company called Go-Ped. And they make these super obnoxious gas-powered scooters that you can hear from half a mile away.

[Chuckles]

**SAM:&nbsp;** But the cool thing is they also sell an un-powered version. They call it the Know Ped. I'll put a link in the show notes. This is one of those kick scooters. You have to push with your feet. And these are fairly spendy. I also have a Razor A5 and I think you can get three or four of those for the same price as one of the Know Ped. But the Razor has these skinny plastic wheels that will dump you on your face if there's even the tracest amount of moisture on the ground. Whereas the Know Ped has solid rubber wheels which they have much better traction and a slight cushioning effect. Trades off a little bit of speed but it's pretty nice. Anyway, a couple of years ago when I was working in downtown Portland I would drop my daughter off at daycare and park the car near the daycare. And then I would scoot the mile and a half to my office, rain or shine. And I would ride through five or six-inch puddles in the dark and it would just keep right on going. This thing is bomb-proof. And it's a pretty nice way to extend your commute in ways that you might not want to if you were strictly on foot. So, I'll put a link in the show notes and that's my pick.

**CHUCK:&nbsp;** Alright. Jessica, what are your picks?

**JESSICA:&nbsp;** Alright. Well, the most recent paper that I enjoyed or let's say got something out of other than Frank's post which we read before this talk was…

**FRANK:&nbsp;** Thank you.

**JESSICA:&nbsp;** Oh yeah, I love the tone in your posts by the way.

**SAM:&nbsp;** Oh, I had so much fun with that, yeah.

**JESSICA:&nbsp;** Yeah. It's really friendly. It's got all the research and none of the stuffiness.

**FRANK:&nbsp;** This is good. This is one of the advantages of not being employed is that there's no one who would otherwise are paying you to disappoint.

**CHUCK:&nbsp;** [Chuckles]

**JESSICA:&nbsp;** Yes. We all benefit from you not getting paid somehow.

**SAM:&nbsp;** Mm.

[Laughter]

**JESSICA:&nbsp;** It is. You have the freedom to do these things that make other people happy. So, thank you for that.

**FRANK:&nbsp;** It's super fun, actually. I recommend, and this isn't really a pick but I recommend everyone get laid off at some point.

**JESSICA:&nbsp;** [Laughs]

**CHUCK:&nbsp;** Mm.

**SAM:** I've tried that a few times.

[Laughter]

**FRANK:&nbsp;** If you can afford it. But it really makes you rethink and refocus a little bit on what do you really care about? What's important to you? That's not a pick. But everyone should at some point. Yeah, totally get fired.

[Laughter]

**JESSICA:&nbsp;** Also beats the heck out of being one of the people left after a round of lay-offs. That's no fun.

**FRANK:&nbsp;** Boo for you. Yeah no, they got rid of our whole lab all at once. So, that was pretty clear. We all went and had drinks. It was good.

**JESSICA:&nbsp;** Mm. I was going to pick a paper which is the '2015 State of the Software Supply Chain Report' from Sonatype. And this is mostly, it's a white paper. And it's mostly terrifying. It's about how many people download things from Maven Central that are old and have security vulnerabilities and they still download them a hundred times a day in a hundred different versions across their company. This is to say, “Oh my gosh, the state of dependency management in our industry,” which I mean, this is what we do in industry. We download things from the internet. We write 10 lines of code to glue them in. It's a little scary. I hope, when I find a solution to it I'll totally pick it. But in the meantime…

**CHUCK:&nbsp;** The solution is npm.

**JESSICA:&nbsp;** Oh god. No. Don't get me started.

**CHUCK:** [Laughs]

**JESSICA:&nbsp;** Don't get me started. [Laughs] Right, so that's my paper pick.

In books I've been reading 'The Screwtape Letters' by C.S. Lewis lately. And that is an interesting study in human psychology. And also in the English language. So, those are my picks.

**CHUCK:&nbsp;** Yeah, terrific book. Awesome. I've got a couple of picks here. The first one is 'Start with Why' by Simon Sinek. Been reading that and it's really making me think which is really awesome. Just really, really enjoyed that.

The other one I'm not sure if I picked it before or not is the Cube projector. It's a couple of inches square. It fits in my bag and it's a projector [laughs] that can hook up via HDMI to my laptop or whatever. So, I may have picked that last week. But yeah, that's what I've been playing with lately.

Frank, what are your picks?

**FRANK:&nbsp;** I've got a few. I wasn't entirely sure what to go with so I sort of spread things out a little bit here. I was really pleased with the book that I'm reading right now but literally have not quite finished yet. So, unless something absolutely horrible happens in the last few pages, I strongly recommend 'The Night Circus' which I think other people have definitely read and reported good things about. I'm only now discovering that I should have read this five years ago, maybe. So yeah, 'The Night Circus', absolutely wonderful book. Sort of in the Neil Gaiman fantastical style which I really like. And actually yeah, if people come up with other ones like that, let me know, because I'm looking for that.

I have also, this is a bit of a weird recommendation but I've been traveling for the past year and I don't know, three months or so. And one of the things that happens when you travel a bit is you realize that for that sort of [inaudible] is you can tell the difference between which clothes are good and which clothes are bad. And I absolutely have to recommend the trousers that I have now. So, I have these really nice trousers by PrAna, these Stretch Zion trousers that I originally got for rock climbing. But they've just stuck with me for a long time. I've gotten some more of them now and they're nice and classy-looking on the one hand. But on the other hand, you scramble over all sorts of horrible rocks and they, whatever dirtiness just gets washed off of them real quick. And absolutely delighted and recommend those unequivocally. Yeah.

Everyone should go and learn Rust, too. That's [www.RustLang.org](https://www.RustLang.org/). You all should do that because it's amazing. And I think that's what I've got though. I can tell you about papers that are awesome, but…

**JESSICA:&nbsp;** Can we have just one paper?

**FRANK:&nbsp;** Oh, just one paper. That's awesome.

**CHUCK:&nbsp;** [Laughs]

**JESSICA:&nbsp;** Not like the most awesome paper. Just one that's awesome.

**FRANK:&nbsp;** Okay. So, let's see. One that I've been reading a bit recently is a paper out of UCLA that's going to be showing up at SIGMOD in 2016 that is one of the first papers as far as I can tell to look into doing things like [inaudible] Datalog. It's this programming language that is like a recursive version of SQL. And so, SQL with some loops and stuff. Doing that on Spark. Let me get the actual citation for you. This is a group at, a UCLA [inaudible] group and the paper is 'Big Data Analytics with Datalog queries on Spark'. And I'll throw a link [inaudible].

**CHUCK:&nbsp;** Very cool. If people want to follow up with you, see what you're working on these days, that kind of stuff, where should they go?

**FRANK:&nbsp;** So, probably the best thing to do is if you type in [www.FrankMcSherry.org](https://www.FrankMcSherry.org/) I think I've rigged that so that it properly resolves to GitHub basically, which is where I dump all of the content that I can think of. I've been doing mostly, I call it sort of pro bono science, like research out in the open. So, anything that I think of or start working on I just put out there. There's a blog there which embarrassingly is just a list of markdown files, sort of chronologically, where you can read a whole bunch of sassy stuff about what I'm doing at the moment or thinking about. There is Twitter where if you tweet some things at me I'll probably tweet something back because that's the sort of person I am. But I think checking out what I do on GitHub is probably the right way to see what I'm actually up to.

**CHUCK:&nbsp;** Awesome. Alright.

**JESSICA:&nbsp;** Thank you.

**CHUCK:&nbsp;** Well, we'll go ahead and wrap the show up. Thank you for coming, Frank.

**FRANK:&nbsp;** Oh no, thank you so much for having me. This is great fun. Talking is wonderful.

**CHUCK:&nbsp;** Alright. Well, we'll catch everyone next week.

**_[Bandwidth for this segment is provided by CacheFly, the world's fastest CDN. Deliver your content fast with CacheFly. Visit C-A-C-H-E-F-L-Y dot com to learn more.]_**

**_[Would you like to join a conversation with the Rogues and their guests? Want to support the show? We have a forum that allows you to join the conversation and support the show at the same time. You can sign up at RubyRogues.com/Parley.]_**
