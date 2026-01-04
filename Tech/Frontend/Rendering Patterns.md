**1. Static Website**
- All webpages are static files and  upload them to a storage somewhere in the cloud. (Amazon S3)
- Hugo, Jekyll, or 11ty
	- can build them programmatically
- Best for websites without interactivity
**2. Multi-page Applications**
- HTML and Data are put together on the server whenever a request is made on the browser.
- Sample is Amazon, whenever we click a link, data changes.
- Django, Ruby on Rails, or Laravel.
**3. Single Page Application**
- Angular and React
- UI rendering happens on the browser.
- Start with an HTML page as a shell, and use JS to render UI and to fetch data using http requests.
- Requires a huge JS bundle, which can make the first loading slow.
- Some Search Engines can have a hard time understanding the content on the dynamic route, problem if we want good SEO.
**4. SSR (Server Side Rendering) with [[Hydration]]**
- Render initial page on the server.
- Hydrate or render all other pages on the client with JS.
- MPA + SPA = SSR
- Next, Nuxt, Svelte, etc. (Meta frameworks)
- Cons: Needs an actual server.
**5. SSG (Static Site Generation**
- Prerender in the server, and upload on a static host like a storage bucket.
- Hydrate with JS after initial load.
- Jamstack (Next, Nuxt, Svelte)
**6. ISR (Incremental Static Regeneration**)
- Started with Next
- Deploy a static site, and rebuild individual pages on the server when the cache is invalidated.
- Complex to self host.
**7. Partial Hydration**
- Render stuff on the top, and when scrolling, load below.
- Lazy load.
**8. Islands**
- When hydrating, JS takeovers the entire page.
- Start with static HTML, and use JS to hydrate interactive components.
- Astro.
**9. Streaming SSR**
- Next 13 - App directory
	- Thanks to building blocks such as React server components.
- Render server-side contents in concurrently in multiple chunks, instead of one.
- UI becomes interactive faster, and feels smooth to user.
**10. Resumability**
- qwik
- All of its data, even like JS event listeners are serialized into HTML.
- Code is broken into tons of tiny chunks.
- Initial load is always static HTML, no hydration needed.
- Any interactivity with JS is lazy loaded in the background.