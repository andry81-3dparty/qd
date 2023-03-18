* README_EN.txt
* 2023.03.18
* qd

1. DESCRIPTION
2. SOURCES
3. PATCHES
4. DEPENDENCIES
5. EXTERNALS
6. KNOWN ISSUES
7. AUTHOR

-------------------------------------------------------------------------------
1. DESCRIPTION
-------------------------------------------------------------------------------
`qd` library fork

-------------------------------------------------------------------------------
2. SOURCES
-------------------------------------------------------------------------------
https://www.davidhbailey.com/dhbsoftware/
http://crd-legacy.lbl.gov/~dhbailey/mpdist/
http://crd.lbl.gov/software/applied-mathematics-software/

-------------------------------------------------------------------------------
3. PATCHES
-------------------------------------------------------------------------------
The original library patched to fix these issues:

1. Missed overloading for constructors, operators and functions.
2. Fix trigonometric range before call and after call to triginometric
   functions because of sloppy QD arithmetic outside and inside a function
   call.

-------------------------------------------------------------------------------
4. DEPENDENCIES
-------------------------------------------------------------------------------
`CMakeLists.txt`:

* `tacklelib`

Third-party libraries:

* `qd`

-------------------------------------------------------------------------------
5. EXTERNALS
-------------------------------------------------------------------------------
To checkout externals you must use the
[vcstool](https://github.com/dirk-thomas/vcstool) python module.

NOTE:
  To install the module from the git repository:

  >
  python -m pip install git+https://github.com/dirk-thomas/vcstool

-------------------------------------------------------------------------------
6. KNOWN ISSUES
-------------------------------------------------------------------------------

1. Construction from the int64_t utilizes conversion into the double type
   directly or as is, which means a big value greater than the length of the
   double type mantissa will be truncated to fit the mantissa.

-------------------------------------------------------------------------------
7. AUTHOR
-------------------------------------------------------------------------------
Andrey Dibrov (andry at inbox dot ru)
