
Pre-compiled FFmpeg 7.1.2 native binaries for Android, built from source using [ffmpeg-android-maker](https://github.com/Javernaut/ffmpeg-android-maker) with NDK 28.

These binaries are used by **WaEnhancer** for dual-channel call recording — capturing uplink (microphone) and downlink (speaker/earpiece) audio simultaneously and merging them into a single WAV file.

## Supported Architectures

| ABI | Download |
|---|---|
| arm64-v8a | `ffmpeg-arm64-v8a.zip` |
| armeabi-v7a | `ffmpeg-armeabi-v7a.zip` |
| x86 | `ffmpeg-x86.zip` |
| x86_64 | `ffmpeg-x86_64.zip` |

## What's Inside Each ZIP

Each ZIP contains one folder matching the ABI name with:
- `libffmpeg.so` — the standalone FFmpeg executable
- [libavcodec.so](cci:7://file:///tmp/ffmpeg-android-maker/build/ffmpeg/arm64-v8a/lib/libavcodec.so:0:0-0:0), [libavfilter.so](cci:7://file:///tmp/ffmpeg-android-maker/build/ffmpeg/arm64-v8a/lib/libavfilter.so:0:0-0:0), [libavformat.so](cci:7://file:///tmp/ffmpeg-android-maker/build/ffmpeg/arm64-v8a/lib/libavformat.so:0:0-0:0), [libavutil.so](cci:7://file:///tmp/ffmpeg-android-maker/build/ffmpeg/arm64-v8a/lib/libavutil.so:0:0-0:0), [libswresample.so](cci:7://file:///tmp/ffmpeg-android-maker/build/ffmpeg/arm64-v8a/lib/libswresample.so:0:0-0:0), [libswscale.so](cci:7://file:///tmp/ffmpeg-android-maker/build/ffmpeg/arm64-v8a/lib/libswscale.so:0:0-0:0), [libavdevice.so](cci:7://file:///tmp/ffmpeg-android-maker/build/ffmpeg/arm64-v8a/lib/libavdevice.so:0:0-0:0) — shared libraries required at runtime

## How It's Used (WaEnhancer Integration)

1. When the user enables **Call Recording** for the first time, the app detects the device's ABI via `Build.SUPPORTED_ABIS[0]`.
2. It downloads only the matching ZIP (e.g. `ffmpeg-arm64-v8a.zip` for most modern phones).
3. The ZIP is extracted to the app's private internal storage (`getFilesDir()`).
4. `libffmpeg.so` is marked executable via `File.setExecutable(true)`.
5. [CallRecording.java](cci:7://file:///Users/mubasharhussain/Developer/Android%20Projects/WaEnhancer/app/src/main/java/com/wmods/wppenhacer/xposed/features/media/CallRecording.java:0:0-0:0) invokes `Runtime.getRuntime().exec()` with `LD_LIBRARY_PATH` pointed to the extracted folder to merge the two captured PCM streams into a final WAV output.

## Build Info

| Property | Value |
|---|---|
| FFmpeg Version | 7.1.2 |
| NDK Version | 28.2.13676358 |
| Min Android API | 19 |
| Built With | [ffmpeg-android-maker](https://github.com/Javernaut/ffmpeg-android-maker) |
| License | LGPL 2.1 |

## License

The FFmpeg binaries are distributed under the [GNU Lesser General Public License v2.1](https://ffmpeg.org/legal.html). By downloading and using these binaries you agree to comply with the LGPL terms.
