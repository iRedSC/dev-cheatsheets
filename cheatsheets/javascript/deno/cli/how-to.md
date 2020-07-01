# How to

Based on [post](https://medium.com/deno-tutorial/deno-testing-bundling-formatting-and-debugging-9c8aad798fc2).


## Install module

```sh
$ deno install https://deno.land/std/examples/welcome.ts
```

The script will be downloaded to the cache and an executable will be added here as a stub.

- `~/.deno/bin/welcome`
    ```sh
    #!/bin/sh
    # generated by deno install
    deno "run" "https://deno.land/std/examples/welcome.ts" "$@"
    ```

It can be run directly like this:

```sh
$ ~/.deno/bin/welcome
Welcome to Deno 🦕
```

If the `bin` directory is in your `PATH` you can just run:

```sh
$ welcome
Welcome to Deno 🦕
```

## Upgrade Deno version

```sh
$ deno upgrade
```

## Run

### Run local script

Run a script in your project. Use `-A` to allow all permissions.

```sh
$ deno run index.ts
```

### Download and run module

This module will be downloaded from the Deno packages the first time and on subsequent runs it will run quicker as it is already installed in `bin`.

```sh
$ deno run https://deno.land/std/examples/welcome.ts
Welcome to Deno 🦕
```

If you installed it with `deno install URL` or with the `run` command above, it will be stored and can be run directly:

```sh
$ ~/.deno/bin/welcome
```

### Open console

Start Deno in interactive mode.

```sh
$ deno
```

Or

```sh
$ deno repl
```


## Development

### Bundle

Bundle a script.

```sh
$ deno bundle https://deno.land/std/examples/echo_server.ts server.bundle.js
```
```
Bundling https://deno.land/std/examples/echo_server.ts
Emitting bundle to "server.bundle.js"
2.61 KB emitted.
```

Run it.

```sh
$ deno run --allow-net server.bundle.js
```
```
Listening on 0.0.0.0:8080
```

### Format

```sh
$ deno fmt index.ts
```

```sh
$ deno fmt --check PATH
```

### Lint

```sh
$ deno lint PATH
```

### Test

- `test.ts`
    ```javascript
    import { assertEquals } from "https://deno.land/std/testing/asserts.ts";

    Deno.test("deno test", () => {
        const name = "Foo";
        const surname = "Bar";
        const fullname = `${name} ${surname}`;
        assertEquals(fullname, "Foo Bar");
    });
    ```

```sh
$ deno test test.ts
```

Assertions

- `equal`
- `assert`
- `assertEquals`
- `assertStrictEq`
- `assertStrContains`
- `assertMatch`
- `assertArrayContains`
- `assertThrows`
- `assertThrowsAsync`
- `unimplemented`
- `unreachable`


## Debugging

### Browser

Allow browser dev tools debugging by using a flag.

```sh
$ deno --inspect
```

- `--inspect` flag allows attaching a debugger at any point in time,
- `inspect-brk` will wait for debugger breakpoint and pause execution on the first line of code.

### VS Code

- `settings.json`
    ```json
    {
        "version": "0.2.0",
        "configurations": [
            {
            "name": "Deno",
            "type": "node",
            "request": "launch",
            "cwd": "${workspaceFolder}",
            "runtimeExecutable": "deno",
            "runtimeArgs": ["run", "--inspect-brk", "-A", "index.ts"],
            "port": 9229
            }
        ]
    }
    ```
