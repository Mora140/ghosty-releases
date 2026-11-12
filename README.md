# Ghostly phone installer

These files install the Ghostly app on an iPhone without a computer.

Instructions: https://ghostlygps.com/iphone

## The files

- `ghostly-boot-pair.wasm` pairs your iPhone with the installer. You run it in the first terminal app.
- `install.sh` downloads and checks the installer in the second terminal app, then starts it.
- `ghostly-boot-…` is the installer itself. `install.sh` refuses to start it unless its checksum matches exactly.

## Your Apple Account

The installer asks for your Apple Account to sign Ghostly for your iPhone. Your sign-in goes only to Apple.
