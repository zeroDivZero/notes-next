# CSR vs SSR

Most React apps use **client-side rendering** (starting React 18 not required). Client downloads html and javascript bundle, browser executes code. When inspecting page source, may not see html of content.

**Server-side rendering** is major Next feature. All page content rendered on server before sending to client. Can be more performant, cached, and better for SEO.

SEO not necessary for all pages. If user needs to be logged in to see specific page, CSR better.
