# botbuilder-wit [![Build Status](https://travis-ci.org/sebsylvester/botbuilder-wit.svg?branch=master)](https://travis-ci.org/sebsylvester/botbuilder-wit) [![npm version](https://badge.fury.io/js/botbuilder-wit.svg)](https://badge.fury.io/js/botbuilder-wit) [![codecov](https://codecov.io/gh/sebsylvester/botbuilder-wit/branch/master/graph/badge.svg)](https://codecov.io/gh/sebsylvester/botbuilder-wit)

Node.js module that provides [Wit.ai](https://wit.ai) NLP integration for the [Microsoft Bot Builder SDK](https://dev.botframework.com/).

## Installation

`npm install --save botbuilder-wit`

## Usage
This package does **not** work with Wit.ai's *Story* feature. It was designed to be used in conjunction with the IntentDialog class.
```
const { IntentDialog } = require('botbuilder');
const WitRecognizer = require('botbuilder-wit');
const recognizer = new WitRecognizer('Wit.ai_access_token');
const intents = new IntentDialog({recognizers: [recognizer]});

intents.matches('intent.name', (session, args) => {...});
intents.onDefault(session => {...});

bot.dialog('/', intents)
```

## Using Entities

You can use the utility class [EntityRecognizer](https://docs.botframework.com/en-us/node/builder/chat-reference/classes/_botbuilder_d_.entityrecognizer.html) to parse & resolve common entities.
```
// Inside your dialog handler that receives the session and arguments object
const { EntityRecognizer } = require('botbuilder');
const location = EntityRecognizer.findEntity(args.entities, 'location')
```

## Using the Wit.ai client
You can still use the Wit.ai client directly by accessing the ```witClient``` property of the instantiated WitRecognizer.
```
const recognizer = new WitRecognizer('Wit.ai_access_token');
const witClient = recognizer.witClient;
```
## Recompiling the TypeScript source
If you want to recompile the source, you will need to make sure the ```node-wit``` dependency has a type definitions file in its root directory. Even though there is a TypeScript definitions package for node-wit you can install with ```npm install --save-dev @types/node-wit```, the compiler will complain when using it. So instead, you can use the minimalistic version in the resources directory that will do the job.

## License

MIT