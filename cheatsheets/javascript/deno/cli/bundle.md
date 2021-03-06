# Bundle

Bundle a TS or JS module as a single JS file.

This includes import modules, both your scripts and external packages.


## Usage

```
deno bundle [OPTIONS] SOURCE [DESTIONATION]
```


## Limitations

- Deno does not currently support JS minification yet.
- You cannot run the JS script with Node.


## Preview bundle

This does not persist - it just prints.

```sh
$ deno bundle index.ts
```


## Write bundle

```sh
$ deno bundle index.ts build/bundle.js
```

Or if you refer:

```sh
$ deno bundle src/index.ts dist/myApp.bundle.ts
```



## Write and watch bundle

Watch for changes continuously using the `--watch` flag.

```sh
$ deno bundle --unstable --watch index.ts dist/bundle.js
```

This is **unstable**. See [issue](https://github.com/denoland/deno/issues/2401#issuecomment-744563503).


## Bundle a URL

The manual says you pass a URL too, if you want to do that for some reason.

```sh
$ deno bundle https://deno.land/std@0.85.0/examples/colors.ts colors.bundle.js
```


## How to run the bundled file

See more details in the [bundle](https://deno.land/manual/tools/bundler) manual.

### Run with Deno

```sh
$ deno run build/bundle.js
```

### Import in scripts

The output file is an ES module, so you can do imports from it as with JS modules in general.

For example, from the docs:

- `lib.bundle.js`
    ```js
    export { foo } from "./foo.js"; // Note export from another module, without an import.

    export const bar = "bar";
    ```
- `main.js`
    ```js
    import { bar, foo } from "./lib.bundle.js";
    
    foo()
    ```
    
Though, the idea is that the bundle is a single JS file, so perhaps the `foo.js` use above would actually (once compiled) be bundled inside the lib script instead of as a separate file.

### Browser

You might distribute your bundle for others to download and use. Or you might use as part of your own web app.

For example, if you have these in a `public` directory:

- `index.html`
- `main.bundle.js`

Then in your HTML file, you could do:

```html
<script type="module" src="main.bundle.js"></script>
```

Or use in an inline script.

```html
<script type="module">
  import * as website from "main.bundle.js";

  import { fizz } from "buzz.bundle.js";

</script>
```




Note that if you use anything Deno-specific, it won't be recognized.

e.g. `Deno.args`, which is intended for the CLI anyway.
