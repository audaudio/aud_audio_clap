# aud_audio_clap

English | [Deutsch](README.de.md)

CLAP shell of the Audanika Audio Engine over its headless host.

Part of the Audanika Audio Engine; planned in
[aud_audio_pm](https://github.com/audaudio/aud_audio_pm).

## Motivation

An app that plays its sound through the engine wants that sound in a DAW
too. Next to the VST3 and AUv3 shells of the family, this package is meant
to become the CLAP format of the engine over the headless host of
`aud_audio_graph`. Today it holds the native boilerplate the shell will
grow from: a C source built by the build hook and called through
`dart:ffi`.

## Installation

The package is not published to pub.dev; add it as a git dependency:

```yaml
dependencies:
  aud_audio_clap:
    git:
      url: git@github.com:audaudio/aud_audio_clap.git
      tag_pattern: "{{version}}"
    version: ^0.0.3
```

## Usage

The public API is the boilerplate of a native package: `sum` calls the C
function on the main isolate, `sumAsync` the long-running one on a helper
isolate. The example app (`example/lib/main.dart`) shows both results on
screen; the same calls as plain Dart:

```dart
import 'package:aud_audio_clap/aud_audio_clap.dart';

Future<void> main() async {
  print(sum(1, 2));
  print(await sumAsync(3, 4));
}
```

It prints:

```text
3
7
```

## Limitations

- No CLAP plugin yet: the package builds and binds its C source, nothing
  more
- The native code is built by the build hook (`hook/build.dart`) with
  `native_toolchain_c`; on Windows it needs MSVC

## Documentation

- The guides in [doc/guides](doc/guides) and the blog posts in
  [doc/blog](doc/blog)
- The changes per version in [CHANGELOG.md](CHANGELOG.md)

## Status

Before 1.0 - the API may change between minor versions. The package is a
placeholder of the family until the CLAP shell is built.

## Contributing

Tickets run through the `gg` workflow: see the
[Develop Guide](doc/guides/develop-guide.md) and the
[Review Guide](doc/guides/for-ai/ai-review-guide.md).

## License

MIT - see [LICENSE](LICENSE).
