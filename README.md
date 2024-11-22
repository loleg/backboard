# Backboard

This is a single page application (SPA) that shows the projects and challenges for a hackathon event using [hackathon.json](https://codeberg.org/dribdat/hackathon.json/) or [Data Packages](https://frictionlessdata.io/). Usually this is connected to a remote API or export of data from [Dribdat](https://dribdat.cc), an open source hackathon management system. 

Project data is shown for a specific event, with flexible configuration options for displaying and sorting the results in different ways. You can seamlessly navigate using your mouse or keyboard between projects and challenges. 

Currently some functions link back to Dribdat, for example, when you click on the **Join** team button you get directed to the main web application. These functions will be soon phased out and moved into a more modern, decoupled frontend.

The Backboard has minimal formatting, tight margins, and is ideal for embedding into your webpage anonuncing the upcoming event or results. If you are developing a Vue.js app, you can import the Challenges, Honeycomb and Preview components into your app.

**Tip:** You may want to enable *Challenges* and *Previews* (opens a modal dialog with swipable navigation) through clicking the `options` button found at the footer of the page (which opens a configuration menu). 
Use the handy *Share* link to get a URL with your config.

**Demo:** https://backboard.vercel.app/

## Installation

Deploy this application with any service that supports Node.js 

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/git/external?repository-url=https%3A%2F%2Fgithub.com%2Fdribdat%2Fbackboard)

TIP: You may want to set the **options** with the link at the bottom of the page - click the Share button, and paste the query string (everything after ?&) into your `VUE_APP_DEFAULT_OPTS` variable.

## Usage

Put a `datapackage.json` file that you exported from dribdat into the **public** folder.

Or use the `VUE_APP_DRIBDAT_URL` configured with a link to your dribdat event or data package elsewhere.

You can use the following environment variables:

- `VUE_APP_DRIBDAT_URL` (required) - fully qualified link to your [Dribdat site](https://dribdat.cc), a specific event, or online hosted Data Package (\* see examples)
- `VUE_APP_DEFAULT_OPTS` - the default display settings - copy the part after ? from the Share link.
- `VUE_APP_HIDE_TOOLBAR` - makes the options toolbar in the footer unavailable.
- `VUE_APP_VOTE_FORM_URL` - link to a form where you are collecting votes or feedback, otherwise the Dribs Post feature will be used.
- `VUE_APP_TIMER_LENGTH` - in minutes, how long the countdown timer should run for in presentation mode (0 to disable).
- `BACKBOARD_ROOT` - if your deployment is not at the root, change it here (e.g. `/backboard`)

\* Examples:

- https://meta.dribdat.cc/
- https://meta.dribdat.cc/event/5
- https://meta.dribdat.cc/event/5/hackathon.json
- https://meta.dribdat.cc/api/event/current/datapackage.json
- https://meta.dribdat.cc/api/project/top.json

Pro tip: the JSON files could also be hosted elsewhere!

## Development

To run locally, install Node.js and Yarn, then to start a development server:

```
yarn install
yarn serve
```

## Credits

Created using Vue.js and CodeSandbox.

See also this earlier version: https://github.com/dribdat/dribdat2_frontend

## Why backboard?

![](https://upload.wikimedia.org/wikipedia/commons/9/9a/Zh_Basketball_backboard_and_basket_bitmap_1940.svg)

_Players typically aim for the box in the backboard when making a shot in basketball._

[MIT License](LICENSE)
