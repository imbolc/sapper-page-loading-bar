# Page preloader for Sapper

I believe this component should be included into [sapper-template][]
by default as due to it's AJAX nature page loading looks a bit broken now.

Try to enable "Slow 3G" throttling in Chrome DevTools and follow
a link on a [sapper][]-based site. Choose a link without [prefetch][] attribute
to see the strongest effect. Did it felt broken enough that you've clicked
the link twice or tried another one? :)

To see what exactly went wrong you can disable js and try to follow the same link again.
You'll see:

- toolbar reloading icon turns into a cross
- tab favicon turns into a spinner
- page url will change only after the page loading

Nothing of these happens with enabled js, but instant url change is
probably the most noticeable effect.

A usual way of fixing this is adding some kind of loading indicator.
And here's how to add a top bar - probably the most common type of these
indicators natively existing in mobile browsers.

# Setup

Install the component:

```sh
npm i sapper-page-loading-bar
```

and include it at the top of your `src/routes/_layout.svelte`,
you can also add a transition effect on page loading:

```html
<PageLoadingBar {preloading}/>

{#if !$preloading}
    <main transition:fade>
        <slot></slot>
    </main>
{/if}

<script>
    import { fade } from "svelte/transition"
    import { stores } from "@sapper/app"
    import PageLoadingBar from "sapper-page-loading-bar/PageLoadingBar.svelte"

    const { preloading } = stores()
</script>
```

## Tuning

While `preloading` parameter is required, there's also a few optional of them you
can use to shape the preloader appearance:

- `height` - height of the preloader line
- `color1` and `color2` - its colors


[sapper]: https://sapper.svelte.dev/
[sapper-template]: https://github.com/sveltejs/sapper-template
[prefetch]: https://sapper.svelte.dev/docs#prefetch_href
