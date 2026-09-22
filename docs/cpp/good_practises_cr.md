# Good practises and CR checklist

1. [ ] **Complete** — Verify that the code implements the complete design
2. [ ] **#Include** — Verify that #includes are complete
3. **Initialization** — Check variable and parameter initialization:
    - [ ] at program initiation
    - [ ] at start of every loop
    - [ ] at function/procedure entry
4. **Calls** — Check function call formats:
    - [ ] pass by value/reference
    - [ ] parameters
    - [ ] use of "const"
    - [ ] no return of reference to local object
5. **Names** — Check name spelling and use:
    - [ ] is it consistent?
    - [ ] is it within declared scope?
    - [ ] do all structures and classes use '.' reference?
6. **Strings** — Check that all strings:
    - [ ] use std::string class
    - [ ] have valid and appropriate subscripts
    - [ ] use correct member functions and operators
7. **Pointers** — Check that:
    - [ ] pointers are initialized null (0 or NULL)
    - [ ] pointers are deleted only after new
    - [ ] new pointers are always deleted after use
8. **Output Format** — Check the output format:
    - [ ] pass by value/reference
    - [ ] parameters
    - [ ] use of "const"
    - [ ] no return of reference to local object
9. [ ] **{} Pairs** — Ensure that the `{}` are proper and matched
10. [ ] **Logic Operators** — Verify the proper use of `==`, `=`, `||`, every logic function and so on
11. **Line by line check** — Check every LoC for:
    - [ ] instruction syntax
    - [ ] proper punctuation
12. **Standards** — Ensure that the code conforms to the coding standards
13. **File usage** — Verify that all files are:
    - [ ] properly declared
    - [ ] opened (normally at declaration)
    - [ ] closed (often automatic at destruction)
    - [ ] correctly tested for end-of-file, where necessary
14. [ ] Replace magic numbers with enums/const class members
15. [ ] Do not use/try to avoid global variables
16. [ ] Try to avoid `#define`
17. [ ] Use `override` for virtual methods
18. [ ] `static const` should be replaced by `constexpr`
