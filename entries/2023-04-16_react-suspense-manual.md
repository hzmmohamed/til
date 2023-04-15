---
date: 16-04-2023
title: Using React Suspense Without Frameworks or `React.lazy`
tags: ['react']
---

Today, I attempted to add a loading screen to a home page full of image assets. It was a NextJS project, and the first thought that came to mind is using Suspense. And how lucky I was to find [this blog post](https://sergiodxa.com/articles/react/suspense-image-loading) by Sergio Xalambrí on exactly my uncommon use case; it is not a recommended way of using Suspense.

Initially, I skimmed through the general structure implementation, and tried to *guess what the detailed implementation would be*. I got stuck eventually at the point where the Suspense child runs its async function. 

**How does the Suspense Boundary know if the child is ready to render?** It cannot be `async/await`.

Here's the trick-- the child **throws a promise** to tell the Suspense boundary that it's not yet ready to render. Check out the code in Serigo's blog post.