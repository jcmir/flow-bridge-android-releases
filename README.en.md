# Flow Bridge Android

[Русский](README.md)

A proprietary third-party Android application for using Google Flow through an embedded GeckoView browser. This repository distributes application binaries and documentation. Application source code is not distributed here.

**Private release preparation: Draft v0.3.0 exists; public release has not been approved.** The selected [distribution repository](https://github.com/jcmir/flow-bridge-android-releases) is being prepared privately.

Features include browsing Google Flow, switching local profiles, selecting files with the Android system picker, and saving supported photos and videos. Successful processing and supported formats also depend on the website.

Requires Android 8.0+ (API 26), arm64-v8a. Version 0.3.0, versionCode 9, package `local.flowbridge.android`, GeckoView 157. No 32-bit ARM or x86 build. The owner reports testing on two Realme phones; broader device compatibility has not been established.

After publication approval, download `FlowBridge-Android-0.3.0.apk` and `SHA256SUMS.txt` from [GitHub Releases](https://github.com/jcmir/flow-bridge-android-releases/releases). A verified public release URL is pending. GitHub source archives do not contain the APK. The project channel referenced in local materials is [ITHRONIC on Telegram](https://t.me/ITHRONIC); availability of build 9 there has not been verified.

Verify the file with `Get-FileHash .\FlowBridge-Android-0.3.0.apk -Algorithm SHA256` on PowerShell, or `sha256sum -c SHA256SUMS.txt` on Linux. Expected APK SHA256:
`de0129a85fd5a73e8c1ff7691bd9f583e7b7c507a0b08506a7402ad72fe1eb51`

Use Android SDK Build Tools: `apksigner verify --verbose --print-certs FlowBridge-Android-0.3.0.apk`. Verification must succeed; the signer certificate SHA256 must be:
`4fe387d417951041c26fe2d296d0e00548d9c38a4f09963c26f4241726e04c94`

Open the verified APK, temporarily allow installation from your chosen source, and install. Update an official build with the same package and signing certificate without uninstalling. Disable the source installation permission afterwards. Older RC builds may have a different certificate or versionCode despite the same version name; do not uninstall or erase data to force an update.

Support: [project Telegram channel](https://t.me/ITHRONIC); public issue links will be added after the new repository is created. Do not submit cookies, credentials, private account content, personal media, or sensitive logs. See [support](SUPPORT.md), [security](SECURITY.md), [privacy status: BLOCKED](PRIVACY.md), [license](LICENSE.md), and [third-party notices](THIRD_PARTY_NOTICES.md).

Flow Bridge is not an official Google product and does not claim affiliation or endorsement. Google determines service availability, account eligibility, and regional restrictions. This application does not guarantee bypassing restrictions or continued third-party service access. Camera capture and directory upload were not added in build 9; an interrupted file selection may need to be repeated.

See [third-party source availability](SOURCE_AVAILABILITY.md). Planned release page after approval: [v0.3.0](https://github.com/jcmir/flow-bridge-android-releases/releases/tag/v0.3.0); this is not a currently available public download.
