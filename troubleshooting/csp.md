---
title: Content Security Policy
page_title: Content Security Policy
description: Content Security Policy and the Telerik UI for Blazor components suite.
slug: troubleshooting-csp
tags: Content Security Policy,csp,unsafe-eval,eval
published: True
position: 5
---

# Content Security Policy

If a strict `Content-Security-Policy` (CSP) mode is enabled, some browser features are disabled, such as:

* Inline JavaScript, such as `<script></script>` or DOM event attributes like `onclick`, are blocked. All script code must reside in separate files, served from a whitelisted domain.
* Dynamic code evaluation via `eval()` and string arguments for both `setTimeout` and `setInterval` are blocked.
* Fonts and images from Base64 `data:` portions in stylesheets.


## Current Limitations

These limitations can adversely affect the Telerik UI for Blazor components, because they need the following:

* `data:` sources to be allowed for fonts, because that's how the font icons we use are loaded.
* `setTimeout()` is used for animations and `eval()` is used for the chart templates.
* If you use our CDN, you must also allow it as a source for scripts and stylesheets.

>caption Sample CSP rule that ensures the Telerik UI for Blazor components function and look as expected

````HTML
<meta http-equiv="Content-Security-Policy" content="
      script-src 'self' 'unsafe-eval' https://blazor.cdn.telerik.com;
      style-src 'self' 'unsafe-inline' https://blazor.cdn.telerik.com;
      font-src 'self' data:;
      img-src 'self' data:" />
````

>tip If you do not use our CDN services, you can remove their domains. If you do not use the Templates of the Charts, you may also be able to remove `'unsafe-eval'`.

## Upcoming Enhancements

Some of the above-listed limitations will be addressed in a future version of Telerik UI for Blazor. The planned enhancements are:

* Remove the need to specify `unsafe-eval` when [Chart Templates]({%slug components/chart/label-template-format%}) are used.
* Remove the need to specify `unsafe-inline`.
* Remove the need to specify `font-src` rule by detaching font icons.
