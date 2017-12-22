run `ocaml gen.ml` to generate a performance test for bsb

The test involves the generation of DR * DC directories, the
"directory matrix", and each directory contains MR * MC modules,
the "module matrix". The module in row r and column c of the module
matrix depends on all modules in the previous row of the same
directory. The first row of modules in a directory depends on
all modules in the preceding row of directories.


The test setup also permits a lot of parallelism for actually executing
the rules: the modules in the same row can be compiled in parallel,
as well as the directories in the same row.

Every module includes a big comment, so that the size of the files
is not super-small.

To test it

```sh
ocaml unix.cma gen.ml -n 2 test && cd test && time bsb
```

Note to test raw performance, it is recommended to use `bsb.exe`


For Hongbo: `ocaml unix.cma gen.ml -dir-rows 2 -dir-cols 1 -mod-rows 1 -mod-cols 5000 -num-opens 10 test`
