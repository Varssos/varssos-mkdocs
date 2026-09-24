# std::optional

Header: `<optional>`

A common use case for optional is the return value of a function that may fail.
If you won't initialize any value for a variable you can use the `value_or()` method instead of creating a special constructor etc.

## Access the contained std::optional\<T\> value without checking if initialized

```cpp
std::optional<int> x {12};
std::cout << *x;
```

## Check whether the std::optional\<T\> object contains a value

- `constexpr explicit operator bool() const noexcept;`
- `constexpr bool has_value() const noexcept;`

Example:

```cpp
// 1st
if( x )
{
    std::cout << "Has value\n";
}

// 2nd
std::cout << x.has_value();
```

## Getting std::optional value

Getting value if not initialized:

```cpp
std::optional<int> o;
std::cout <<   o.value() << '\n';
// Output:
std::bad_optional_access

std::optional<int> o;
std::cout <<   o.value_or(2) << '\n';
// Output:
2
```

Getting value when initialized:

```cpp
std::optional<int> o{13};
// OR: o = 13;
std::cout <<   o.value_or(2) << '\n';
// Output:
13
```
