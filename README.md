# Text Parser Frontend

## What is this?

This is the decoupled frontend for a backend that analyses text. It contains a form with a file upload that posts to our backend, and when we receive a successful answer we display the data in a (pretty usable) format. The bulk of that data is the text from the uploaded file, where we've found all occurrences of the most common word and surrounded it with _foo_ and _bar_.

As a bonus we've added a couple of buttons to click:

- Download original text
- Download modified text
- Highlight changes

Try them out!

## Installation

This app is built on Vue, with Vue CLI. The generated app is essentially static files, so you don't need anything to run those. Just point your favorite server to the dist directory and you're done.

However, in order to modify the source and generate a new build, you'll want to install Vue CLI and its dependencies:

- https://cli.vuejs.org/guide/installation.html

Once that is taken care of you can use the following commands:

Project setup:
```
npm install
```

Compiles and hot-reloads for development:
```
npm run serve
```

Compiles and minifies for production:
```
npm run build
```

Run your tests:
```
npm run test
```

Lints and fixes files:
```
npm run lint
```

## Improvements

It's easy to be critical of your own work, especially if it's a small demonstration like this. If I were to revisit this frontend again I would probably fokus on the following areas:

- Styling and typography. For a text parsing app, the general readability and styling are woefully underworked.
- Features. We could highlight so much more fun things, like show hidden characters in the processed text.
- Code. We could refactor and make everything much tidier - we are a bit lacking in the structure department. To be honest, doing it with a feature set as small as this would probably be unnecessary complication, but if the app would grow it would be critical.
- Tests. There are none right now.

## Wait, who are you again?

I'm Linus! You can find me here:

- https://linusbohman.se

And the two repos for this app can be found here:

- https://github.com/bohman/text-parser-backend
- https://github.com/bohman/text-parser-frontend

Live demos for frontend and backend can be found here:

- http://text-parser.linusbohman.se
- http://text-parser-backend.linusbohman.se

Cheers! I hope you're having a great day!
