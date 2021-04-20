# Basic ESP32 Scaffold

The purpose of this project is to provide a stripped down basic scaffold from which other ESP32 projects can easily be built. It's built specifically to run in VSCode in windows with a custom-compiled rustc that supports the xtensa instruction set, so if you're in linux you'll probably want to use some other project. Probably the one I stole most of this code from.

I stole most of this code from https://github.com/MabezDev/xtensa-rust-quickstart, but it's licensed under apache/MIT so they won't mind.

In order to make this work, we had to do the following:

- compile rust-xtensa fork from scratch per the instructions here: https://github.com/MabezDev/xtensa-rust-quickstart

- set environment variables for this project folder in settings.json (adjust to match your actual paths as needed):
```json
"terminal.integrated.env.windows": {
    "RUSTC": "C:\\rust_code\\rust-xtensa\\build\\x86_64-pc-windows-msvc\\stage2\\bin\\rustc.exe",
    "XARGO_RUST_SRC": "C:\\rust_code\\rust-xtensa\\library\\",
    "CUSTOM_RUSTC": "C:\\rust_code\\rust-xtensa\\build\\x86_64-pc-windows-msvc\\stage2\\bin\\rustc.exe"
}
```
- set the rust-analyzer settings to use xargo and the correct feature flags for the build (you will need to install xargo and adjust the path to match your actual paths as needed):
```json
"rust-analyzer.runnables.overrideCargo": "C:\\rust_code\\rust-xtensa\\build\\x86_64-pc-windows-msvc\\stage1-tools\\x86_64-pc-windows-msvc\\release\\.cargo\\bin\\xargo.exe",
"rust-analyzer.cargo.features": [
    "xtensa-lx-rt/lx6",
    "xtensa-lx/lx6",
    "esp32-hal"
]
```
- flash command :
```powershell
cargo espflash --chip esp32 --speed 115200 --features="xtensa-lx-rt/lx6,xtensa-lx/lx6,esp32-hal" COM#
```
- Alternatively just run `./flash.bat COM#` in the root directory of this project.

- when running the flash command, to get the chip to talk, we had to connect to and then disconnect from the COM port in putty first.

- look into cross-rust-analyzer extension for VSCode? May make it work better than it is now.