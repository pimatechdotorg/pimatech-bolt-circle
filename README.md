# PimaTech Bolt Circle Resolver

Native offline Android calculator for equally spaced, equal-size holes around a complete bolt circle. Version 1.0.0 development preview · Android 8+ · MIT open source.

## Enter what you know

Supply any three of these four values:

- Hole count N (2–360)
- Bolt-circle diameter B
- Common hole diameter d
- Inside edge-to-edge span S between **adjacent** holes

The remaining value is calculated. Supplied inputs are **amber**, with INPUT labels; calculated results are **bright green**, with CALCULATED labels. Missing values have NEEDED labels. Tap a field to edit it; Clear + Save makes it unknown. Solve / inputs can choose the unknown and retain the other available values as supplied inputs. Four supplied values must agree; the app reports conflicts without changing supplied values.

Count plus bolt-circle diameter already determine angular spacing, adjacent center distance and coordinates, even if diameter and gap are unknown. Other underdetermined values remain blank. First-hole angle defaults to 0°; dimensions cannot determine rotation.

## Example from the shop

Six holes, each Ø0.500000 in, with a 2.000000 in inside gap between adjacent edges:

- Bolt-circle diameter: **5.000000 in**
- Adjacent hole-center distance: **2.500000 in**
- Angular spacing: **60°**
- At first-hole angle 0°, Hole 1: **X +2.500000 in, Y 0.000000 in**
- Hole 2: **X +1.250000 in, Y +2.165064 in**

## Coordinates and angles

Zero is at **3 o'clock / +X**. 90° is at **12 o'clock / +Y**. Positive angles and hole numbering increase **counterclockwise**. Coordinates are relative to bolt-circle center; X is right and Y is up.

Tap any hole in the drawing to open its numbered X/Y popup. Previous/Next browses holes, and All coordinates opens a scrolling list. Expand opens a larger drawing. Dense patterns can be selected individually through Coordinates or accessibility actions.

Hole centers and known hole diameters are drawn to scale. If hole diameter is unknown, center markers are illustrative. The marked span is between the nearest edges of Holes 1 and 2 along their line of centers.

## What “span” means

Use the clear **inside gap** between adjacent hole edges, along the line joining their centers. This can be a nominal dimension or an inside-gap result from PimaTech Hole Distance Calculator. Enter it manually; the apps do not exchange data automatically. Do not enter an outside span, center-to-center dimension, or overall width across the pattern. Use actual hole diameters when resolving a measured pattern.

This model assumes equal spacing around 360° and equal-size, round holes with parallel axes. Tangent holes are allowed (zero inside gap); overlapping holes are rejected. Caliper alignment, off-center chords, burrs, chamfers, out-of-roundness and measurement uncertainty affect results. No GD&T true-position assessment, calibration or temperature corrections are provided. Display precision is not measurement accuracy.

## Relationships

Let C be adjacent center distance.

- C = S + d = B sin(180°/N)
- B = (S + d) / sin(180°/N)
- S = B sin(180°/N) − d
- d = B sin(180°/N) − S
- N = 180° / asin((S + d)/B)
- Angular spacing = 360°/N
- Hole i angle = first angle + (i − 1) × 360°/N
- X = (B/2) cos(angle), Y = (B/2) sin(angle)

A calculated count must be a whole number within a numerical threshold; a fractional result is rejected instead of silently choosing a nearby pattern. See `docs/ENGINEERING.md` for the numerical limits and consistency threshold.

## Installation and local behavior

Open the Android APK on your device and allow installation by that browser/file manager if prompted. The app installs separately as `com.pimatech.boltcircle`, label Pimatech Bolt Circle. No Internet permission, accounts, ads, subscriptions or analytics. Values and units save on this device. Changing units preserves physical lengths; first-hole angle and count are unchanged. Backups are disabled.

This is a development preview signed with a development certificate, not a Google Play release. Developer validation does not include physical-device measurement acceptance against calibrated parts.

## Build

JDK 17, Android SDK / Build Tools 35, Gradle 8.9, AGP 8.7.3, Kotlin 2.0.21 and Compose BOM 2024.12.01. Configure SDK location with `ANDROID_HOME` or a local `local.properties`.

```sh
./gradlew :engine:test :app:assembleDebug :app:lintDebug :app:testDebugUnitTest
```

Output: `app/build/outputs/apk/debug/app-debug.apk`. An optional private existing development key can be selected with `-PpimatechDebugKeystore=/absolute/private/path/to/key.keystore`. The signing key is intentionally excluded from the source archive; preserve it privately to sign compatible updates.

Every page and popup displays:

> Proudly made and released open source by PimaTech.org

## Downloads and repository contents

[Android APK](https://github.com/pimatechdotorg/pimatech-bolt-circle/releases/download/v1.0.0-preview/Pimatech-Bolt-Circle-1.0.0-debug.apk) · [Source archive](https://github.com/pimatechdotorg/pimatech-bolt-circle/releases/download/v1.0.0-preview/Pimatech-Bolt-Circle-1.0.0-Source.zip) · [Release notes](https://github.com/pimatechdotorg/pimatech-bolt-circle/releases/tag/v1.0.0-preview)

The complete multi-module source, Gradle wrapper, documentation, test results and native UI proof images are supplied in `Pimatech-Bolt-Circle-1.0.0-Source.zip` at the repository root and as a release asset. Extract that archive to build; the source tree is not expanded in this repository. Private signing keys are excluded.

The owner tested the Android app, confirmed it works as intended, and approved publication. The source archive retains the developer validation record from before owner acceptance.
