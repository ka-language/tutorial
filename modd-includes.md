# Including Other Files

Tusk provides the `;include:` prefix to use other files

```clojure
;include:
;r test.omm
;w test.omm
;s ommstd/json

;the rest of the test.tusk file
```

The `;include:` prefix tells the compiler to link the files listed at compile time. The `r`, `w`, and `s` are location identifiers.

`r` includes relative to the current file
`w` includes relative to the working directory
`s` includes from the tusk installation folder (standard library)