# hyp2003-linux-driver

Vendor PKCS#11 library for the Hypersecu **HYP2003** USB token (Feitian ePass2003 family, `2ccf:080a`) on Linux. OpenSC cannot read this token: its card uses Feitian's `ENTERSAFE-ESPK` layout, not PKCS#15.

| File | What it is |
|---|---|
| `libcastle_v2.so.1.0.0` | Hypersecu's module, unmodified (x86-64, FIPS 140-3 build, 2026-06-30). Needs only glibc and libstdc++. |
| `VENDOR-README.txt` | The vendor's readme from the package. |
| `SHA256SUMS` | Checksum of the library. |

## Install

```sh
git clone https://github.com/quantavil/hyp2003-linux-driver && cd hyp2003-linux-driver
sha256sum -c SHA256SUMS
mkdir -p ~/.local/lib/hyp2003 && cp libcastle_v2.so.1.0.0 ~/.local/lib/hyp2003/
pkcs11-tool --module ~/.local/lib/hyp2003/libcastle_v2.so.1.0.0 -L    # token plugged in; lists "HYP2003"
```

No root and no service. Remove with `rm -r ~/.local/lib/hyp2003`. Do not run the vendor's `config.sh`.

## Use

Any PKCS#11 program can load it as a module path. [icegate-sign](https://github.com/quantavil/icegate-sign) finds `~/.local/lib/hyp2003/` by itself. Listing needs no PIN (certificate and public key are public objects); only signing logs in.

If the token is not found: check `lsusb | grep 2ccf`, that your user can access the USB device, and that no other program holds the token.

## License

Notes: AGPL-3.0-or-later (`LICENSE`). The library and vendor readme belong to Hypersecu/Feitian, are redistributed unmodified, and keep the vendor's own terms. Official download: https://www.hypersecu.com/updates-india
