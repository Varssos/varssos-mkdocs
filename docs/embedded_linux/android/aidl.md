# AIDL

AIDL - Android Interface Definition Language

## Links
- [About AIDL](https://developer.android.com/develop/background-work/services/aidl)
- [AIDL overview](https://source.android.com/docs/core/architecture/aidl)
- [Android Code Search](https://cs.android.com/android/platform/superproject/+/android-latest-release:frameworks/native/libs/binder/ndk/include_cpp/android/)
- [binder_manager.h source](https://android.googlesource.com/platform/frameworks/native/+/refs/heads/main/libs/binder/ndk/include_platform/android/binder_manager.h)


## Core info about AIDL

- `calls to an AIDL interface are direct function calls`
- `an implementation of an AIDL interface must be completely thread-safe`
- [AIDL servers must be declared in the VINTF manifest](https://source.android.com/docs/core/architecture/aidl/aidl-hals#writing-server)
- [AIDL clients must declare themselves in the compatibility matrix](https://source.android.com/docs/core/architecture/aidl/aidl-hals#writing-client)
- [SEPolicy for AIDL HALs](https://source.android.com/docs/core/architecture/aidl/aidl-hals#sepolicy)
- [Major AIDL and HIDL differences](https://source.android.com/docs/core/architecture/aidl/aidl-hals#compare-hidl-aidl)




## Useful commands

List all services
```
dumpsys -l
```

Dump service(if it has implemented dump())
```
dumpsys <service_name>
```

Check if service is available
```
service list | grep -i <service name>
```