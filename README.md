<h1 align="center">
  <!-- Logo -->
  <br/>
  @marko/fastify
	<br/>

  <!-- Language -->
  <a href="http://typescriptlang.org">
    <img src="https://img.shields.io/badge/%3C%2F%3E-typescript-blue.svg" alt="TypeScript"/>
  </a>
  <!-- Format -->
  <a href="https://github.com/prettier/prettier">
    <img src="https://img.shields.io/badge/styled_with-prettier-ff69b4.svg" alt="Styled with prettier"/>
  </a>
  <!-- CI -->
  <a href="https://github.com/marko-js/fastify/actions/workflows/ci.yml">
    <img src="https://github.com/marko-js/fastify/actions/workflows/ci.yml/badge.svg" alt="Build status"/>
  </a>
  <!-- Coverage -->
  <a href="https://codecov.io/gh/marko-js/fastify">
    <img src="https://codecov.io/gh/marko-js/fastify/branch/main/graph/badge.svg?token=KWZ4YNTZVY"/>
  </a>
  <!-- NPM Version -->
  <a href="https://npmjs.org/package/@marko/fastify">
    <img src="https://img.shields.io/npm/v/@marko/fastify.svg" alt="NPM Version"/>
  </a>
  <!-- Downloads -->
  <a href="https://npmjs.org/package/@marko/fastify">
    <img src="https://img.shields.io/npm/dm/@marko/fastify.svg" alt="Downloads"/>
  </a>
</h1>

Render [Marko](https://markojs.com/) templates in a [`Fastify`](https://www.fastify.io/) application.

# Installation

```console
npm install @marko/fastify
```

# Examples

## Setup

```javascript
import fastify from "fastify";
import markoPlugin from "@marko/fastify";
import Template from "./template.marko";

const app = fastify();

app.register(markoPlugin);

app.get("/", (request, reply) => {
  // Streams Marko template into the response.
  // Forwards errors into fa error handler.
  reply.marko(Template, { hello: "world" });
});
```

## $global / out.global

When calling `reply.marko` the [`input.$global`](https://markojs.com/docs/rendering/#global-data) is automatically merged with `app.locals` and `reply.locals` (both added by this plugin). This makes it easy to set some global data via fastify hook or globally, eg:

```js
app.locals.appName = "My App";

app.addHook("onRequest", (request, reply) => {
  reply.locals.locale = "en-US";
});
```

Then later in a template access via:

```marko
<div>${out.global.appName}: ${out.global.locale}</div>
```

# Code of Conduct

This project adheres to the [eBay Code of Conduct](./.github/CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.
