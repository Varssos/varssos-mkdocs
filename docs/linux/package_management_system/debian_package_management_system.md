# Debian package management system

- [Build binary deb package - practical guide](https://www.internalpointers.com/post/build-binary-deb-package-practical-guide)
- [Debian FAQ - package basics](https://www.debian.org/doc/manuals/debian-faq/pkg-basics.en.html)
- [How to setup a Debian repository](https://wiki.debian.org/DebianRepository/Setup?action=show&redirect=HowToSetupADebianRepository)

## Where is the list of package repository links?

For example if you want to erase a link for package repositories:
```
Err:10 https://packages.cloud.google.com/apt drive Release
```

You can modify the files located here:
```
/etc/apt/sources.list.d
```
