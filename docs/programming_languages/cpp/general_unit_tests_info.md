# General info about unittests

## Unit tests

## Mock

Nice [tutorial](https://cpp-polska.pl/post/podstawy-pracy-z-googlemock) about google mocks

Main mock function is to replace external environment for our code.
For example instead of using a Modbus slave device, we use its simulator.

### Fake object

It only imitates the real object's behaviour

### Stub

The only difference between a fake object and a stub is that a stub returns fixed values like:

```cpp
std::string getMessage() const override {
    return "this is stub message";
}
```

### Mock object

Mocks are objects which allow us to define **stubs**
