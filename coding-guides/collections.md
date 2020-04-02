---
description: >-
  In this page we will explore Collections, and how to use them to grab data
  from various part of the API.
---

# Collections

A **Collection** is a _utility class_ that stores data. Collections are the Javascript Map\(\) data structure with additional utility methods. This is used throughout discord.js rather than Arrays for anything that has an ID, for significantly improved performance and ease-of-use.

Examples of Collections include:

* `client.users.cache`, `client.guilds.cache`, `client.channels.cache`
* `guild.channels.cache`, `guild.members.cache`
* message logs \(in the callback of **`fetchMessages`**\)
* `client.emojis.cache`

##  Getting by ID

 Very simply, to get anything by ID you can use `Collection.get(id)`. For instance, getting a channel can be 

`client.channels.cache.get("81385020756865024")`

 Getting a user is also trivial: 

`client.users.cache.get("139412744439988224")`

##  Finding by key

If you don't have the ID but only some other property, you may use `find()` to search by property:

`let guild = client.guilds.cache.find(g => g.name === "NextGen Team");`

The `.find()` method also accepts a function. The _first_ result that returns `true` within the function, will be returned. The generic idea of this is:

`let result = <Collection>.find(item => item.property === "a value")`

Obviously this looks a lot like the key/value find above. However, using a custom function means you can also be looking at other data, properties not a the top level, etc. Your imagination is the limit.

Want a great example? Here's getting the first role that matches one of 4 role names:

```javascript
const acceptedRoles = ["Mod", "Moderator", "Staff", "Mod Staff"];
const getModRole = member.roles.cache.find(role => acceptedRoles.includes(role.name));
if(!modRole) return "No role found";
```

{% hint style="info" %}
 Don't need to return the actual role? `.some()` might be what you need. It's faster than find, but will only return a boolean true/false if it finds something:
{% endhint %}



```javascript
const hasModRole = member.roles.cache.some(role => acceptedRoles.includes(role.name));
// hasModRole is boolean.
```

##  Mapping Fields

One great thing you can do with a collection is to grab specific data from it with `map()`, which is useful when listing stuff. `<Collection>.map()` takes a function which returns a string. Its result is an array of all the strings returned by each item. Here's an example: let's get a complete list of all the guilds a bot is in, by name:

```javascript
const guildNames = client.guilds.cache.map(g => g.name).join("\n")
```

Since `.join()` is an array method, which links all entries together, we get a nice list of all guilds, with a line return between each. Neat!

We can also get a most custom string. Let's pretend the `user.tag` property doesn't exist, and we wanted to get all the user\#discrim in our bot. Here's how we'd do it \(using awesome template literals\):

```javascript
const tags = client.users.cache.map(u=> `${u.username}#${u.discriminator}`).join(", ");
```

##  More Data!

 To see **all** of the Discord.js Collection Methods, please [refer to the docs](https://discord.js.org/#/docs/main/stable/class/Collection). Since Collection extends Map\(\), you will also need to refer to [this awesome mdn page](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Map) which describe the native methods - most notably `.forEach()`, `.has()`, etc.

