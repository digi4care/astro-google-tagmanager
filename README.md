# @digi4care/astro-google-tagmanager

Astro components for injecting Google Tag Manager (GTM) snippets with built-in **View Transitions / ClientRouter** support. Compatible with **Astro 6+**.

## Installation

```bash
npm install @digi4care/astro-google-tagmanager
```

## Usage

### Basic Example (with `<ClientRouter />`)

```astro
---
import { ClientRouter } from 'astro:transitions';
import {
  GoogleTagmanager,
  GoogleTagmanagerNoscript,
  SiteVerification
} from '@digi4care/astro-google-tagmanager';
---
<!doctype html>
<html lang="en" dir="ltr">
  <head>
    <ClientRouter />
    <SiteVerification id="SITE_VERIFICATION_ID" />
    <GoogleTagmanager id="GTM-XXXXXX" />
  </head>

  <body>
    <GoogleTagmanagerNoscript id="GTM-XXXXXX" />
    <slot />
  </body>
</html>
```

### Self-hosted / Server-side GTM

```astro
<GoogleTagmanager
  id="GTM-XXXXXX"
  domain="https://analytics.yourdomain.com"
  container="custom-container.js"
/>
```

### Partytown (Web Worker)

```astro
---
import {
  GoogleTagmanagerPartytown,
  SiteVerification
} from '@digi4care/astro-google-tagmanager';
---
<!doctype html>
<html lang="en" dir="ltr">
  <head>
    <SiteVerification id="SITE_VERIFICATION_ID" />
    <GoogleTagmanagerPartytown id="GTM-XXXXXX" />
  </head>

  <body>
    <slot />
  </body>
</html>
```

> **Note:** Partytown requires installing `@astrojs/partytown` in your project:
> ```bash
> npx astro add partytown
> ```
> The `GoogleTagmanagerPartytown` component injects the GTM script with `type="text/partytown"`, but the Partytown library itself must be set up separately. Do **not** combine `GoogleTagmanagerPartytown` with `GoogleTagmanager` or `GoogleTagmanagerNoscript`.

## View Transitions / ClientRouter

The `GoogleTagmanager` component automatically handles Astro's client-side navigation:

- On initial page load, the standard GTM snippet fires a `gtm.start` event.
- On each client-side navigation (via `<ClientRouter />`), an `astro:after-swap` listener pushes a **virtual pageview** to the dataLayer:
  ```js
  {
    event: 'virtualPageview',
    'gtm.start': new Date().getTime(),
    virtualPagePath: window.location.pathname,
    virtualPageTitle: document.title
  }
  ```
- A guard prevents duplicate listener registration when the inline script re-executes during transitions.

### Configuring GTM for virtual pageviews

In your GTM container, create a trigger for the `virtualPageview` event and use it to fire your GA4 pageview tag or any other tracking tags. This ensures analytics fire on both full page loads and client-side navigations.

## Props

### GoogleTagmanager

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | GTM container ID (e.g. `GTM-XXXXXX`). **Required.** |
| `domain` | `string` | `https://www.googletagmanager.com` | Custom domain for server-side GTM. |
| `container` | `string` | `gtm.js` | Custom container script path. |

### GoogleTagmanagerNoscript

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | GTM container ID. **Required.** |
| `domain` | `string` | `https://www.googletagmanager.com` | Must match the domain used in `GoogleTagmanager`. |

> **Must** be placed directly after the opening `<body>` tag.

### GoogleTagmanagerPartytown

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | GTM container ID. **Required.** |

### SiteVerification

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `id` | `string` | — | Verification ID. **Required.** |
| `name` | `string` | `google-site-verification` | Meta tag name attribute. |

Supported verification services: Google, Bing, Yandex, Pinterest, Facebook, Baidu, Apple, LinkedIn, and more. Use the same component multiple times with different `name` and `id` values.

## Important

- Do **not** use `GoogleTagmanager` and `GoogleTagmanagerNoscript` together with `GoogleTagmanagerPartytown`. Choose one approach.
- The `GoogleTagmanagerNoscript` component should always be placed directly after the opening `<body>` tag.

## License

MIT
