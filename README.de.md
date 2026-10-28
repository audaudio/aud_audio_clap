# aud_audio_clap

[English](README.md) | Deutsch

CLAP-Shell der Audanika Audio Engine über ihrem Headless Host.

Teil der Audanika Audio Engine; geplant in
[aud_audio_pm](https://github.com/audaudio/aud_audio_pm).

## Motivation

Eine App, die ihren Klang über die Engine spielt, will diesen Klang auch
in einer DAW. Neben den VST3- und AUv3-Shells der Familie soll dieses
Paket das CLAP-Format der Engine über dem Headless Host von
`aud_audio_graph` werden. Heute enthält es das native Grundgerüst, aus dem
die Shell wächst: eine C-Quelle, die der Build-Hook baut und die über
`dart:ffi` aufgerufen wird.

## Installation

Das Paket ist nicht auf pub.dev veröffentlicht; es kommt als
Git-Abhängigkeit dazu:

```yaml
dependencies:
  aud_audio_clap:
    git:
      url: git@github.com:audaudio/aud_audio_clap.git
      tag_pattern: "{{version}}"
    version: ^0.0.3
```

## Verwendung

Die öffentliche API ist das Grundgerüst eines nativen Pakets: `sum` ruft
die C-Funktion auf dem Main-Isolate, `sumAsync` die langlaufende auf
einem Helfer-Isolate. Die Beispiel-App (`example/lib/main.dart`) zeigt
beide Ergebnisse auf dem Bildschirm; dieselben Aufrufe als reines Dart:

```dart
import 'package:aud_audio_clap/aud_audio_clap.dart';

Future<void> main() async {
  print(sum(1, 2));
  print(await sumAsync(3, 4));
}
```

Es gibt aus:

```text
3
7
```

## Grenzen

- Noch kein CLAP-Plugin: Das Paket baut und bindet seine C-Quelle, mehr
  nicht
- Der native Code wird vom Build-Hook (`hook/build.dart`) mit
  `native_toolchain_c` gebaut; unter Windows braucht er MSVC

## Dokumentation

- Die Guides in [doc/guides](doc/guides) und die Blogbeiträge in
  [doc/de/blog](doc/de/blog)
- Die Änderungen je Version in [CHANGELOG.md](CHANGELOG.md)

## Status

Vor 1.0 - die API kann sich zwischen Minor-Versionen ändern. Das Paket
ist ein Platzhalter der Familie, bis die CLAP-Shell gebaut ist.

## Mitwirken

Tickets laufen über den `gg`-Workflow: siehe den
[Develop Guide](doc/guides/develop-guide.md) und den
[Review Guide](doc/guides/for-ai/ai-review-guide.md).

## Lizenz

MIT - siehe [LICENSE](LICENSE).
