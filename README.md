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
    <SiteVerification id="GTM_VERIFICATION_ID" />
    <GoogleTagmanager id="GTM_MEASUREMENT_ID" partytown={false} domain="https://www.some-custom-domain-is-also-supported.com" container="custom-container-path-is-also-supported.js" />
  </head>

  <body>
    <GoogleTagmanagerNoscript id="GTM_MEASUREMENT_ID" domain="https://www.some-custom-domain-is-also-supported.com" />
    <slot />
  </body>
</html>
```

### Notes

- **GoogleTagmanager Component**: This component injects the Google Tag Manager script into your Astro project. Pass your GTM measurement ID as the `id` prop. If needed, you can specify a custom domain using the domain prop and a custom container path using the container prop.
- **GoogleTagmanagerNoscript Component**: This component provides a no-script fallback for Google Tag Manager. Note that there is no `partytown` support for this component.
- **SiteVerification Component**: Use this component to add site verification meta tags. Pass your verification ID as the `id` prop. You can also specify the `name` prop to use different site verification names for various vendors.

### Important

Be aware that the `GoogleTagmanagerNoscript` component does not support `partytown`. Do not use it if you want to enable `partytown`.

## Props

### GoogleTagmanager

- **id** (string): Your GTM measurement ID.
- **partytown** (boolean): Enable or disable partytown. Default is `false`.
- **domain** (string): Custom domain for the Google Tag Manager script. Default is `https://www.googletagmanager.com`.
- **container** (string): Custom container path for the Google Tag Manager script. Default is `gtm.js`.

### GoogleTagmanagerNoscript

- **id** (string): Your GTM measurement ID.
- **domain** (string): Custom domain for the Google Tag Manager script. Default is `https://www.googletagmanager.com`.

### SiteVerification

- **id** (string): Your site verification ID.
- **name** (string): The name attribute for the meta tag. Default is `google-site-verification`. This allows you to use different site verification names for various vendors.

```astro
---
export interface Props {
  name?: string;
  id?: string;
}
const { id, name = "google-site-verification" } = Astro.props;
---

{id && <meta name={name} content={id} />}
```

## License

This project is licensed under the MIT License.
