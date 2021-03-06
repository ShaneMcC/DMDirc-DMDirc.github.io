---
layout: post
title: Even more intelligent tab completion
author: Chris Smith
author_github: csmith
---
In DMDirc 0.5 we introduced a feature described in the release notes as "intelligent tab completion for commands" (introduced in <a href="{% post_url 2007-08-18-introducing-intelligent-command-completion %}">this blog post</a>), which allowed commands to tell the tab completer about the arguments that they're expecting. In that incarnation, commands can specify a bunch of extra words to add, and can toggle whether the default tab completion targets (nicknames, channel names, command names) are used.

In DMDirc 0.6, we've taken this one step further. Commands can now specify exactly what group(s) of targets should be used - so, for example, the first argument of the <code>/ctcp</code> command will now only tab complete to nicknames and channel names (but not command names, as it would have done in DMDirc 0.5).

We've also added support for what I call "deferred intelligent tab completion". This comes in to play with the half-dozen or so commands that take another command as one of their arguments, such as the <code>/alias</code> command, which takes an alias name and then a command to associate with that alias. So, say you want to create an alias to start a timer that will CTCP PING a certain person after five seconds. You type: <code>/ali<strong>&lt;tab&gt;</strong> ping /tim<strong>&lt;tab&gt;</strong> 1 5 /ctcp Nickname <strong>&lt;tab&gt;</strong></code>. When you hit that final tab, DMDirc suggests eight standard CTCP types (PING, FINGER, VERSION, etc...), even though the CTCP command is in the middle of a much larger command. How's that for intelligent tab completion?

As far as I'm aware, no other IRC client comes close to the intelligence of DMDirc 0.5's tab completer, so DMDirc 0.6's puts us leagues ahead of the competition in that respect. But, as ever, we're eager to hear any feedback or suggestions that you might have - feel free to leave a comment here, drop by #DMDirc on Quakenet to talk to us, or use the "Send feedback" feature (available in the help menu) of DMDirc 0.5.5.