
For a function to be usable outside of your package, you must __export__ it. By default roxygen2 doesn't export anything from your package. If you want an object to be publicly available, you must explicitly tag it with `@export`.

Use the following guidelines to decide what to export:

* Functions: export functions that you want to make available. Exported
  functions must be documented, and you must be cautious when changing their
  interface.

* Datasets: all datasets are publicly available. They exist outside of the
  package namespace and should not be exported.

* S3 classes: if you want others to be able to create instances of the class
  `@export` the constructor function.

* S3 generics: the generic is a function so `@export` if you want it to
  be usable outside the package

* S3 methods: every S3 method _must_ be exported, even if the generic is not.
  Otherwise the S3 method table will not be generated correctly and internal
  generics will not find the correct method.

    If you are providing a method for a generic defined in another package,
    you must also import that generic.

* S4 classes: if you want others to be able to extend your class, `@export` it.
  If you want others to create instances of your class, but not extend it,
  `@export` the constructor function, but not the class.

      ```R
      # Can extend and create
      #' @export
      setClass("A")

      # Can extend, but constructor not exported
      #' @export
      B <- setClass("B")

      # Can create, but not extend
      #' @export C
      C <- setClass("C")

      # Can create and extend
      #' @export D
      #' @exportClass D
      D <- setClass("D")
      ```

* S4 generics: `@export` if you want the generic to be publicly usable.

* S4 methods: you only need to `@export` methods for generics that you
  did not define.

* RC classes: the same principles apply as for S4 classes. `@export`
  will only export the class.

### Specialised exports

Generally, roxygen2 can generate the correct namespace directive when `@export`ing a specific object. However, you may want to override the defaults and exercise greater control. In this case you can use the more specialised tags described below:

* `@export foo` generates `export(foo)`
* `@exportClass foo` generates `exportClasses(foo)`
* `@exportMethod foo` generates `exportMethods(foo)`
* `@exportPattern foo` generates `exportPattern(foo)`

For even more specialised cases you can use `@rawNamespace code` which inserts `code` literally into the `NAMESPACE`. If you need to automate this, `@evalNamespace foo()` will evaluate the `foo()` in the package environment and insert the results into `NAMESPACE`. Because `evalNamespace()` is run in the package environment, it can only generate exports, not imports.
