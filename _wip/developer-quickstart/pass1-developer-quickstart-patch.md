# Pass 1 patch — Developer Quick Start

Minimal surgical fixes for the live page at
https://docs.teak.io/user-guide/developer-quickstart.html
(source: `teak-usage/modules/ROOT/pages/developer-quickstart.adoc`). No structural changes.

These three are live bugs — stale links and a wrong label. The pass-2 router rewrite removes
the sections they live in, but these are worth shipping now in case pass 2 takes review cycles.

---

## Fix 1 — Remove stale iOS manual-download links

The `sdks.teakcdn.com` framework/bundle downloads are the legacy manual-install method; the iOS
quickstart now installs via Swift Package Manager / CocoaPods. The bullet already links to the iOS
integration guide, so drop the dead download lines.

**Current:**
> * Be prepared to modify your `Info.plist`.
> * Know how to add dependencies (frameworks, libraries) in Xcode.
> * Download the latest iOS Native SDK
> ** http://sdks.teakcdn.com/ios/Teak.framework.zip
> ** http://sdks.teakcdn.com/ios/TeakResources.bundle.zip
> * For full setup details, see xref:ios::page$integration.adoc[Integrating Teak on Native iOS].

**Replace with:**
> * Be prepared to modify your `Info.plist`.
> * Know how to add dependencies (frameworks, libraries) in Xcode.
> * For full setup details, see xref:ios::page$integration.adoc[Integrating Teak on Native iOS].

---

## Fix 2 — Remove stale Android manual-download link

**Current:**
> * Be prepared to modify your `AndroidManifest.xml`.
> * Know how to add dependencies to your `build.gradle`.
> * Download the latest Android Native SDK
> ** http://sdks.teakcdn.com/android/teak.aar
> * For full setup details, see xref:android::page$integration.adoc[Integrating Teak on Native Android].

**Replace with:**
> * Be prepared to modify your `AndroidManifest.xml`.
> * Know how to add dependencies to your `build.gradle`.
> * For full setup details, see xref:android::page$integration.adoc[Integrating Teak on Native Android].

---

## Fix 3 — Fix the Android link mislabeled "iOS Native Integration"

In "Next Steps," the Native Android link uses the iOS label (copy-paste error).

**Current:**
> 1. **Pick Your Platform** and follow the relevant integration guide:
>    - Unity → xref:unity::page$quickstart/index.adoc[]
>    - Javascript → xref:javascript::page$quickstart/index.adoc[]
>    - Native iOS → xref:ios::page$integration.adoc[iOS Native Integration]
>    - Native Android → xref:android::page$integration.adoc[iOS Native Integration]

**Replace with:**
> 1. **Pick Your Platform** and follow the relevant integration guide:
>    - Unity → xref:unity::page$quickstart/index.adoc[]
>    - Javascript → xref:javascript::page$quickstart/index.adoc[]
>    - Native iOS → xref:ios::page$integration.adoc[iOS Native Integration]
>    - Native Android → xref:android::page$integration.adoc[Android Native Integration]

---

## Flag for eng/SME review

- Confirm the `sdks.teakcdn.com` artifacts are truly deprecated before removing the links. The
  quickstarts install via SPM / CocoaPods / Gradle / UPM, so the manual downloads look legacy — but
  if any customer still relies on direct framework downloads, keep a single pointer instead of removing.
