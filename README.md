# Bot Builder SDK

This is a personal fork from [Microsoft's Bot Builder SDK](https://github.com/Microsoft/BotBuilder) at v1.0.1 for NodeJS.

## Changes
- Added `SlackBot.listenForMentionsAndDirectMessages` to allow queries to be received and processed on Direct Messages as well.
- Added support for [Slack's Interactive Message Buttons](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwjonJXVysfOAhVDj5QKHbPdBt4QFggeMAA&url=https%3A%2F%2Fapi.slack.com%2Fdocs%2Fmessage-buttons&usg=AFQjCNFHC6txg6yCx6lztvPEVkwEuDpxmw) via `SlackBot.listenForMentionsAndDirectMessages` upon emit of `interactive_message` from `Botkit`'s `BotController`.
