# Document

[Site](https://torai55.github.io/blog/)

This blog is using [Hugo](https://gohugo.io/documentation/) for generating static site with [Blowfish](https://blowfish.page/docs/) theme.

## Development

- create a new post: `$ hugo new posts/filename.md`
- create a new post using folder in archetypes: `$ hugo new --kind <archetypes-folder> posts/url-pathname`
- start a dev server including draft content: `$ npm run server`
- compile `main.css` with watch mode: `$ npm run dev`

## Build

1. compile `main.css`: `$ npm run build`
2. build a site: `$ hugo`
