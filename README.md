# @digi4care/astro-google-tagmanager

A seamless integration for injecting Google Tag Manager snippets into Astro projects, supporting popular web analytics tools.

## Installation

To install the package, use npm or yarn:

```bash
npm install @digi4care/astro-google-tagmanager
```

or

```bash
yarn add @digi4care/astro-google-tagmanager
```

## Usage

This package provides components for easily adding Google Tag Manager (GTM) and Site Verification snippets to your Astro project.

### Example

```astro
---
import { GoogleTagmanager, GoogleTagmanagerNoscript, SiteVerification } from '@digi4care/astro-google-tagmanager';
---
<!doctype html>
<html lang="en" dir="ltr">
  <head>
    <SiteVerification id="SITE_VERIFICATION_ID" />
    <GoogleTagmanager id="GTM_MEASUREMENT_ID" domain="https://www.some-custom-domain.com" container="custom-container.js" />
  </head>

  <body>
    <GoogleTagmanagerNoscript id="GTM_MEASUREMENT_ID" domain="https://www.some-custom-domain.com" />
    <slot />
  </body>
</html>
```

### Partytown Example

```astro
---
import { GoogleTagmanagerPartytown, SiteVerification } from '@digi4care/astro-google-tagmanager';
---
<!doctype html>
<html lang="en" dir="ltr">
  <head>
    <SiteVerification id="SITE_VERIFICATION_ID" />
    <GoogleTagmanagerPartytown id="GTM_MEASUREMENT_ID" />
  </head>

  <body>
    <slot />
  </body>
</html>
```

### Notes

- **GoogleTagmanager Component**:

  This component injects the Google Tag Manager script into your Astro project. Pass your GTM measurement ID as the `id` prop. If needed, you can specify a custom domain using the `domain` prop and a custom container path using the `container` prop.

- **GoogleTagmanagerNoscript Component**:

  This component provides a no-script fallback for Google Tag Manager and **must be placed directly after the opening `<body>` tag**. Pass your GTM measurement ID as the `id` prop. You can also specify a custom domain using the `domain` prop.

- **GoogleTagmanagerPartytown Component**:

  This component enables [Partytown](https://partytown.builder.io/) for offloading GTM script execution to a web worker. Pass your GTM measurement ID as the `id` prop.

- **SiteVerification Component**:

  Use this component to add site verification meta tags. Pass your verification ID as the `id` prop. You can also specify the `name` prop to use different site verification names for various vendors.

### Important

- Do **not** use `GoogleTagmanager` and `GoogleTagmanagerNoscript` together with `GoogleTagmanagerPartytown`. If you want to use Partytown, use `GoogleTagmanagerPartytown` with `SiteVerification`, but without the standard `GoogleTagmanager` or `GoogleTagmanagerNoscript` components.
- The `GoogleTagmanagerNoscript` component should always be placed directly after the opening `<body>` tag for correct functionality.

## Props

### GoogleTagmanager

- **id** (string): Your GTM measurement ID.
- **domain** (string): Custom domain for the Google Tag Manager script. Default is `https://www.googletagmanager.com`.
- **container** (string): Custom container path for the Google Tag Manager script. Default is `gtm.js`.

### GoogleTagmanagerNoscript

- **id** (string): Your GTM measurement ID.
- **domain** (string): Custom domain for the Google Tag Manager script. Default is `https://www.googletagmanager.com`.

### GoogleTagmanagerPartytown

- **id** (string): Your GTM measurement ID.

### SiteVerification

- **id** (string): Your site verification ID.
- **name** (string): The name attribute for the meta tag. Default is `google-site-verification`. This allows you to use different site verification names for various vendors.

You can use this component multiple times to verify your site with different services. For example:

- `google-site-verification` for Google.
- `yandex-verification` for Yandex.
- `bing-site-verification` for Bing.
- `pinterest-site-verification` for Pinterest.
- `facebook-domain-verification` for Facebook.
- `baidu-site-verification` for Baidu.
- `apple-site-verification` for Apple.
- `alexaVerifyID` for Alexa.
- `norton-safeweb-site-verification` for Norton Safe Web.
- `twitter-site-verification` for Twitter.
- `linkedin-site-verification` for LinkedIn.
- `adobe-site-verification` for Adobe.
- `mail.ru-verification` for Mail.ru.
- `myspace-site-verification` for MySpace.
- `tumblr-site-verification` for Tumblr.
- `shopify-site-verification` for Shopify.
- `weebly-site-verification` for Weebly.
- `webmaster-site-verification` for Generic Webmaster Tools.
- `whatsapp-site-verification` for WhatsApp Business.
- `stripe-site-verification` for Stripe.

This flexibility makes it easy to add verification for various platforms by using the same component with different `name` and `id` values.
