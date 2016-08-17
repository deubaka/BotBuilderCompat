# Bot Builder for Node.js

Refer to Microsoft's Official [BotBuilder NodeJS rep](https://github.com/deubaka/BotBuilder/tree/compat/Node)o for more info.

## Changes
- Added `SlackBot.listenForMentionsAndDirectMessages` to allow queries to be received and processed on Direct Messages as well.
- Added support for [Slack's Interactive Message Buttons](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwjonJXVysfOAhVDj5QKHbPdBt4QFggeMAA&url=https%3A%2F%2Fapi.slack.com%2Fdocs%2Fmessage-buttons&usg=AFQjCNFHC6txg6yCx6lztvPEVkwEuDpxmw) via `SlackBot.listenForMentionsAndDirectMessages` upon emit of `interactive_message` from `Botkit`'s `BotController`.

## Usage
### SlackBot.listenForMentionsAndDirectMessages
```javascript
var slackBotInstance = new BotBuilder.SlackBot(botController, bot);
slackBotInstance.add('/', BotDialog);
slackBotInstance.listenForMentionsAndDirectMessages();
```

Where in, `botController` is an instance of your `Botkit.slackbot` and `bot` is an instance of your instantiated bot.

### Slack Interactive Message Bridge
Given an example `/slack_actions` running on Express.

```javascript
app.post('/slack_actions', function (req, res) {
	if ('Your Slack Verification Token' === payload.token) {
		var payload = JSON.parse(req.body.payload);
		var message = payload;
		
		for (var key in req.body) {
		    message[key] = req.body[key];
		}
		
		message.user = message.user.id;
		message.channel = message.channel.id;
		
		// We pass the value to process as respone for BotBuilder
		message.text = message.actions[0].value;
		
		botController.findTeamById(message.team.id, function (err, team) {
		    if (team) {
		    	// Send a confirmation message for request not to timeout with Slack
		        res.status(200);
		        res.send(message.text + ' it is then! :robot_face:');
		
		        var bot = controller.spawn(team);
		
		        bot.team_info = team;
		        bot.res = res;
		
		        message.type = 'message';
		        message.source = 'interactive';
		
		        botController.trigger('interactive_message', [bot, message]);
		    } else {
		    	// Respond to message any way
		        res.status(200);
		        res.send('Oops! Something went wrong. Please try again.');
		    }
		});
	}
});
```

Where in, `botController` is an instance of your `Botkit.slackbot`.

