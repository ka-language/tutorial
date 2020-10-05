# Specific File Access

We already covered private and public fields in prototypes, but sometimes we only want the current file to access the field. In Java, we can use the `protected` keyword to do this. Tusk has a similar concept. Instead of allowing use in the current package (like in java and go), we list the files that have access to the field.

```clojure
;include:
;w test2.omm

;test.omm

var p = proto {
    access ("thisf", "test2.omm", etc...)
    static var protectedfield = fn() {

    }
}

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;test2.omm

var main = fn() {
    log p::protectedfield:()
}
```

(The `"thisf"` is an alias for the current file)

This example works, but if we tried to do something like:

```clojure
;include:
;w test2.omm

;test.omm

var p = proto {
    access ("thisf") ;only allow for this file to use this field
    static var protectedfield = fn() {

    }
}

;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;

;test2.omm

var main = fn() {
    log:(p::protectedfield:())
}
```

The code would panic, because we did not grant access for the "test2.omm" file. If we do not specify an access file, it will assume that every file has access.