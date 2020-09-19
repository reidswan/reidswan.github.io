---
layout: post
title:  "Updates to Auxify"
date:   2020-09-16 19:26:45 +0200
categories: auxify projects announcement
---

After a limited trial run of [Auxify][auxify] - working Friday at my mom's house, playing Spotify in the background - I spent last night and this morning ironing out some kinks and usability issues we discovered over the course of the day, and deployed the changes this morning. 

- The `+` icon on the home page now directs you to either join or create a room; supply an owner ID or a room ID, and you'll be directed to join the corresponding room.
- Owners can now reveal the room code while inside a room to give to their friends. There is also a new room deactivation button.
- Improved the feedback on enqueueing a song
    - For 1.5 seconds after a song has been enqueued, there will be a green success indicator
    - While a song is being enqueued, it is disabled and cannot be enqueued again until success
- Fixed a bug that caused rooms to be listed on the owner's home page multiple times (once for each member)

As always the code is available on [my GitHub][my-github]: the [frontend](https://github.com/reidswan/auxify-frontend) and the [backend](https://github.com/reidswan/auxify)

I won't be making announcements for every change to every project, by the by. It's just that both reidswan.com and Auxify are new, and the blog section looked a little bare. I didn't want the introductory post feeling lonely. I've yet to make up my mind what this blog will be dedicated to, and I'm running light on blog post ideas. I'm using this commit to add Google analytics, though; I'll be able to say quite definitively that 0 people are reading this. 


[my-github]:   https://github.com/reidswan
[auxify]:      https://auxify.reidswan.com/
