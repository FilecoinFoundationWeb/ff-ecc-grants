# FF ECC Grants

#### Filecoin Foundation + Electric Coin Co. Grants Website

<p align="left"><img src="static/images/open-graph.png" width="550" alt="ff ecc grants image" /></p>

## Overview

- This is the repository for the _FF ECC Grants_ website ([ff-ecc-grants.org](https://ff-ecc-grants.org))

- This repo represents a static site which requires compilation, but can then be served as a static resource
- This site is hosted on IPFS and is compatible with relative URLs, for IPFS and IPNS gateway paths
- The site's resources are served statically, but internal navigation is virtualized: in other words, the site acts as an SPA when browsed on the client
- While a static site, this app can be extended at any time to a full application by changing the `target` in settings

## Stack
- Requires nodeJS and has been tested on node 16
- Uses a Vue framework, [nuxtJS](https://nuxtjs.org/), deployed in static mode

## Build
To build this site locally
- Clone this repo
- Make sure NodeJS 16 or newer is installed
- To build a static site
    - Run `npm ci && npm run generate`
    - A directory `dist` is created, which contains the static site output
- To run locally, for features like hot reload
    - Run `npm ci && npm run dev`
    - The site will be available in real time via a localhost URL
    - Resources are compiled in this process; for example, all SCSS styles are converted to CSS and tree-shaken

## Structure
Key areas of this repo include
- `/pages` - All page templates
- `/components` - Each reusable collection of elements is abstracted to a component, and most components accept various properties that determine the way they are rendered
- `/static` - Static resources which will be available post-compile
- `/assets/scss` - The global styles for the app are available here in SASS/SCSS, more specific styles can be found at the bottom of `.vue` pages and components ([single file components on vuejs.org](https://vuejs.org/guide/scaling-up/sfc.html))
- `/assets/svgs` - Contains iconography or other small vectors, in SVG format
- `/content` - The site's content, which is edited using the Forestry CMS

## URLs and branches
- Staging - `develop` builds to `a non public url`
- Production - `main` builds to `ff-ecc-grants.org`
- Content - `content` is a branch that the CMS writes to
  - When pull requested against `main`, the `content` branch will be auto approved by a Github action
- Each PR will also generate an IPFS build preview link, so it can be validated before being merged

## Managing Content
- Editing content directly
  - Structured content can be found in `json` files
  - Written paragraph-type content can be found in `md` files, in markdown format
  - See the `content/pages/` directory
