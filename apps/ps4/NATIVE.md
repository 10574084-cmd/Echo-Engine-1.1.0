# Native console port (PS4 / OpenOrbis): plan and status

Goal: run Echo Engine as a native program on a jailbroken PS4 (GoldHEN), built with the OpenOrbis toolchain.

1. **Native build without extras** (`-Dnative_lite`): Haxe -> C++ with hxcpp, without Lua, HScript, Discord, videos. Workflow `native.yml`.
2. A minimal Lime/OpenFL app that draws an image on the PS4 (toolchain for hxcpp + SDL2/piglet from OpenOrbis).
3. Audio and gamepad.
4. The full game and its assets inside the PKG.

## Status

- Step 1 done: `native.yml` (Actions > Native build probe) builds Echo Engine as native C++ for Linux with `-Dnative_lite`
  (no Lua, HScript, Discord, videos, crash handler or update check). The web-only online and Echo Live code is guarded for it.
- Step 2 (next): the hard one. Lime's native layer (`lime.ndll`: window, OpenGL ES, input, audio, files) has to be built for the
  PS4 with the OpenOrbis clang, on top of OpenOrbis' SDL2 / piglet ports, plus an hxcpp toolchain file for that target.
  This cannot be tested without a console: every attempt needs an installed PKG and its log (klog).

## Step 2a: graphics test (release "native-test")

`Echo-Engine-native-test-graphics-ps4.pkg` = OpenOrbis' `piglet` sample (OpenGL ES 2 on the PS4) with the Echo Engine icon as
its texture. Built by `ps4-native-test.yml`. If it shows the icon on a console, the graphics side can work.
To read the console log (klog) with GoldHEN: from a PC on the same network run `nc <PS4 IP> 9081`.
