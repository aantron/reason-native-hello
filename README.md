<h1 align="center">Reason Native <i>Hello!</i></h1>

<br>

This is the smallest possible Reason Native project that still uses all the
latest tools. Run:

```
git clone https://github.com/aantron/reason-native-hello.git
cd reason-native-hello
npx esy install
npx esy dune exec ./hello.exe
```

<br>

This will print

```
Hello, world!
```

The first time you run this, esy will take several minutes building all the
dependencies. After that, esy will use its cache.

<br>

That's it!

<br>
<br>
<br>

## Explanation

We are using four tools here:

1. [**Reason**][reason] will parse our [`hello.re`][hello.re] file for the
   compiler.
2. The [**OCaml compiler**][ocaml] will translate our parsed `hello.re` into
   native code.
3. [**Dune**][dune] is the OCaml build system. It knows how to call into Reason
   and OCaml in the right way to build our executable. We tell it what we want
   in the [`dune`][dune-file] file:

    ```
    (executable
     (name hello))
    ```

4. [**esy**][esy] is a package manager that is able to download, build, and
   organize all of the above. Hence, [`esy.json`][esy.json] looks like this:

    ```json
    {
      "dependencies": {
        "@opam/dune": "^2.9",
        "@opam/reason": "^3.7.0",
        "ocaml": "^4.12"
      }
    }
    ```

    The `@opam/***` package namespace refers to the [**opam package
    repository**](https://opam.ocaml.org/), which has a lot of useful OCaml
    packages. However, we are not using the opam *tool* &mdash; we are using esy
    itself to connect directly to the opam repository.

    Reason libraries are also [found][npm-reason] in npm. However, many of those
    target JavaScript &mdash; though some target both or only native code.

<br>

## Next steps

- You can make a multi-file project by just creating another `.re` file, for
  example `another.re`:

  ```reason
  let how_are_you =
    "amazing!"
  ```

  You can refer to this value from `hello.re` like this:

  ```reason
  let () =
    print_endline(Another.how_are_you)
  ```

- To depend on a library, say [Dream][dream], tell esy to download it:

  ```json
  {
    "dependencies": {
      "@opam/dream": "*",
      "@opam/dune": "^2.9",
      "@opam/reason": "^3.7.0",
      "ocaml": "^4.12"
    }
  }
  ```

  ...and run `npx esy install`. Then, tell Dune to link it:

  ```
  (executable
   (name hello)
   (libraries dream))
  ```

- If you are using Visual Studio Code, download the [**OCaml Platform**][lsp]
  extension to get syntax highlighting, type hints, etc. Add this to `esy.json`:

  ```json
    "devDependencies": {
      "@opam/ocaml-lsp-server": "*"
    }
  ```

  and re-run `npx esy install`.

- Reason can do a lot more. If you want to do full-stack Reason, meaning
  compile Reason to both native code and JavaScript, get
  [**ReScript**][rescript], which can compile Reason code to JS, and see the
  [Full-stack ReScript][fullstack] example.

<br>

## Contact

Visit the [Reason Discord][discord] and chat with us! Edits/suggestions for this
repo are welcome. Open an issue, PR, or highlight @antron in Discord!

[reason]: https://reasonml.github.io/
[hello.re]: https://github.com/aantron/reason-native-hello/blob/master/hello.re
[ocaml]: https://ocaml.org/
[dune]: https://dune.build/
[dune-file]: https://github.com/aantron/reason-native-hello/blob/master/dune
[esy]: https://esy.sh/
[esy.json]: https://github.com/aantron/reason-native-hello/blob/master/esy.json
[opam]: https://opam.ocaml.org/packages/
[npm-reason]: https://www.npmjs.com/search?q=reason
[dream]: https://github.com/aantron/dream
[discord]: https://discord.gg/Hrz3qKsK
[rescript]: https://rescript-lang.org/
[fullstack]: https://github.com/aantron/dream/tree/master/example/w-fullstack-rescript#files
[lsp]: https://marketplace.visualstudio.com/items?itemName=ocamllabs.ocaml-platform
