# AGENTS.md

Guidance for work in this folder. It holds one proprietary vendor binary and its notes; it is a git repository that redistributes the vendor library unmodified (the owner decided to publish it).

## Rules

- `libcastle_v2.so.1.0.0` is proprietary to Hypersecu/Feitian. It is committed here deliberately and unmodified; do not copy it into any other repo, and do not modify it. Other vendor binaries (nCode JAR/DLLs, installers) must still never be committed.
- Never store the token PIN, in this folder or anywhere else. Listing (`pkcs11-tool -L/-O`, `icegate-sign certs`) needs no PIN; do not log in just to look.
- Do not run vendor scripts (`config.sh`, `nssdb.sh`) or the vendor GUI. They were removed on purpose: they edit system files as root.
- Do not pass the library or the token to anything that would expose it on the network.
- Before replacing the library, verify the new download and update `SHA256SUMS`. Check the file's source; the vendor publishes no checksums.

## Facts

- Token: Hypersecu HYP2003 (USB `2ccf:080a`, ePass2003 family, ATR `3b:9f:95:81:31:fe:9f:00:66:46:53:05:10:11:31:71:df:00:00:86:00:00:b5`). The card has `ENTERSAFE-ESPK` (not PKCS#15), so OpenSC cannot use it.
- The library drives the token over USB itself, without pcscd. If it reports "no token", check that nothing else holds the device (Wine token manager, old nCode processes) and that the token is plugged in (`lsusb | grep 2ccf`).
- Consumer: `~/Documents/icegate-sign` (`src/icegate_sign/token.py` has the default path in `VENDOR_MODULE`). If this file moves, update that constant.
- A system-wide reminder lives in `~/AGENTS.md`; update it after changes here.
