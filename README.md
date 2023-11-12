# ReadMe

Templates for use with [ffizer](https://ffizer.github.io/).


## cl-script-project

Usage:

```sh
ffizer apply --source https://github.com/herbertjones/ffizer-templates \
    --source-subfolder cl-script-project \
    --rev main \
    --destination ./my-project \
    -v project=my-project
```

This is a Common Lisp template based on:

* [ocicl](https://github.com/ocicl/ocicl)
* [peru](https://github.com/buildinspace/peru)
* [just](https://github.com/casey/just)
* [sbcl](https://sbcl.org/)

It uses `package-inferred-system` to keep files organized.
Although you can place the code inside the `~/common-lisp/` directory, it is not required thanks to using ocicl and peru.

To use it interactively, just add the directory to your asdf sources.
I happen to use something like this in my interactive .sbcl file:

```lisp
(let ((path #P"/home/herbert/.local/share/ocicl/"))
  (defun initialize-local-source-registry ()
    (asdf:initialize-source-registry
     `(:source-registry
       :ignore-inherited-configuration
       (:directory "/home/herbert/devel/my-project/")          ;; <-- add this
       (:tree ,(merge-pathnames "peru-managed-systems/" path))
       (:tree ,(merge-pathnames "systems/" path)))))
  (cl:export 'initialize-local-source-registry)
  (initialize-local-source-registry))
```

It is already setup to be run as a script with command line argument parsing using [clingon](https://github.com/dnaeon/clingon).
You can also dump an image using the build command.

Testing is setup using [parachute](https://shinmera.github.io/parachute/).
Run the `test` script to run the tests or `(asdf:test-system 'your-system)` when interactivity is setup.

