# @strait/sdk-node

Server SDK for [Strait](../) — create & manage links and send conversion events
from your backend. Zero dependencies; uses your tenant API key.

## Install

```sh
npm install @strait/sdk-node
```

## Use

```ts
import { StraitClient } from '@strait/sdk-node';

const strait = new StraitClient({
  apiKey: process.env.BRIDGE_API_KEY!,   // bk_live_… from the dashboard
  baseUrl: 'https://go.yourbrand.com',
});

// Create a link
const link = await strait.createLink({
  slug: 'launch',
  longUrl: 'https://yourapp.com/launch',
  tags: ['campaign'],
});

// List / update / delete
await strait.listLinks();
await strait.updateLink('launch', { longUrl: 'https://yourapp.com/launch-v2' });
await strait.deleteLink('launch');

// Send a conversion / revenue event (ties revenue to the funnel)
await strait.sendEvent({ appId: 'YOUR_APP_ID', event: 'purchase', value: 49.99, currency: 'USD' });
```

Failures throw a `StraitError` with `.status` and the parsed `.body`.

## API

| method | endpoint |
|--------|----------|
| `createLink(input)` | `POST /v1/links` |
| `listLinks()` | `GET /v1/links` |
| `updateLink(slug, fields)` | `PATCH /v1/links/:slug` |
| `deleteLink(slug)` | `DELETE /v1/links/:slug` |
| `sendEvent(input)` | `POST /v1/event` |
