# djs-pagination
This is a utility to paginate discord embeds. It's meant for discord.js master (12.0.0) but it should also work for older versions.

## Installation
`npm install djs-pagination`

## Usage
**Usage**
```js
// Import the package
const Paginator = require('djs-pagination');
// Import MessageEmbed (or RichEmbed on stable)
const { MessageEmbed } = require('discord.js');

// First parameter is an array of MessageEmbeds (optional) to be set as the starting pages (you can add to them further with the add method). 
// Second is the filter and the timeout.
// The filter is the same as the Discord.js ReactionCollector filters with ignoring bots & limited to the emojis built-in. 
// The timeout is the time the paginator is active (default 5 minutes).

new Paginator([], { filter: (reaction, user) => user.id === '123', timeout: 60000 }) 
	.add(new MessageEmbed().setTitle('Page 1').setDescription('Description')) // These all need to be MessageEmbeds or RichEmbeds.
	.add(new MessageEmbed().setTitle('Page 2').setDescription('Description'))
	.setEndPage(new MessageEmbed().setTitle('Done')) // This is optional, when the paginator is finished after timeout it will edit itself to become this if provided.
	// Optional, this will be run for every page currently. Put this after you've added all your pages (first parameter current embed, second index, third amount of pages)
	.setTransform((embed, index, total) => embed.setFooter(`Page ${index + 1} / ${total}`)) 
	.start(message.channel); // ID is currently not supported, only a valid text-based channel will work.
```

