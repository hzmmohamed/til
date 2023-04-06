---
date: 12-02-2022
title: Use Cases for react-hook-form Controlled Components
tags: ['react', 'forms', 'library']
---

## What I Learned
One important use case for `Controller` is when you need to replace the `onChange` handler with `setValue` somewhere else in the code. Otherwise, (using `register`), you are stuck with the default behaviour of reading the input value on change.

If you want to do this to add a validation step, you can still use [`register`](https://react-hook-form.com/api/useform/register) and pass `validate` rules.

## The Application
I discovered this insight by studying the dropzone input in [Aether Design System](https://aether.thcl.dev/). Passing the `register` methods to the file input would conflict with [react-dropzone](https://react-dropzone.js.org/)'s callbacks used to handle the input events. So a `Controller` component is used.