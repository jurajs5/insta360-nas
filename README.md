# Insta360 NAS

Archivace vybraných videí z Insta360 cloudu na Synology DS916+ (Braswell), DSM 7.2.2 a novější.

Cloud metadata are checked automatically. Video downloads require an explicit file selection and confirmation. The app provides date folders, resumable transfers, 1–5 concurrent downloads, Czech/English, system light/dark themes and DSM administrator session authentication.

## Instalace / Installation

Download the `.spk` from [Releases](https://github.com/jurajs5/insta360-nas/releases), then use DSM **Package Center → Manual Install**. Open Insta360 NAS from the DSM main menu, signed in as a DSM administrator. No separate installation password is required. The app no longer uses port 8765.

## Automatické aktualizace / Automatic updates

Once the first release and GitHub Pages deployment finish, add this source in DSM **Package Center → Settings → Package Sources**:

```
https://jurajs5.github.io/insta360-nas/braswell/index.json
```

Then enable Insta360 NAS under **Settings → Auto-update**. DSM decides when to check and install updates; the application runs without root privileges. If the checkbox is unavailable, automatic installation is not supported by that DSM configuration; the same source can still be used for update detection and the Update button. This delivery pipeline and its catalog are checked locally; real DSM installation and auto-update eligibility must be verified on the NAS.

An update restarts the service. Cloud credentials, settings, manifests and partial downloads are retained. An interrupted video queue requires confirmation to resume.

## Nové verze / Publishing a release

1. Enable **Settings → Pages → Source: GitHub Actions** once.
2. Publish a stable GitHub Release tagged `vMAJOR.MINOR.PATCH` with `Insta360-NAS-DS916-MAJOR.MINOR.PATCH.spk` and its `.sha256` companion. Attach the source ZIP as well.
3. The **Publish DSM update catalog** workflow downloads the latest stable release, validates checksums, package identity, Braswell architecture and package privilege policy, then deploys the package catalog to GitHub Pages.

Draft or prerelease packages are not offered as automatic updates. A failure leaves the previous deployed catalog in place. Publishing new application versions requires building and testing the application; this workflow does not generate application code or promise unattended development.

Application source, tests and modified cloud-client source are included in the release asset `Insta360-NAS-Synology-SPK-zdroje.zip`. The package embeds its runtime and third-party license notices. No personal credentials, session files or video files belong in this repository.

References: [Synology Package Center settings](https://kb.synology.com/en-us/DSM/help/DSM/PkgManApp/configure?version=7), [DSM authentication](https://help.synology.com/developer-guide/integrate_dsm/web_authentication.html), [instapi360](https://github.com/sunsided/instapi360).
