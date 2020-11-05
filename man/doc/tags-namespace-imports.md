
The `NAMESPACE` also controls which functions from other packages are made available to your package. Only unique directives are saved to the `NAMESPACE` file, so you can repeat them as needed to maintain a close link between the functions where they are needed and the namespace file.

If you are using just a few functions from another package, the recommended option is to note the package name in the `Imports:` field of the `DESCRIPTION` file and call the function(s) explicitly using `::`, e.g., `pkg::fun()`.  Alternatively, though no longer recommended due to its poorer readability, use `@importFrom`, e.g., `@importFrom pgk fun`, and call the function(s) without `::`.

If you are using many functions from another package, use `@import package` to import them all and make available without using `::`.

If you want to add a new method to an S3 generic, import it with `@importFrom pkg generic`.

If you are using S4 you may also need:

* `@importClassesFrom package classa classb ...` to import selected S4 classes.

* `@importMethodsFrom package methoda methodb ...` to import selected S4
  methods.

To import compiled code from another package, use `@useDynLib`

* `@useDynLib package` imports all compiled functions.

* `@useDynLib package routinea routineb` imports selected compiled functions.

* Any `@useDynLib` specification containing a comma, e.g.
  `@useDynLib mypackage, .registration = TRUE` will be inserted as is
  into the the NAMESPACE, e.g. `useDynLib(mypackage, .registration = TRUE)`
