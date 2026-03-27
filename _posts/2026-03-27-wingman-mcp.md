---
layout: post
title: Wingman-MCP
categories:
- AI
- MCP
tags:
- Wingman
- MCP
description: Giving AI Models knowledge about Workspace ONE UEM
comments: false
date: 2026-03-27 16:43 +1000
---
For the last couple of months I've been working some (more) side projects, and after meeting with some long-term colleagues at our recent Sales Kick-Off, it made me realise I need to start sharing more of the interesting things I get to do.

**tl;dr?** - [Download Links](#download)

---

## What is Wingman?

![Wingman Logo](/assets/img/wingman.png){: .left w="120" } Before we get into the the MCP part, I should start with Wingman itself. Wingman is the overall term I've given for set of tools that act as your Wingman when it comes to deploying, managing and supporting Workspace ONE. One of the things I've learned over the last couple of years specifically is that a lot of the things we get asked as technical folks are just the same thing - "How do I do X?", "What does Y mean?" or "How can I do Z using an API?".

So, just like everything now lets push that responsibility to a chat agent. However, to do that we need to give it the actual knowledge to respond correctly rather than it being like that one person that **doesn't actually know but wants people to think they do so will just make up stuff to sound correct**.

At the *heart* of Wingman is a vector database to leverage [Retrieval Augmented Generation](https://blogs.nvidia.com/blog/what-is-retrieval-augmented-generation/) (RAG for short) to give the LLM specific information to enhance the accuracy and reliability of the results. 

Fundamentally, the data provided via RAG with Wingman is the **entirety** of:

- [Omnissa Docs](https://docs.omnissa.com/) content
- Tech Articles and How-Tos from [Tech Zone](https://techzone.omnissa.com/)
- Workspace ONE Release Notes
- And all of the Workspace ONE [APIs and Documentation](https://developer.omnissa.com/)

This, hopefully, makes it smart enough to handle any kind of task it needs to answer about the Workspace ONE UEM Platform.

## So, what is the MCP bit?

[Model Context Protocol](https://modelcontextprotocol.io) (MCP) is a "server" that connects AI assistants and tools (Claude, ChatGPT, Codex etc.) directly to your other tools, agents - or in our case - RAG processes. There is a lot new terms in this new AI world, and I am definitely no expert, but I like to think of MCP as being the REST API of the LLM world. It is a standardised way that allows the developer to expose capabilities that can be leveraged agnostically across AI tools and agents.

In the Wingman world, just because we have a vector database that has all of the content in it, something like Claude cannot just natively query it. So MCP gives an interface for Claude to send context around what it needs to get information on, and the MCP server returns it in a standardised way that any (well, most) AI Assistants and Tools can understand. 

And its not just for accessing data via RAG. MCP allows you to publish other capabilities using agents or even straight up tasks/tools where it understands which tool or agent to get the outcome. You could expose a way for a user to ask a question to ChatGPT like "How many Windows devices do I have that require Windows Updates?" and the MCP Server can call the APIs in your environment needed to gather the response.

So for Wingman, that's exactly what Wingman-MCP does. Its the middleware that knows how to return information about anything Workspace ONE related.

---

## Who Is It For?

Right now, it's for anyone administering, designing or supporting Workspace ONE UEM. 

If you spend your days managing device fleets, troubleshooting enrolment issues or just trying to find that one setting buried three menus deep in a portal - this is for you. Given that I deliberately didn't just want to ingest *only* content from Omnissa Documentation, Wingman has content from our Product Specialists on TechZone with real "how-to" information as well to give a much more rounded context to the answers.

---

## What Can It Actually Do?

  
This is the part I'm most excited about, because it's not just one thing. Wingman is the "brain" that has all of the update to date knowledge, but I have a heap of other tools with Wingman I'm building that all build of this base capability.

#### Right Now:

Wingman-MCP is just the first part that gives a way to start leveraging the simplest of AI/LLM tasks - retrieving tailored information.

**Ask questions in plain English.** Instead of navigating portals to find information, just ask. "What are the new features for iOS in the Workspace ONE UEM release?" or "Where do I go to see which devices have failed Windows Updates?"  and get a real answers pulled from documentation and guidance data. You can also ask it questions about your environment - "How many devices do I have enrolled?".

**Contextual Awareness.** The database used for RAG already has all of the latest release notes across versions so you can (once exposed) ask it to provide you a summary of the latest capabilities and fixes that are relevant to your environment. It knows what there *is* and it can find out what you *have*, so why show information about an OS or capability you don't use.


{: .prompt-tip }
> Try asking this:
>
> "`Check the latest release notes and tell me what's relevant to my environment`"


### Coming Soon:

**Automate the repetitive stuff.** Managing Workspace ONE is full of tasks that are annoying to do manually but relatively straightforward to describe. Wingman-MCP aims to let you hand those off to an AI Agent that can actually carry them out, not just tell you the steps. Right now, Wingman can 100% get information about your Workspace ONE environment but I just want to make sure I can provide this capability in a secure fashion.

**Contextual Guidance.** I also have in my back pocket (aka. an unpublished Git repo) a Browser Extension that understands the context of what area in the Workspace ONE UEM Admin Console you are in, and will display accurate documentation links for that specific capability without you needing to locate or search Omnissa Docs. If you provide the Wingman process access to a more capable LLM, you can also ask it specific questions about what is on the page directly from the browser.

---

## Why Bother?

If you know me - or any of the *other* tools I've built - you know its mostly because I believe there is a better and easier way to do the repetitive or difficult tasks.

A problem is only a problem until is solved.

It still early days, but the basics are solid and I'm fortunate to be able to work on these things that keep me interested that fix real customer problems. 
## So What's Next?

The near-term focus is building out the tool library and exposing more capabilities than just "information":

- Query live information about your Workspace ONE Environment
- Improve the matching logic of the context to returned data
- Bring in Omnissa Horizon and Workspace ONE Access information
- Introduce self-learning and feedback to the MCP Server and RAG database processes so it will learn from what *you* tell me to make it more personalised.

The goal is a set of tools that cover the things Workspace ONE customers and partners actually ask about every day - built to be practical, not just impressive in a demo or AI because everyone SaaS company has to have that.

---

More updates coming as the tool library grows ✌️

### Download

{: .prompt-info }
> **Github Repository**
>
> [Wingman](https://github.com/tbwfdu/wingman)

