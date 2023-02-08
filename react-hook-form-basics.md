---
date: 07-02-2022
title: Grasping the basics of react-hook-form
tags: ['react', 'forms', 'library']
---
## Background
I've worked fleetingly with react-hook-form before for adding a form to an existing project. But the setting wasn't the best for durable learning; I copied and pasted my way to a working form before the looming deadline.
Now, having dedicated a solid day to exploring the documentation, I think I've built a mental model of the library, its features and the why of using it.

## Introduction
React Hook Form basically centralizes all form-related logic in one hook, `useForm`. The hook returns all the tools you need to wire up the UI to get the form values into react-hook-form, as well as the functions to access those values on change, on blur (clicking out of input), etc.

## Scales Simply
The UI can be as simple as a single input to a complex multi-page wizard with nested components. The `register` function is used for adding the needed callbacks to uncontrolled inputs. More on controlled and uncontrolled inputs later.

## Controlled and Uncontrolled
Uncontrolled inputs have their state handled by the browser outside of react, and the library will use a ref to read the input's value for validation or on submit. Controlled inputs, on the other hand, read their value from state in Javascript. My understanding, today, is that controlled inputs are needed only when the state is needed by some other logic beyond the form (e.g. a live-updating preview for the form values). But I now recall that the `watch` method or hook from react-hook-form gives access to all the form state changes,even in uncontrolled components. Given this, perhaps the main use case for `Controller` or `useContainer` would be when one has to use an input from a component library that doesn't support passing refs and callbacks, the ones coming frmo `register`.

## Optimized
Granular re-renders are the default behaviour of the library. That is for controlled inputs and for `useWatch` and `watch`

## Complex validation logic
Form state can get quite complex and overwhelming very easy. The library allows defining some constraints like `required` declaratively, in the `register` call, but not in the `useForm` parameters. I find that scattering such validation/logic throughout the markup makes making changes to a large form quite frustrating. I get dizzy from scrolling just to find the input I am looking to make a change to.
First-party integration with zod and many other JS parsing/validation libraries, I think, can make the validation decalarative in one place. I haven't tested the limits of that. I know that the zod resolver's equivalent of `required: true` for a text input is `z.string().min(1)`.

