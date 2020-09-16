---
layout: page
title: Auxify
categories: project_page
permalink: /projects/auxify
blurb: Auxify is a shared Spotify play queue that allows your friends and family to queue songs of their choosing onto your queue! 
---
---

_{{page.blurb}}_
---

## Origin story 
A little while ago, I was listening to music on Spotify through a bluetooth speaker with some friends. We were passing around my phone whenever someone wanted to enqueue a song of their choice, but it pained me that there wasn't a better way, a way for everyone to add songs without needing to physically take my smartphone. That's when I started working on Auxify. Just sharing a room ID and a room code allows people to joom my room and enqueue songs of their choice onto the play queue whenever they want. Since then, Spotify released the [group session](https://support.spotify.com/us/article/group-session/) feature which fills the same niche, but I finished and launched the site regardless. Auxify is available [here](https://auxify.reidswan.com).

## What's in a name?
The name is a portmanteau of "aux chord" and "Spotify" - the idea being users virtually pass around an aux chord, connected to one Spotify account. 

## The tech
_You can view the frontend source [here](https://github.com/reidswan/auxify-frontend) and the backend source [here](https://github.com/reidswan/auxify)_

The code is split into separate repositories for the backend and frontend. 

### The backend
Auxify's [backend](https://github.com/reidswan/auxify) is a Python REST API, written to target Python 3.8. It makes extensive use of Python's `asyncio` facility for asynchronous programming. I used the [`aiohttp`](https://docs.aiohttp.org/en/stable/) web framework, a stable, `asyncio`-first web framework with a clean and easily useable interface. The deployed site uses [`gunicorn`](https://gunicorn.org) as the WSGI server; both the backend and frontend have [NGINX](https://www.nginx.com) as a reverse proxy in front. Most of the utilities used in the backend are provided directly by `aiohttp`.  

For the persistence layer, I settled on [`sqlite3`](https://www.sqlite.org). Initially, I was working with MySQL, but I wanted to avoid unnecessary additional complexity on a website I don't expect to achieve very many concurrent users. Websites with far greater performance requirements successfully use `sqlite` for persistence, and avoiding the additional complexity and operational overhead and/or cost of a MySQL server seemed worth the eventual, very distant scale barrier, especially given the app's very low reliance on persistence. I use the [`aiosqlite`](https://pypi.org/project/aiosqlite/) library to provide an `asyncio` layer on top of Python's built-in `sqlite3` library. 

### The frontend
I was a little more experimental with Auxify's [frontend](https://github.com/reidswan/auxify-frontend/). I had worked with [React](https://reactjs.org) in a professional capacity at takealot.com, but I had never used anything other than the Semantic UI framework, and hadn't touched [redux](redux.js.org). I decided to use this as an opportunity to venture further into the JS ecosystem. I settled on [Grommet](https://v2.grommet.io/) as a UI framework - easy-to-use, low overhead, support for theming, flexibility and good-looking UI components out of the box, it satisfied all the requirements I was looking for in a UI framework. [Axios](https://github.com/axios/axios) took a lot of the overhead away from managing network requests. Redux made state management and testing components a breeze.

I still intend to investigate adding TypeScript to the codebase, but given the size of the project, it might be more hassle than it's worth. 


### Future directions
I would like to add an integrated player using Spotify's [web playback SDK](https://developer.spotify.com/documentation/web-playback-sdk/), specifically to give user's a view into the current state of the queue. The idea would be to put this onto a shared screen like a TV for everyone to see. 

An interesting, but legally tricky, idea is to monetize the app by using it as a sort of "jukebox" - a bar or similar establishment can allow users to use credits to enqueue songs from a predetermined list of the establishment's choosing. 
