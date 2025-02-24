---
title: "uv: An extremely Fast Python Package Manager :: Jane Street"
source: "https://www.janestreet.com/tech-talks/uv-an-extremely-fast-python-package-manager/"
author:
published:
created: 2025-02-20
description: "Jane Street is a quantitative trading firm and liquidity provider with a unique focus on technology and collaborative problem solving."
tags:
  - "clippings"
---
![](https://youtu.be/gSKTfG1GXYQ)
##### Transcript

Hi everyone. [[Charlie Marsh]] is the founder of Astral, a company building high performance developer tools for the Python ecosystem. Over the past two years, he’s released Ruff, a Python lintern auto formatter, and UV, a Python package and project manager. Both projects have grown to tens of millions of downloads per month, and have seen rapid adoption across both open-source and enterprise.

Okay, everyone can hear me? Okay, great, excellent. Wow, very nice intro. Now, what am I gonna do with my own intro slides?

Yeah, my name is Charlie, I’m the founder of Astral. Yeah, so I, me and my team, we spend our time trying to build really fast Python tooling in Rust.

We’re primarily known for two tools, right? The first of which is Ruff, which is a linter, formatter, and code transformation tool. So you can use it to format your code, but also to identify issues like unused imports and fix ‘em automatically.

And the second, which is gonna be the focus of what I’m talking about today, is UV, which is our Python package manager. I gave a talk at PyCon about Ruff, and it sort of covered what Ruff is, a little bit of how it works, and then what makes it fast. This is gonna be similar, but focused on UV.

So I wanna talk through what UV is. I’ll try to keep that short, because it’s maybe the least interesting part. Why we built it, some of the hard problems that went into building it. And with a couple examples or sort of case studies of things we did that make it really fast, because that’s the thing that we tend to get the most questions about, is, why is it fast?

So UV is what I would call a fast all-in-one Python package manager. So you can use UV to install Python itself, create virtual environments, resolve dependencies, install packages of course, it is package manager. You can use it to build your own Python packages that you would then upload and redistribute.

So UV is, if you’re familiar with the Python ecosystem, you could think it as a drop-in alternative to tools like pip, pipx, plinth, virtualnv, poetry. And it’s not a replacement for any one of these, it’s really intended to be a replacement for all of them.

So we model what we’re trying to do with UV after Cargo. So if you’ve worked in the Rust ecosystem, the tooling is very streamlined and very unified. And the way I would describe it is, I feel like Rust tooling… Oh no. Okay. Hold on. Okay, the way I think of it is that Rust tooling is very high confidence. When I clone a Rust project, I’m very confident that I can run it. It will run successfully and I know how to run it. And we’re trying to get to a similar experience with UV for Python tooling.

So UV is this single static binary that ideally gives you everything you need to be productive with Python. You install UV and then everything is sort of taken care of for you. So UV does a lot of stuff, and it does it all while being just way, way faster than a lot of the other tools in the ecosystem.

And when we started, I knew when we started working on a package manager, and this was some of the reaction. That it would be a little bit of this, because in the Python ecosystem there’s just a lot of different tools for packaging. And so when you come out and say, “Hey, we finally built a Python package manager,” there’s a lot of, well this cartoon.

And we still see a little bit of this actually, which is kind of funny to me because the tool’s pretty popular. But I think UV is actually pretty different from a lot of the other things that exist in the ecosystem in the previous attempts to build this tool for Python, primarily for two reasons.

One is just the scope of what we’re trying to do. So I mentioned this before, or hinted at it least. Python tooling is very fragmented, and I think of that in two ways. One is, for anything you wanna do, there’s a bunch of different options, and it’s very hard to choose and know which one you should use. And the second dimension is, for anything that you’re trying to do that’s non-trivial, you have to chain together a bunch of tools.

And for UV, it’s meant to be a totally unified stack. So we didn’t build on top of anything else, right? We didn’t build on top of pip or inherit any of the baggage that comes from existing Python tooling. We built everything from scratch. And that creates a really powerful model both in terms of the user experience we can deliver, but also how good it can be, I guess internally.

The second reason, I think that it’s a little bit different is just the performance, right? UV, as I mentioned, it’s very, very fast. And the thing that I’ve seen in my time working on this stuff is that when things are way, way faster, they really change the user’s relationship to the tool, and even the way that they work with it.

So we saw this in Ruff, where jobs that people used to only be able to run in CI, they could now make pre-commit hooks, because the speed differences were just so different. And so suddenly this thing that you dread running is something that you can just do locally and get in pass.

And with UV, another analogy would be virtual environments. In Python often, you have a virtual environment on your machine. It’s in a certain state, and you really don’t wanna mess it up because you won’t be able to recreate it and get it into that place. Or it’s really expensive to recreate ‘cause it has all these packages installed. But with UV, destroying and creating a virtual environment is extremely fast. We try to view them as totally ephemeral. You can just destroy them and recreate them because it’s so cheap.

So we’re actually trying to change. There’s a lot of obvious nice things that come with being much faster, but I also think that it can just change a lot of the workflows around how people work with Python.

So over, yeah, over we released UV in mid-February. And since then, yeah it’s just grown a lot. So it’s at 16 million downloads a month. It’s now more than 10% of the requests to PyPI come from people running UV. Which is kind of crazy. I would’ve been happy maybe with 1%. Just because the sheer volume of what people are doing with Python is pretty wild.

So that’s been a cool thing to see. Yeah, we have a lot of stars, we have contributors, blah blah blah. But the point is, we built this thing, I consider it fairly well battle tested. It’s been used across the industry, so hopefully the stuff I say has some credibility behind it.

All right, so the main job, right, or the main thing you do with a package manager is you install packages. So I just wanna talk through the life cycle of what happens when you run a command to install packages with UV.

And UV has two primary interfaces that you can use to engage with it. The first is that we have a pip compatible interface. So if you’ve run pip install, you can just run UV pip install and we implement a lot of the same commands that pip would. Which is great for people who wanna adopt it without changing their workflow, although we would like their workflow to change obviously.

And the second is, we have these higher level commands like UV sync and UV lock, that you sort of declare your dependencies, and then we just take care of everything and make sure the environment is in the right state whenever you wanna do anything. But they both operate under a fairly similar lifecycle, right?

So the first thing we have to do is we have to find the user’s Python interpreter. UV does not depend on Python, but we do need a Python interpreter in order to do a lot of useful things. So if you wanna create a virtual environment, for example, a virtual environment has to sim link in a Python interpreter. We can create a virtual environment, but we wouldn’t have a Python to put in it. And we need to know things like, what version of Python are you running, what platform are you on? All that kind of stuff. So this is actually pretty hard, but really not very interesting.

The next thing we need to do right is we need to discover the actual user requirements. This is the user telling us the state they want to be in at the end of the command. And that could be, they gave it to us directly, maybe we read it from a requirements TXT file, something similar.

Given those requirements, we resolve them into, this is the core job of a package manager. You give us some requirements, and we try and figure out a set of versions that satisfy those requirements. So the user might say, “I want Pydantic.” And that’s not really enough information on its own, right, for us to. What does it mean for the user to want Pydantic?

So the first thing we have to do is we have to resolve that into a set of versions, such that everyone’s dependencies are satisfied and all the versions are compatible. And ideally it’s the latest version of Pydantic too, because that’s what the user asked for.

So even this isn’t quite enough information for us to really do anything. ‘Cause this just describes the packages and the versions, but it doesn’t really tell us anything about where to get them. So ultimately this is not what we’re trying to produce, we’re trying to produce something that looks more like this.

So UV ultimately will create a lock file, and that lock file represents a resolution. And in that lock file we have information, like this is one entry from a lock file. So we have the package name, the version, but we also have information about where it came from. Also the packages it depends on, we have a sha, we have file size, et cetera, et cetera.

So ultimately when we resolve, we’re trying to create something like this. And I’ll talk more about how this is structured in a bit. Once we have that graph, we come up with a term I made up, like install plan. The idea is, we know the state that the user wants to get to, which is represented by the lock file. We have to look at the current state of the user’s machine, maybe they have an old version of Pydantic installed. So we need to uninstall it and then install the newer version of Pydantic.

So most of the, well not all, but most of the interesting work happens in here, in the actual resolver. And this was also, I think the hardest part of building UV. So I wanna talk about a couple of the hard problems that are maybe non-obvious, especially if you don’t spend a lot of time thinking about Python packaging, which I hope most of you don’t.

Okay, so the first thing that makes this problem quite hard is that Python has no multi version support. So you cannot have two versions of the same package installed at the same time. This might sound like a very obvious, so you can’t have Pydantic version one and Pydantic version two installed at the same time. This might sound obvious, but actually a lot of languages do support this.

So Rust and Node will let you do this without any issues. In Python, it’s basically a limitation of the runtime. Imports are a global cache keyed by module names, so you can’t have multiple modules with the same name.

So there’s a concrete example, let’s say the root is our project and we depend on a specific version of VLLM, and we also depend on a specific version of lang chain. And VLLM depends on Pydantic two, but this old old version of lang chain does not work with Pydantic two, it requires Pydantic version one.

So this is not a solvable graph in Python. You cannot satisfy these dependencies. And if you try to give this to UV, you’ll get this pretty error message that tells you this doesn’t work because you have these two dependencies, and they have an incompatible Pydantic requirement.

So instead imagine that the user says, “I’ll accept any version of VLLM, but I still need this old version of Pydantic.” In that case, what we need to do, right, is we need to backtrack and we need to test out all the versions of VLLM, and try to find a version of VLLM that does work.

So eventually we go and find, the previous version was VLLM 0.6.1, I think. So we tried out a bunch of versions. Eventually we find a set of compatible requirements. When we do the solve, right, it’s typically not just these four packages. This is just a snapshot of ultimately the resolved graph from those set of dependencies, right? It’s typically a sprawling thing with lots of different requirements, and there’s lots of different ways to satisfy it.

And ultimately, I mean the shape of this problem might look familiar to some of you, we’re trying to do version solving. So given we have a universe of packaged versions. They have constraints, like some things depend on different versions of Pydantic. We need to find the set such that all the dependencies are satisfied, we can only have one version of every package, and also we don’t wanna have extraneous packages.

And this, yeah, this is a Boolean satisfiability problem. It is NP-hard. So I like to think that as quite hard. And I’m not gonna go into the details of exactly what our solver looks like, but if you, maybe if you think back to school, we use a SAT solver, it’s based on CDCL, which is conflict driven clause learning.

It’s basically just a fancy thing that tries to solve those graphs in as efficient a way as it can by exploiting heuristics and things that it can learn. It can be exponential, there’s no guarantee that it’s actually gonna solve it in a reasonable amount of time.

So because we don’t have multi version support, we have to do the SAT solve. If we had multi version support by the way, we wouldn’t necessarily have to do that. Cargo’s solver, it’s not a SAT solver. It does a graft reversal, but if you get to a hard place, where things are not quite working, you can kinda just bail out and say, “Let’s add two versions of this package.” So that escape valve exists, but it does not exist in Python. And this is also true of other languages.

Okay, second thing. And I’ve never tried to explain this. This is all new material, by the way. This in particular, I’ve never tried to explain to a group of people so I might, let me know afterwards if it makes any sense. But this was surprisingly, or parts of this were surprising, but this was maybe the hardest part of building this resolver.

Which is Python has this very rich syntax for declaring requirements that should only be installed on certain Python versions or only on certain platforms, et cetera, et cetera. So just as an example, these are dependencies of a real package. I can’t remember what, maybe Flask. And you see the last one has, the import lid package should only be installed if the user’s Python version is 3.10 or earlier.

And if we look at some of the transitive dependencies here, Click itself depends on Colorama, but only on Windows. And it also depends on import lid, but only if the Python version is less than 3.8.

So when you see this set of requirements, there’s kind of two ways to think about solving the graph. One is solving the graph for a specific user, a specific point in time, it’s on a specific computer. Right, so maybe a user comes up and they’re using Windows on Python 3.12. So some things here are relevant and some things aren’t. That’s actually pretty easy because you’re basically just filtering things out while you solve, it’s not a huge problem.

But we wanna solve a slightly different problem, which is we want to generate a lock file that any user on any machine can then use to get a reproducible install. And what that means is, if a user is on Windows and a user’s on Mac, they may not get the exact same set of packages. The user on Windows would get Colorama, the user on Mac would not. But all the users on Windows on the same Python version should get the same set of packages.

And ideally, the differences between those users are as small as possible. That’s not actually something we guarantee, but the gist of it is you wanna be able to take the lock file. And any user on any machine should be able to take it and install. We don’t just want a lock file for Windows 3.12, we want what we would call a universal lock file. And that problem is a lot harder.

So again, the core of our solver is the SAT solver, and then there are kind of two pieces that go into trying to build this universal resolution. So one is that at a high level we kind of try to find a solution that works on all platforms. Effectively we assume that all of those markers are true, and try to see if we can find a solution. So the marker that said Colorama only on Windows, we would basically say let’s just assume that’s true and see if we can find a solution. And then afterwards we’ll filter out the packages that are only for Windows.

So that’s good, but the problem is, right, you can have these conflicting dependencies. So this is totally valid. You could have a user say it has to be Pydantic 2 on Windows, but it cannot be Pydantic 2 on all other platforms. And again, we’re trying to find a solution such that a user shows up and they’re on Windows, they install, they get Pydantic version two. A user shows up in their Mac, they get Pydantic version less than two.

Okay, so the way that we solve this is we, and again we’ve made up all this terminology because I don’t really know if there was good terminology for it that existed. But what we do is we basically try and fork and solve the two graphs separately. So in this case, on the left we would try to solve Pydantic greater than two. Assume we’re on Windows basically, and just solve the rest of the graph. On the right we would do the same thing. The graph ends up being a lot simpler, but we would solve these two graphs effectively independently.

And then we merge the results back together. So this is the merged resolution of taking those two. And oh wow, great. Oh, it’s all. Okay, I messed up the transitions on this slide, but I think we’ll be okay. Okay, this is what this is supposed to look like.

So basically, right, the thing on the bottom right is the merged resolution, and on the two sides we have the platform specific resolutions. So annotated types needs to be included, but only on Windows because it was only present in the Windows resolution. I think this is gonna do it on all of these, okay.

Pydantic is included twice, right? But once for Windows and once for non Windows. And those markers are disjoint, there’s no overlap on them. So everyone will get one version of Pydantic, but it will be one of these two.

And then importantly there’s also a package that’s included in both resolutions. So typing extensions is included both on Windows and on not Windows. Sorry, I know this is super annoying. So if you look at the way that that marker gets constructed, we have typing extensions and we’re saying we wanna include it on Windows or, but also include it on not Windows, right?

And that marker, these come from these two different places. And that marker is always true, right? So we can actually just ignore it completely. That’s why it’s not present in the final resolution. So not only do we have to solve these graphs in this way, but we end up doing a lot of different, this whole marker algebra that we have to consider.

The ors and the ands that you’re seeing there, we have to do a lot of operations. Like here, evaluating that that marker always, or figuring out that that marker always evaluates the true and that we can just omit it. I mean, it’s easy in that case, but we’ll see some hard cases.

Similarly, we have to be able to test for disjointedness with these. I mentioned that we had the two Pydantic requirements and they were disjoint. That just means that they can never both be true effectively. So for example, maybe we’re doing the solve on the left side of the previous slide, we’re solving for Windows and then we see a dependency that has this marker on it.

We wanna know, is this dependency relevant? We know we’re solving for Windows, so should we even care about this dependency because it’s only applicable on these platforms, right? And that question is basically, can they both be true? Are they disjoint? This is also a Boolean satisfiability problem.

And the markers can be pretty complicated, right? This is also NP-hard, totally separate NP-hard problem, which is we have to be able to test whether these two Boolean expressions are disjoint. And we’re doing this all the time.

Now, most markers are pretty simple, which is great, but these are just some examples of, these are the fully simplified markers for a real example from our test case. This is resolving if any of you use transformers, the Huggingface Project. One of our test cases is we take that project and we enable all of the optional dependencies, which no one should do, but it creates a very, very large graph. And so it’s one of our harder test cases.

And these are the fully simplified markers, and you can see some of them are pretty large. And by the way, before we did this, before we did this marker simplification of trying to get to these simplifies normalized forms, we would do that resolution, and each dependency would have tens of kilobytes of markers. The marker expressions were huge.

We even had some very basic heuristics, just kind of simple stuff for trying to normalize and filter them out. Ultimately someone on the team wrote this marker normalizer based on a technique called algebraic decision diagrams. It’s a totally separate solver that we had to build to try and normalize those markers and asked questions like, are they disjoint?

So these were both very, very hard problems. A third that I’ll just mention briefly is that, I’m not actually gonna talk about this one that much, but I do like to complain about it a little bit. So in the Python ecosystem, there’s really no guarantee that you have static metadata for a package or a dependency you wanna resolve.

And by that I mean, if we’re trying to resolve Pydantic version two, we’re gonna go to the registry and we’re gonna say, “What’s the metadata for Pydantic version two?” And it’s actually not guaranteed that they will be able to give us an answer.

Ultimately what might happen is we might have to run some sort of arbitrary Python code in order to get the dependencies. Basically if they publish a built distribution, it’ll have dependencies. But if they only publish the source for the package, we might have to effectively pull that down and run, if you’ve ever seen a setup .py file before, we have to run a setup .py file. We might have to build the whole package even, just to get the dependencies.

So we do a lot of things to try and avoid doing that, while still being correct. And I’ll talk about some of those in a bit. But kind of just concluding on this section. Ultimately what we’re trying to build here, we model it as a graph, right? The nodes are package specific versions, and the edges are weighted by markers.

So in this case we have the two versions of Pydantic, but one edge is weighted by only being on Windows, the other is never being on Windows. And you can see they share some common nodes, et cetera, et cetera. And the nice thing about this representation is, when a user comes along and wants to install on Linux or whatever, we just are traversing, we’re just doing a direct graph traversal and saying which edges are relevant and which are not.

So there are some tools in the pipeline ecosystem that try to do this, but they then have to do a separate SAT solve at install time. So they have a set of packages, and then when you install they actually have to run a SAT solver to figure out the right versions.

We have the nice property that it’s just, there’s no second resolution when you install. We’re just traversing this graph and figuring out the things to include. So this is the ultimate goal, all that work goes into trying to produce this thing.

Okay, so I talked a lot about some of the hard problems we had to solve to build this. Now, I wanna talk a little bit about things we did to make it fast. And the first thing that comes to everyone’s mind and also that I just talk about a lot is Rust. Rust is a big part of of UV and of how we’ve made it so fast. UV is written in Rust.

Like I said, we don’t have a dependency on Python, although you do need to have Python installed. But the observation for me, this slide is sort of just opinions. UV has gotten faster and faster over time, right? Despite being written in Rust the whole time. So it’s not just about being written in Rust.

From my perspective, I think Rust gives you a really fast baseline, and then it gives you a lot of tools that you need if you wanna write really, really fast programs. And other programming languages can expose these too. But for example, it’s pretty hard to care deeply about memory allocation if you’re writing Python. You just don’t really have a lot of control over what’s happening.

Whereas in Rust, you’re actually forced to care about a lot of those things, right? Which some people will complain about. It is ultimately one of the strengths of the language. So Rust is part of it, and I’m gonna talk about some parts of Rust that we use. But UV is also, like most package managers, a lot of what we do is IO. And Rust is only so helpful with IO, there’s a lot of other things we need to do. Rust is a big part of UV, but it’s not all about Rust.

I do wanna start though with an example that I think illustrates why Rust is helpful and important. And you can do this in other languages too, but we do it in Rust, so that’s what I’m gonna talk about. Okay, version parsing.

Okay, so in Python, every package has a version, right? And you could have a very simple version, like 1.0.0. But they can get very complicated, so you can have pre-releasees. That can be alpha, beta, or RC, which is release candidate. And the pre-release can have a number. You can have beta one, beta two, beta three.

You can also have post releases. So if you need to update, this would typically be if you need to update the documentation but not the source code, you might do a post-release. The contents are the same, but you had to release it again for some reason.

Yeah, there’s also this piece called the local version identifier. Which if you’ve ever worked with PyTorch, you will probably be familiar with this. This is intended for, I’ll probably get this wrong, in spec at least, it’s intended for you’re building a package locally and you want to be able to tag it in some way on your local machine.

PyTorch has now used this, due to other limitations in the packaging ecosystem, to mark packages as being compatible with certain accelerators. So you might have to build a lot of different versions of PyTorch that support different versions of Cuda. And they now use this part of the identifier, just ‘cause it was sort of an open, a free space to indicate that. ‘Cause there’s no other support in the standards for marketing packages as compatible with an accelerator. It’s sort of a hole in the standards. So anyway, this has become very popular now in the Python ecosystem.

Okay, this one, I actually forgot this one existed, and then I was doing the slides. You can do this epoch thing. I actually don’t really remember what this is for, but you can put a number and then an exclamation mark. And that’s a valid Python version. And of course, you can actually compose these things together. You can have a post-release of a pre-release. I’m pretty sure you can have a local version of a pre-release, et cetera, et cetera.

So representing these is pretty hard, it’s very rich syntax. So the full representation of this is something like this, right? We have multiple vectors, which means we’re gonna be allocating memory. ‘Cause the release segments, there can be more than three. There can be as many as you want, actually. It can be 1.1.1.1.1, that’s fine. You can have multiple of those local segments. You can have plus something, plus something, blah blah blah.

So this is pretty heavy, and we are dealing with these things all over the place. So someone on our team, he goes by BurntSushi online, so I should credit him ‘cause he figured this out. He noticed that we can represent over 90% of versions with a single U64. Which is great, because one, it’s fully stack allocated, and there’s a second property that’s really nice about it that I’ll get to in a second.

But this is actually what we use internally. So internally we have a version, and then we have an enum, and we try to represent most versions as the small, this version small. And then we represent things with the full version if they don’t fit into that scheme.

So it’s a U64, so we have eight bytes to work with, okay? Eight bytes of space. So the first two, or the first or last two bytes, however you wanna think about it. Byte six and seven refer to the first release segment.

So when we had 1.0.0, that would be the one. And that’s because calendar versioning is still fairly popular in the Python ecosystem. So we need two bytes for the first release segment because people would have packages that have a version like 2023.1, 2023.4, et cetera.

Okay, the next three bytes just represent the second, third, and fourth release segment. And then the three bytes at the end represent one of a pre-release specifier or a post-release specifier. We do not try to even capture both of them in this representation.

But the really nice thing about this, it’s not just that it’s cheap to… Sorry, it’s not just that it doesn’t have to allocate memory. The really great thing is that greater versions map to larger integers. It’s not just that we’re parsing creating these all the time, we’re also comparing them constantly. Because we want to know, is this version greater than this version? Does this version satisfy this version specifier?

And now, in this representation, you have to be very, very careful in how we constructed the representation. But in this representation, answering that question is just a single mem comp. It’s just like, is this U64 greater than this other U64? As opposed to dealing with those two big version things that have vectors, and we have to understand, blah blah blah.

So most of the implementation of this is actually a huge comment explaining the representation, how it works. It does have limitations, right? We can’t support that epoch thing. You can’t have more than four release segments, like 1.1.1.1. But again, over 90% of versions can be modeled this way.

And yeah, this is actually something we did. When there’s minimal IO, so everything’s fully cached, and we have this very hard resolution that has to do a lot of package version testing, it sped things up three or four times. It was super, super impactful because this is what, we were just spending a ton of time parsing versions, allocating memory for them, and comparing them.

So again, this is just, you can do this with other languages too, but Rust I think is very amenable to doing this kind of thing, and it made a really big difference for us. I mentioned that most, a lot of what we have to do with the package manager is actually IO. So I wanna have go through one or two examples of ways that we try and cheat a little bit with IO.

So I hinted at this before, but when you want to understand the metadata for a package, you need to know its dependencies, it’s not guaranteed that you can actually get that information without running some Python code. But often you can, so when you publish a package to the index, there are two kinds of packages, one is a source package and one is a built distribution.

And the built distributions are probably like most of what you interact with. And those are really important, because when you interact with Python, a lot of what you’re doing is actually interacting with native code, right? So if you use NumPy, or SciPy, or whatever, those have to be built on a bunch of different platforms because they’re not pure Python.

So Python has this extensive support for built distributions. And built distributions do include the metadata, which is great. The built distributions are actually just zip archives. They’re called wheels, I don’t fully understand why. But the suffix is .whl, but it’s actually just a zip file. And somewhere in the zip file there’s a metadata file, literally a file called metadata that contains the metadata for the package.

Some registries will let you ask for this directly, but a lot of them won’t. It just depends on the registry. Like PyPI, the public index will let you just say, “Gimme the metadata.” But for whatever reason, a lot of the commercial registries do not support this yet.

So we wanna get the metadata, but we don’t want to download the whole wheel. Because the wheel, the PyTorch wheels are hundreds of megabytes. And we don’t wanna download them just to know the metadata, because we might have to test a bunch of versions too.

So what we do instead. This is a representation of a zip file. I used to be very scared of file formats, but zip is very simple. It’s sort of just a series of entries. Each entry has a header and then it has the contents of the file. And then at the very end there is what’s called the central directory. It’s kind of like an index.

So the central directory knows what all the files are and where they’re located. You can think of the zip file, it’s just a stream of bytes, and all the files are somewhere. The central directory knows where all the files are.

So what we do is we first make a range request for the central directory. So we guess where it is, we say it’s probably within this many bytes at the end of the file. And then we grab the central directory, which is basically an index of information. And that does not require downloading the whole wheel. We can ask the registry to just give us those end bytes at the end of the file. We then find the metadata file in the central directory, and then we make a second range request just for that metadata file, because the central directory knows where it is.

So we grab the central directory, we figure out what we need to request, and then we go and get the metadata file. Yeah, this has nothing to do with Rust, right, by the way. Other Python tools can do this too. But it does save a lot of time because we don’t have to download these huge files just to answer the question of what packages does it depend on.

Probably the biggest contributor to why UV is so fast and why it feels so fast is the cache design. So UV is, the cache itself is all optimized for warm operations. As in operations where you have the data you want in the cache, and you just need to get it into your environment.

And that’s because, one, most of the time when you’re installing a package, you’ve probably installed it already on your machine at some point in time. That’s may not be true for a continuous integration environment, but on your machine you probably have a lot of copies of the same packages that you’ve installed in different places.

And so we try to optimize for those kinds of interactions, where you have data in the cache and we wanna make it really fast for you to do something with it. So the way that we model this is we have this sort of global cache of unpacked archives.

Recall, every archive is a zip file. We don’t actually store the zip files in the cache. What we do instead is, while we download those files, we just unzip them directly into the cache. So the cache contains the fully unzipped contents of the files.

And when we need to install, the installation operation is basically that we just, we use ref linking where we can, or hard linking. We just link the files into your environment. So if you’re using UV and you need NumPy in a bunch of different environments, we just install it in one place. And then when you install it in your environment, we are basically just creating links to the files in the cache.

That’s really, really fast, and it’s also very space efficient, because it means that you’re not installing the same contents over and over in all your different projects. So again, most installs are just hard linking a bunch of files from the cache into your environment.

So this is just literally just a screenshot of my file system of the cache. The cache looks like this, right? There’s packages, packaged versions, and then it’s just the unzipped contents. And so when you wanna install Rich in your virtual environment, we’re just creating similar to all these files effectively. And that’s really, really fast, which is great.

So this alone contributes to a lot of the feeling of things being instant. Like if you’ve installed something on your machine, you reinstall with UV. A lot of it is due to how we design this cache, and the fact that we try to optimize for those kinds of operations.

Okay, last thing. So this is really good, but it only works for, this only applies to files. A lot of what we need to store in the cache is metadata. So maybe blobs of data, right? Maybe we need to know what are all the available versions of this package. This does not apply to that.

So we use a slightly different trick for those cases, which is we use a technique called zero copy. And this will require the most Rust knowledge, but I’ll try to avoid it. The intuition here is, let’s say that you have a struct, This blob struct and it has a field, and it’s being stored as JSON.

So if you wanna deserialize this, you read the JSON file from disc into memory, and then you run a, basically you run a parser, and then you grab the contents and put them in the struct. The observation of zero copy though is, and I don’t know if anyone will know the difference between these two things. But when you’re trying to create the struct, you already read the JSON file into memory, right? So you already allocated memory to read that file into a string.

So you don’t actually need to allocate more memory to create that blob struct. The version on the left, that requires an allocation. So if we wanna go from the thing at the top to the thing at the bottom, we have to allocate once to read the contents into memory, and then allocate again to create the struct. Instead, we already know that the string is there verbatim in the contents. So ideally instead we could just create a pointer to it.

So we read the JSON into memory, we parse it, and then we ideally, this is sort of theoretical, right? We just create a pointer to it rather than reallocating memory to create everything. So this is what we do, but we do it sort of on steroids I guess.

The way it works is, we store the data on disc in effectively the same representation that it’ll have in memory. And when we read it back, we’re basically just doing a pointer cast to go from red data to fully realize structs. We use a library for this called Archive, which is very good. And there are some safety checks around this of course. I mean, it’s totally unsafe for us, but there are safety and validation checks you can do around this.

But the really cool thing about this is the deserialization does not scale with your data. So you have to read the contents from disc, and as you have more and more data, that file will be bigger and bigger and you have to read more and more. But going from the data that you read to the fully, the deserialized struct, that does not scale as the data gets larger.

Unlike with JSON, right? With JSON, you’d have to parse it, right? You would have to go through all these operations that would get slower and slower as the data got bigger. The really cool thing about, in my opinion at least, about zero copy to serialization is the deserialization does not scale with your data. So it doesn’t matter, really how big the struct is or how large that string is. It does matter for reading the data from disc, but it does not matter for deserializing it into memory.

Okay, that was the last thing I was gonna cover. I had a bunch of other things I wanna talk about, but I just put links to them and maybe I can share the slides. And I think that’s it.