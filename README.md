This is a build of dnsmasq to target the Ubiquiti Edge Router X.

---

Build this with

```
./dockcross-2 bash
make all
```

The `dockcross-2` binary comes from `dockcross/linux-mipsel`, do
`docker run --rm dockcross/linux-mipsel` to get it.

# TODO

We don't quite match how Ubiquiti built the binary. Notably, these
reported options differ:

**Ubiquiti**

```
DBus
i18n
conntrack
cryptohash
DNSSEC
```

**Ours**

```
no-DBus
no-i18n
no-conntrack
no-cryptohash
no-DNSSEC
```

Unfortunately, it looks like these correspond to various extra
packages that need to be installed, which is hard/annoying.

## Maybe?

We might be able to set `COPTS` to `-DHAVE_DBUS -DHAVE_CONNTRACK
-DHAVE_CRYPTOHASH -DHAVE_DNSSEC` and then build with `make all-i18n`.
