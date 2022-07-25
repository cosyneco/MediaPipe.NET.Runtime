# MediaPipe.NET.Runtime

> Native library package for MediaPipe.NET.

[![Discord](https://img.shields.io/discord/871618277258960896?color=7289DA&label=%20&logo=discord&logoColor=white)](https://go.vignetteapp.org/discord) ![NuGet](https://img.shields.io/nuget/v/MediaPipe.NET.Runtime.CPU) ![NuGet](https://img.shields.io/nuget/v/MediaPipe.NET.Runtime.GPU) ![Deploy workflow](https://github.com/vignetteapp/MediaPipe.NET.Runtime/actions/workflows/deploy-all.yml/badge.svg) ![CI workflow](https://github.com/vignetteapp/MediaPipe.NET.Runtime/actions/workflows/ci.yml/badge.svg)

This is the first half of the port of [MediaPipeUnityPlugin](https://github.com/homuler/MediaPipeUnityPlugin/), in order to use MediaPipe on the latest .NET environment. The goal is to separate the actual C# bindings from the native library into 2 different workflows to increase productivity and efficiency. We think it will drastically improve maintainability as we'll be able to take better advantage of CI and other things like GitHub releases.

We take homuler's Mediapipe C API and building utilities almost completely as-is, use them to build a native Mediapipe library, and ship all libraries for different OSes into one Nuget native runtime package: `Mediapipe.Net.Runtime`.

Since the workflow also generated C# Protobuf sources, we decided to also bundle them in their own Nuget package. This helps separating the source code from an auto-generated one, and also makes more sense when it comes to package releases.

A few key points to note:
- The namespace where all C# Protobuf sources belong is `Mediapipe.Net.Framework.Protobuf`, to match our MediaPipe.NET namespaces.
- On Windows, the name of the native library is `mediapipe_c.dll` rather than `libmediapipe_c.dll` as it makes more sense on Windows and helps avoiding confusion when making bindings to it.
- Since the native library can be shipped in CPU and GPU version, we ship both in their individual Nuget package: `Mediapipe.Net.Runtime.CPU` and `Mediapipe.Net.Runtime.GPU`. Since Mediapipe only supports GPU computation on Linux as of now, it also means that `Mediapipe.Net.Runtime.GPU` only bundles a Linux native library.
- We considerably changed the `build.py` script to adapt for this workflow. For example, some things are not downloaded as they are only relevant in Unity, and options such as `--protobuf` and `--install` have been added to better control the build process.

## Build instructions

Coming soon!

While waiting, you can look at the [MediaPipeUnityPlugin installation guide](https://github.com/homuler/MediaPipeUnityPlugin/wiki/Installation-Guide), as it already gives a very good indication on how to build the native libraries. Most if not every command there will also work here.

You can also check [some of our CI files](https://github.com/vignetteapp/MediaPipe.NET.Runtime/blob/ci/.github/workflows/ci.yml) and look at the commands used for something more accurate but less commented.

## License

This repository is licensed under the MIT license. See [LICENSE](LICENSE) for details.
