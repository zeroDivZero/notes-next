# HOW IT WORKS

## Environment

Cxt in which app is run.

### Development

Optimized for dev experience, with features like TypeScript and ESLint integration, and Fast Refresh.

### Production

Optimized for end-users. Aims to transform code to make it performant and accessible.

## Compiler

Handles **code transformations** and underlying infrastructure to make it easier for app to go to prod.

Written in Rust and SWC, platform for compilation, minification, bundling, etc.

Devs write code in dev-friendly languages like JSX, TypeScript, and modern versions of JS. Compiling takes code in one language and outputting it in another, or another version of that language.

![Compiling](/assets/how_it_works/compiling.png)

In Next, compilation happens during dev (editing code), and as part of build step to prepare app for prod.

## Minifying

Removes unnecessary code formatting and comments without changing functionality. Improves perf by decreasing file sizes.

![Minifying](/assets/how_it_works/minifying.png)

In Next, JS and CSS files automatically minified for prod.

## Bundling

Devs break up app into modules, components, and functions. Exporting and importing internal and external 3rd-party packages create complex web of dependencies.

Bundling resolves dependencies, merging/packaging files/modules into optimized bundles for browser, to reduce number of file requests when user visits.

![Bundling](/assets/how_it_works/bundling.png)

## Code-Splitting

App usually split into multiple pages, each becoming unique entry point (URL). Code-splitting splits bundle into smaller chunks required by each entry point. Improves initial load time by loading minimal code for that page.

![Code-Splitting](/assets/how_it_works/code-splitting.png)

Next has built-in code-splitting support. Each file inside `pages/` directory automatically code-split into own JS bundle during build step.

Further:

* Code shared among pages also split into another bundle to avoid re-downloading.
* After initial load, Next can start preloading code of other pages users likely to visit.
* Dynamic imports are another way to manually split what code is initially loaded.

## Build Time

Or build step, is series of steps to prepare app for prod. Next transforms code into optimized files to be deployed to servers and consumed by users. Include:

* HTML files for statically generated pages
* JS code to render pages on server
* JS code to make pages interactive on client
* CSS files

## Runtime

Or request time, is period of time app runs in response to user's request, after app built and deployed.

## Client

In cxt of web apps, client is browser on user's device that sends request to server for app. Turns response into UI.

## Server

Computer in data center that stores app, receives requests from client, does computation, and sends back response.

![Client Server](/assets/how_it_works/client-server.png)

## Rendering

Unavoidable work to convert code to HTML representation of UI. Can take place on server or client. Can happen ahead of time, at build time, or on every runtime request.

### Pre-rendering

Includes server-side rendering and static site generation, external data fetched and React components transformed into HTML before result sent to client.

### Client-side vs Pre-rendering

In standard React app, browser receives HTML shell from server along with JS to construct UI (client-side rendering, initial rendering happens on user's device).

![Client-side Rendering](/assets/how_it_works/client-side-rendering.png)

Next pre-renders by default. Can opt for client-side rendering for specific components with data fetching hooks like React's `useEffect` or `useSWR`.

![Pre-Rendering](/assets/how_it_works/pre-rendering.png)

### Server-Side Rendering

HTML generated on server *per request*.

On client, HTML used to show fast non-interactive page, while React uses JSON data and JS instructions to make components interactive (e.g., attaching event handlers to button). Process called **hydration**.

In Next, opt in to server-side render pages with `getServerSideProps`.

### Static Site Generation

HTML generated on server, but unlike server-side rendering, no server at runtime. Content generated once at build time when app deployed, HTML stored in CDN and re-used per request.

In Next, opt in to statically generate pages with `getStaticProps`.

Can use **Incremental Static Regeneration** to create or update static pages after site built. No need to rebuild entire site if data changes.

## Network

Where app code stored and run after deployed. Linked computers (or servers) capable of sharing rscs.

### Origin Server

Main computer that stores and runs original ver of app.

When origin server receives request, it does some computation, result can be moved to CDN (Content Delivery Network).

### Content Delivery Network (CDN)

Between client and origin server, stores static content (such as HTML and image files) in multiple locations around world. When request comes in, closest CDN location to user can respond with cached result.

![CDN](/assets/how_it_works/cdn.png)

Reduces load on origin, since computation doesn't need to happen on each request. Faster response for user.

### Edge

Generalized concept for fringe of network, closest to user. CDNs could be considered part of it.

Distributed to multiple locations around world. Unlike CDNs, some Edge servers can run small snippets of code; i.e., caching and code execution can be done at Edge closer to user.
