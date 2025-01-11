# addtoluatexpath


The `addtoluatexpath` package provides a convenient way to add input and Lua package paths to your document.
You may want this package if `.cls` or `.sty` files are located outside of your tex directories (like a network drive or cloud storage drive).

## Usage
* You can either pass the comma-separated paths via package options like `\RequirePackage[path1,path2]{addtoluatexpath}` in pre-amble,
 or by using the macro `\addtoluatexpath{path1,path2}` after the package has been loaded.
* If you wish to include first-level sub-directories as well as a path, inlcude a `/*` at the end of the path.
   eg. `\RequirePackage[C:/Users/me/Desktop/*]{addtoluatexpath}` adds your Desktop and all folders in the desktop to path.
* If you wish to include all nested sub-directories of all levels, include a `/**` at the end of the path.
* If you want to add to Lua path (`package.path`) only, include `notex=true` in the argument.
* If you want to add to tex input path only, include `nolua=true` in the argument, eg. `\RequirePackage[nolua=true, C:/Users/me/Desktop/*, /**]{addtoluatexpath}`.
* If you want to supress a package error that comes up if a directory you try to add does not exist, set `noerror=true`.
* The lua table `addtoluatexpath` is globally defined with the following attributes: 
* `.main(paths_str)` is the main function that runs, `paths_str` is the argument to `\addtoluatexpath` or the package options.
* `.paths = {'.', ...}` is a table containing all paths added by this package
* `.find_file(file_str)` is a function that returns the full path of a file, it searches through all paths that were input to this package and returns the first valid. If no paths are found, an error is issued.
* `.prt_paths()` prints the paths to the log file.



## Notes
This package appends to the `package.path` Lua variable and the `\input@path` command sequence (it first uses `\providecommand` to initialize it).
Lua files in the added paths can then be added via `require'fileinpath1'`; however `loadfile` and `dofile` still require the full path. Caveat: 
`graphicx` internally uses `\input@path` as a default list of the paths;
therefore, paths specified by this package will also include graphics if the `graphicx` package is loaded _after_ paths are set.
However, if `\graphicspath{}` is used after paths are added by this package, graphics search paths will not use `\input@path`, therefore not using the paths you added with this package.

## Dependencies
`luacode`, `luakeys`, `penlight`

## Repo & Contact

* <https://github.com/kalekje/addtoluatexpath>

* [kalekje@gmail.com](mailto:kalekje@gmail.com)


## License

Copyright (C) 2023-2025 Kale Ewasiuk

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF
ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED
TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT
SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR
ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN
ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE
OR OTHER DEALINGS IN THE SOFTWARE.

