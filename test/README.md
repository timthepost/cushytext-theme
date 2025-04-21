# What's This?

A simple way to test the theme build based on what's declared in 
`./mod.ts`, which defines the remote theme properties. Running 
`deno task build` in this directory should result in a successful
build with no broken links. 

## What If There Are Broken Links?

If broken links are reported it's because:

 1. Remote links broke (documentation links on [cushytext.deno.dev](https://cushytext.deno.dev)),
 2. The theme didn't generate correctly.

The files aren't actually 'remotely' loaded; they're just used in-place from 
`src/`, which is the base of the `files[]` array. If they're broken in this test, that
means they're probably broken in `src/` too.

Otherwise, something that the nav links to didn't generate, which shows up on every 
page, and produces a lot of broken links. If you need help figuring out a bug, head 
to our Discord Server.

At some point this and other tests will be automated. 
