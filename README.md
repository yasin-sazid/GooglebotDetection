# Crawler Detection with Angular Universal

A server-rendered Angular application that identifies crawler requests at the Express boundary. The project brings request inspection into an Angular Universal rendering workflow, showing where bot-aware behavior belongs in a full-stack frontend application.

## Request lifecycle

```text
Incoming request
      |
   Express
   /     Static   Page route
assets      |
       Crawler detection
            |
       Angular Universal rendering
```

[server.ts](server.ts) serves built assets with caching and processes page routes through `es6-crawler-detect`. It logs `I am a user` for ordinary requests and `I am a bot` with request headers for detected crawlers, then renders the Angular page through `ngExpressEngine`.

## Implementation

- **Angular 13** provides the application and component structure.
- **Angular Universal** bootstraps the server application from `AppServerModule`.
- **Express** handles assets, request routing, and the HTTP listener.
- **`es6-crawler-detect`** classifies crawler-like requests from request information.
- **`src/constants.ts`** defines viewer-related constants and crawler-agent entries.

The executable server defaults to **port 4000**, with `PORT` available as an override. Browser and server artifacts are resolved beneath `dist/BotDetection/`.

## Development

Use a Node.js environment compatible with Angular 13, then install dependencies:

```bash
npm ci
npm run dev:ssr
```

`dev:ssr` invokes the Angular Universal development target. The repository also defines `build:ssr`, `serve:ssr`, and `prerender` scripts in [package.json](package.json). `npm start` runs the built server, and `npm test` runs the Jasmine/Karma suite.

After starting the server, compare ordinary browser requests with crawler user-agent requests and inspect the server's classification messages. This demonstrates the integration between server-side request metadata and Angular page rendering.
