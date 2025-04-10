# CushyText Is A Multi-Purpose Interactive Theme For Lume 3+

Built on top of [Infima CSS][1], Cushy Text is made for text-heavy
sites that need a little bit of interactivity. 

By default, Cushy Text includes 

 - A full-featured blog, complete with tag wiki and individual tag feeds, 
 - A mini-documentation system with auto-navigation and progress links
 - Search configured out of the box via Pagefind
 - An interactive content-rating system to capture anonymous feedback on your 
   posts
 - Turn-key almost no config deploy on Deno Deploy

## Currently In Alpha Testing

This repo is public, and you're welcome to poke around, but it relies on 
a bleeding-edge version of Lume that needs nightly updates. Additionally, 
while I don't think there will be any breaking changes, there are still
some that could conceivably happen as testing continues.

Have a look at [the main site blog](https://cushytext.deno.dev/blog/) for
more updates!

## Just using the "Simple SEO" plugin:

Because a release has now been tagged in, you can use jsdelivr to get
and update the SEO plugin (it's fine to use the plugin without the theme, they're just shipped together):

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

[See the full docs for many more configuration options](https://cushytext.deno.dev/docs/theme-plugins/#simple-seo).

Here's an example of using it for English and Japanese, along with the
common word set contributed by [Rick Cogley](https://github.com/RickCogley):

```js
import seo from "https://cdn.jsdelivr.net/gh/timthepost/cushytext-theme@latest/src/_plugins/seo/mod.ts";
import { japaneseCommonWords } from "https://cdn.jsdelivr.net/gh/timthepost/cushytext-theme@latest/src/_plugins/seo/japanese_common_words.js";
```

Again, later on, after other plugins that affect rendered HTML are loaded:

```
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

Notice that here one ignores all but English and uses characters as the count unit, and 
the other ignores all but Japanese and uses words as the count unit. See the docs for 
all of the available options, including how to squelch errors.

  [1]: https://infima.dev
