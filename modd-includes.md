# Including Other Files

Omm provides the `include` keyword to use other files

```clojure
;test1.omm
include "test2.omm"
```

```clojure
;test2.omm
var main = fn() {
  log "hello world"
}
```

In addition, Omm automatically puts header guards on the files (header guards just prevent the developer from making an include cycle).

If you want to build the entire directory, you must provide a `main.omm` file. The `main.omm` file will include all of the other files in the directory if you run
```bash
cd /your-directory/
omm *
```

You can also include oat archives inside of omm scripts.

```clojure
include "test.oat"
```

When you include like above, you are including relative to the entry file's directory. Image a project like this:

```
src/
| util/
| | data.omm
| | util.omm
| index.omm
```

In `util.omm`, let's say that we have something like:

```clojure
include "data.omm"
```

This would cause a compile-time error because it would search for it in the `src/` directory instead of the `src/util/` directory. To include relative to the current file, you can surround your quotes in parenthesis:

```clojure
; instead of include "data.omm"
; we can use:
include ("data.omm")
```

This causes no compiler error, and find the "data.omm" file in `src/util/`.

To include from the Omm standard library, you can use backticks
```clojure
include `util/somestdlib.omm`
```
