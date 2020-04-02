# Making an Eval command

##  What is eval exactly?

 In JavaScript \(and node\), `eval()` is a function that evaluates any string _as javascript code_ and actually executes it. Meaning, if I `eval(2+2)` , eval will return `4`. If I eval `client.guilds.cache.size`, it'll return however many guilds the bot is currently on. And if I eval `client.guilds.cache.map(g=>g.name).join('\n')` then it will return a list of guild names separated by a line return. Cool, right?

##  But eval is dangerous

I'll say this in a way that's probably dead simple to understand: Giving someone access to eval\(\) is literally like sitting them at your computer, with full admin access, and then stepping out of the room. eval\(\) in browser javascript is trivial and not dangerous - you're running in your own browser, anything you fuck up is going to be on your own PC, not the web servers.

But eval\(\) in node is really, really dangerous and powerful. Because it can run anything you run as a bot, and it can also run code you're not expecting to run, if someone else has access to it. Node.js has access to your hard drive. The whole thing. Every bit of it. To understand what this means, look at the following command: rm -rf / --no-preserve-root . Do you know what this command does? It deletes your entire server's hard drives. I mean, it only works on Linux, but most VPS systems and most hosting providers are on UNIX-based systems.

Another thing that's on your hard drive is passwords. Have a config file with your database password? I can get that. config.json with your token and other API keys in it? I can grab that easy. Hell I can just grab your token straight from the client object if I know how to.

