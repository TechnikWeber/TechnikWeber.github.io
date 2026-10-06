---
layout: beitrag
title: "Fedora KDE: was nach der Installation zu tun ist"
date: 2026-10-06 09:00:00 +0200
tags: [Linux, Allgemeines]
---

Fedora liefert aus rechtlichen Gründen keine patentbehafteten Codecs und keine
proprietären Treiber mit. Nach der Installation fehlen deshalb ein paar
Handgriffe – hier in der Reihenfolge, in der sie Sinn ergeben.

## Vorweg: warum Fedora KDE und nicht Linux Mint?

Linux Mint ist die übliche Einsteiger-Empfehlung, und das zu Recht: Codecs
sind ab Werk dabei, eine Version wird fünf Jahre gepflegt, es überrascht einen
nichts. Wer genau das will, ist dort richtig. Ich bin trotzdem bei Fedora mit
KDE Plasma gelandet:

- **Aktuelle Hardware läuft einfach.** Fedora 44 steht bei Kernel 7.2 und
  Mesa 26.2. Mint 22 baut auf Ubuntu 24.04 vom April 2024 auf; Mint 23 kommt
  erst im Dezember 2026 und bringt dann Kernel 7.0 und Mesa 25.3.
- **Wayland ist der Normalfall.** Plasma läuft bei Fedora ab Werk auf
  Wayland: Skalierung pro Bildschirm, HDR, variable Bildwiederholrate. Bei
  Cinnamon bleibt X11 auch in Mint 23 die Voreinstellung.
- **Plasma lässt sich einstellen, statt es umzubauen.** Leisten, Kacheln,
  Tastenkürzel, KDE Connect fürs Handy – alles in den Systemeinstellungen.
- **Nah am Original.** Fedora liefert Plasma, Kernel und Treiber weitgehend
  so aus, wie die Projekte sie veröffentlichen. Fehler sind dann meist
  schon woanders gemeldet und gelöst.

Der Preis: alle sechs Monate eine neue Version, jede wird nur rund 13 Monate
gepflegt. Das Upgrade ist ein Klick in Discover, aber es ist eben fällig. Und
die folgende Liste muss man einmal abarbeiten.

Wer noch schwankt: der [LinuxKompass]({% post_url 2026-09-03-linuxkompass %})
fragt nach Hardware und Geduld und begründet seine Empfehlung.

## 1. System aktualisieren

```bash
sudo dnf upgrade --refresh -y
sudo reboot
```

## 2. Firmware aktualisieren

BIOS/UEFI, SSD, Thunderbolt – soweit der Hersteller mitmacht:

```bash
sudo fwupdmgr refresh --force
sudo fwupdmgr get-updates
sudo fwupdmgr update
```

## 3. RPM Fusion einschalten

Die Quelle für Codecs und proprietäre Treiber:

```bash
sudo dnf install \
  https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm \
  https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
sudo dnf update @core
```

Kontrolle – hier darf nichts mit `rawhide` auftauchen, das wäre die
Entwicklerversion und führt zu Abhängigkeitsfehlern:

```bash
dnf repolist --enabled | grep -i rpmfusion
```

## 4. Codecs

Fedoras `ffmpeg-free` gegen das vollständige FFmpeg tauschen und die
GStreamer-Plugins nachziehen:

```bash
sudo dnf swap ffmpeg-free ffmpeg --allowerasing
sudo dnf install @multimedia --setopt="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
sudo reboot
```

Danach spielen Firefox, VLC und Kdenlive H.264, H.265 und AAC.

## 5. Video-Beschleunigung der Grafikkarte

Nur den Block für die eigene Karte ausführen. Welche das ist, zeigt
`lspci | grep -iE "vga|3d"`.

**Intel** (ab etwa 2014):

```bash
sudo dnf install intel-media-driver
```

**AMD:**

```bash
sudo dnf install mesa-va-drivers-freeworld
sudo dnf swap mesa-vulkan-drivers mesa-vulkan-drivers-freeworld
```

**NVIDIA** – erst den Treiber, dann die Brücke zur Video-Beschleunigung:

| Karte | Paket |
|---|---|
| RTX 20xx, GTX 16xx und neuer | `akmod-nvidia` |
| GTX 9xx, GTX 10xx | `akmod-nvidia-580xx` |
| GeForce 600/700 | `akmod-nvidia-470xx` |

```bash
sudo dnf install akmod-nvidia xorg-x11-drv-nvidia-cuda
sudo dnf install libva-nvidia-driver
```

Für ältere Karten in beiden Paketnamen die Endung ergänzen, etwa
`akmod-nvidia-580xx xorg-x11-drv-nvidia-580xx-cuda`. Der aktuelle Treiber
lässt sich auf einer GTX 1060 zwar installieren, endet aber mit schwarzem
Bildschirm.

Nach der Installation **nicht sofort neu starten**: Das Kernelmodul wird im
Hintergrund gebaut, das dauert bis zu fünf Minuten. Fertig ist es, wenn hier
eine Versionsnummer erscheint:

```bash
modinfo -F version nvidia
```

Bei eingeschaltetem Secure Boot muss das Modul zusätzlich signiert werden,
sonst bleibt der Bildschirm ebenfalls schwarz – Anleitung im
[RPM-Fusion-Wiki](https://rpmfusion.org/Howto/Secure%20Boot).

## 6. Flathub ohne Filter

Fedora bringt Flathub mit, zeigt aber nur eine Auswahl. Für alles:

```bash
sudo flatpak remote-modify --no-filter --enable flathub
```

Flathub nicht zusätzlich mit `--user` hinzufügen – sonst steht jede
Anwendung doppelt in Discover.

## 7. Bei Bedarf

**Microsoft-Schriften**, damit Word-Dokumente ihren Umbruch behalten:

```bash
sudo dnf install cabextract xorg-x11-font-utils fontconfig
sudo dnf install https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
```

**OBS Studio** – bei NVIDIA als RPM statt Flatpak, dann funktioniert NVENC
ohne Zusatzpakete:

```bash
sudo dnf install obs-studio
```

**DVDs abspielen** – Rechtslage in Deutschland selbst beurteilen:

```bash
sudo dnf install rpmfusion-free-release-tainted
sudo dnf install libdvdcss
```

**Ältere AppImages**, die mit einem `libfuse.so.2`-Fehler abbrechen:

```bash
sudo dnf install fuse fuse-libs
```

## Stand

Geprüft im Oktober 2026 auf Fedora 44 KDE. Die Befehle enthalten keine
Versionsnummer und gelten ebenso für Fedora 45, das für den 20. Oktober
angekündigt ist. In den ersten Tagen nach einer neuen Version hinkt RPM Fusion
manchmal hinterher – bei „nichts gefunden" einfach zwei Tage später noch
einmal versuchen.
