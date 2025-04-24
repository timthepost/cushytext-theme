# CushyText Is A Multi-Purpose Interactive Theme For Lume 3+

Built on top of [Infima CSS][1], Cushy Text is made for text-heavy sites that
need a little bit of interactivity.

By default, Cushy Text is:

- A full-featured blog, complete with tag wiki and individual tag feeds,
- A mini-documentation system with auto-navigation and progress links,
- A simple low-overhead for MDX landing pages with reusable components,
- Complete with search configured out of the box with Pagefind,
- An interactive content-rating system to capture anonymous feedback on your
  posts,
- Multi-instance capable (more than one blog or documentation instance on the
  same url),
- Built with SEO in mind; comes with a comprehensive SEO static analysis plugin
  (AKA Simple SEO),
- Turn-key almost no config deploy, especially on Deno Deploy or a Deno VPS.

While it's built to be a _theme_, it delivers a lot of valuable features that
those working for early-stage technical / technology startups would want. Use it
to create a blog, great landing pages, documentation - all with the ease of MDX
optimized for static sites via SSX.

Cushy brings you all the comforts of Infima, "just enough" interactivity to
connect with your readers, and all the power of Lume 3 with Deno.

## Currently In Alpha Testing - Git Only

This repo is public, and you're welcome to poke around, but it relies on a
bleeding-edge version of Lume that needs nightly updates. Additionally, while I
don't think there will be any breaking changes, there are still some that could
conceivably happen as testing continues.

Have a look at [the main site blog](https://cushytext.deno.dev/blog/) for more
updates!

A week or two after Lume 3 releases (Mid-May 2025), this will become a proper
"template" repo you can use to set up a site quickly, and the theme will be
listed in the Lume Themes Registry for remote / CLI installs.

## Just using the Simple SEO plugin:

Just need the SEO plugin? That's cool! You can pull it right from this repo via jsdelivr and it'll be kept
up-to-date:

```js
import seo from "https://cdn.jsdelivr.net/gh/timthepost/cushytext-theme@latest/src/_plugins/seo/mod.ts";
```

And a bit later on when all other plugins that affect rendered HTML have loaded:

```js
.use(
  seo({
    output: "./_seo_report.json",
    ignore: ["/404.html"],
    lengthUnit: "character",
    lengthLocale: "en",
  }),
)
```

Simple SEO _should_ work okay on Lume 2, as long as the `document` object is present
in the page data layer. There are some rare instances where it might not be present
in some Lume 2 generated pages, which might cause an exception to be thrown, as the 
plugin is written for Lume 3+ where `document` is guaranteed to be present.

[See the full docs for many more configuration options](https://cushytext.deno.dev/docs/theme-plugins/#simple-seo).

Just to show how flexible it is, here's an example of using it for English and Japanese, 
along with the common word set generously contributed by [Rick Cogley](https://github.com/RickCogley):

```ts
import seo from "https://cdn.jsdelivr.net/gh/timthepost/cushytext-theme@latest/src/_plugins/seo/mod.ts";
import { japaneseCommonWords } from "https://cdn.jsdelivr.net/gh/timthepost/cushytext-theme@latest/src/_plugins/seo/japanese_common_words.js";
```

Again, later on, after other plugins that affect rendered HTML are loaded:

```ts
.use(
  seo({
    output: "./_seo_report.json",
    ignore: ["/404.html"],
    lengthUnit: "character",
    lengthLocale: "en",
    ignoreAllButLocale: "en",
    logOperations: false
  }),
)
.use(
  seo({
    output: "./_seo_report_ja.json",
    ignore: ["/404.html"],
    lengthUnit: "word",
    lengthLocale: "ja",
    userCommonWordSet: japaneseCommonWords,
    ignoreAllButLocale: "ja",
    logOperations: false
  }),
)
```

Notice that here one ignores all but English and uses characters as the count
unit, and the other ignores all but Japanese and uses words as the count unit.
See the docs for all of the available options, including how to squelch errors.

[1]: https://infima.dev
