# gravitationalWAVS - Projekthandbuch

![Titel](images/title.png)

## TLDR

**gravitationalWAVS** ist eine interaktive 3D-Audio-Installation zur psychoakustischen und dokumentarischen Vermittlung von Gravitationswellen in Museums- und Wissenschaftskontexten. Über einen kabellosen, sputnik-inspirierten Haptik-Controller (ESP32/IMU via OSC) steuern Rezipient*innen die Orbits zweier gekoppelter Schwarzer Löcher sowie eine Shepard-Ton-Kreiselbewegung in einem 3D-Klangfeld, während historische und erklärende Sprachsamples als räumlich fixierte Ankerpunkte dienen. Das System wird vollständig als autarke Standalone-Applikation in Max 9 mit IRCAM SPAT5 (Higher Order Ambisonics) umgesetzt, wobei mathematische Trägheitsfilter (Inertia) eine spürbare Illusion von physischer Masse im Raum erzeugen.

## Inhaltsverzeichnis

- [TLDR](#tldr)
- [Konzept](#konzept)
- [Wissenschaftliche & Technische Beratung](#wissenschaftliche--technische-beratung)
- [Arbeitspakete](#arbeitspakete)
- [Zeitplanung & Workload](#zeitplanung--workload)
- [Ressourcenplanung](#ressourcenplanung)
  - [Materialien & Software-Lizenzen](#materialien--software-lizenzen)
  - [Räume](#räume)
  - [Literatur und Recherche](#literatur-und-recherche)
- [Chancen und Risiken](#chancen-und-risiken)
- [Erwarteter Kompetenzgewinn](#erwarteter-kompetenzgewinn)
- [Software](#software)
- [Hardware](#hardware)
- [Werbung](#werbung)

---

## Konzept

Das Ziel des Projekts **GRAVITATIONAL WAVs** ist es, ein fundamentales Phänomen des Universums – die 2015 erstmals gemessenen Gravitationswellen – interaktiv, haptisch und psychoakustisch greifbar zu machen. Wenn massereiche Objekte wie Schwarze Löcher oder Neutronensterne kollidieren, stauchen und dehnen sie die Raumzeit.

<figure>
  <img src="images/wave.gif" alt="Zweidimensionale Betrachtung von Gravitationswellen, die von zwei einander umkreisenden Neutronensternen ausgesandt werden" />
  <br>
  <figcaption><i>Zweidimensionale Betrachtung von Gravitationswellen, die von zwei einander umkreisenden Neutronensternen ausgesandt werden</i></figcaption>
</figure>

In der Installation wird dieses Prinzip in ein dreidimensionales Klangfeld übersetzt, das dokumentarische Erzählung und physikalische Simulation miteinander verbindet:

1. **Cosmic Microwave Background (CMB):** Ein fundamentales, waberndes Hintergrundrauschen repräsentiert die kosmische Mikrowellen-Hintergrundstrahlung. [Audiobeispiel online](https://www.youtube.com/watch?v=gJJmFnMea1Q)

<figure>
  <img src="images/Planck_CMB_orig.jpg" alt="Kosmische Mikrowellen-Hintergrundstrahlung bildlich dargestellt" />
  <br>
  <figcaption><i>Kosmische Mikrowellen-Hintergrundstrahlung</i></figcaption>
</figure>

2. **Binary Black Hole System & Shepard-Kreiselbewegung:** Zwei gekoppelte Soundobjekte simulieren zwei einander umkreisende Schwarze Löcher. Die kontinuierliche Beschleunigung und Annäherung (Inspiral) wird durch eine psychoakustische Shepard-Ton-Synthese als endlose Kreiselbewegung abgebildet.

3. **Testpartikel-Ring:** Ein virtueller Ring aus Soundquellen macht die Polarisation ($h_+$ und $h_\times$) der Raumzeit-Dehnung auditiv erfahrbar.

<figure>
  <img src="images/GravitationalWave_CrossPolarization.gif" />
  <br>
  <figcaption><i>Der Effekt von kreuzpolarisierten Gravitationswellen auf einen Partikelring.</i></figcaption>
</figure>
<br>

4. **Dokumentarische Ebene & Fixierte Sprach-Anker:** Authentische Sprachsamples (wie LIGO-Entdeckungszitate) und erklärende Erzählstränge vermitteln den wissenschaftlichen Kontext im dokumentarischen Stil. Um die räumliche Orientierung zu wahren, bleiben diese Stimmen an festen Positionen im Raum verankert, während sie durch die bewegten, hardwaregesteuerten Audioeffekte dramaturgisch untermalt werden.

5. **Interaktiver Controller & Trägheits-Engine:** Über ein physisches Objekt mit Gyroskop greifen die Zuhörer direkt in das System ein. Über mathematische Trägheitsfilter (Inertia) besitzen die Schwarzen Löcher eine spürbare Masse: Bei einer plötzlichen Richtungsänderung fliegt das System organisch weiter und dreht zeitverzögert ab. Es entsteht eine haptische Illusion von Masse im Raum.

---

## Wissenschaftliche & Technische Beratung

Im Rahmen der Konzeption und technischen Evaluation wurden Expertenkonsultationen durchgeführt, um die optimale Architektur für Barrierefreiheit, Performance und Weitergabe an Hochschulen und Museen zu bestimmen:

- **Gespräch mit Prof. Frank Melchior:**  
  Prof. Melchior betonte die Wichtigkeit einer direkten, kohärenten Raumklang-Engine für wissenschaftliche und künstlerische Exponate. Er bekräftigte die Empfehlung, auf eine native Aufbereitung in Max mit IRCAM SPAT5 zu setzen, um eine präzise psychoakustische Kontrolle über Higher Order Ambisonics (HOA) zu gewährleisten.

- **Austausch mit Eric Raynaud (aka Fraction, Entwickler von XP4Live):**  
  Im direkten Austausch riet Raynaud explizit davon ab, sein eigenes Produkt *XP4Live* oder DAW-Infrastrukturen als Zwischenschicht für dieses spezifische Vorhaben zu nutzen. Er empfahl nachdrücklich, SPAT5 direkt nativ in der Max-Umgebung anzusteuern, da dies maximale Flexibilität, niedrigste Latenzen und vollständige Unabhängigkeit von Drittanbieter-Plugins bietet.

Auf Basis dieser Expertenratschläge wurde die Minimal-Fallback-Lösung (Ableton Live + M4L/XP4L) verworfen und die **reine Max 9 Standalone-Architektur** als Hauptpfad definiert.

---

## Arbeitspakete

Das Projekt gliedert sich in folgende Arbeitspakete (AP), die weitgehend iterativ und nebenläufig entwickelt werden:

### AP0: Konzeption, Recherche & Projektdefinition

- Anforderungsanalyse, Systemarchitektur-Entwurf und Festlegung der Schnittstellen.
- Recherche zu Spatial-Audio-Formaten (HOA), Sensorik (IMU-Fusion) und physikalischen Modellierungsgrundlagen.

### AP1: Hardware-Prototyping & Sensorik (Embedded & Physical Computing)

- Gehäuseentwicklung im Sputnik/Vanguard-Look (CAD, 3D-Druck mit PLA).
- Schaltungsentwurf, LiPo-Lademanagement & Löt-Assembly (Seeed Studio XIAO ESP32-C6 + Adafruit BNO085 IMU).
- Firmware-Entwicklung (C++/Arduino): Sensor-Fusion, Kalibrierung & Low-Latency OSC-Streaming via Wi-Fi.

### AP2: Max 9 Systemarchitektur & Mathematik (Inertia Engine)

- Aufbau des Max 9 Standalone-Frameworks & OSC-Parsing.
- **Inertia-Engine in JavaScript:** Programmierung der mathematischen Trägheitsberechnung, Beschleunigung, Impulserhaltung und gekoppelter Kepler-Bahnen.
- Entwurf der interaktiven Benutzeroberfläche (UI) für Monitoring, Kalibrierung und Perspektivsteuerung.

### AP3: Spatial Audio & IRCAM SPAT5 Integration (Higher Order Ambisonics)

- Einbindung und Konfiguration von IRCAM SPAT5 für Higher Order Ambisonics (HOA).
- Implementierung dynamischer Raumtrajektorien (Orbits, Distanz-Attenuations-Filter) im Kontrast zu räumlich fixierten Anker-Positionen für die Sprachebene.
- Audio-Routing via Dante Virtual Soundcard zur flexiblen Ansteuerung von Mehrkanalsystemen (z. B. 7.1.4 Studio-Array).

### AP4: Dokumentarisches Storytelling & Sprachsamples

- Recherche, Auswahl und Aufbereitung historischer Original-Zitate (z. B. LIGO-Entdeckung) sowie Erstellung erklärender Erzähltexte.
- Dramaturgische Strukturierung des dokumentarischen Erzählstrangs und Einbettung in einen Sample-Player innerhalb von Max 9.
- Spektrale Anpassung und dynamisches Pegel-Management (Sidechain-Ducking), um die Sprachverständlichkeit gegenüber den bewegten Raumzeit-Effekten sicherzustellen.

### AP5: Sounddesign & Synthese

- Klangsynthese in Max (FM-, Granular-, 80s-Synth- und Rauschsynthese für CMB, Schwarze Löcher und Partikelring).
- Implementierung der **Shepard-Ton-Synthese** zur psychoakustischen Abbildung der endlosen Kreisel- und Annäherungsbewegung (Inspiral).
- Erstellung psychoakustischer Modulations-Patterns gekoppelt an die physikalischen Raumzeit-Parameter.

### AP6: Integration, Labor-Einmessen & Usability-Testing

- Testläufe und akustisches Einmessen im 3D-Audio-Labor der Fachhochschule.
- Haptik- und Usability-Tests mit Testpersonen zur Verifikation der kontinuierlichen Raumtrajektorien, Trägheitsillusion und Sprachverständlichkeit.

### AP7: Dokumentation, Open-Source-Release & Exponat-Aufbereitung

- Erstellung des Projekthandbuchs, technische Dokumentation.
- Vorbereitung auf die Projektschau/Vernissage und wissenschaftliche und museale Weiterverwendung.

---

## Zeitplanung & Workload

### Sprint- & Workload-Matrix

| Phase / Fokus | Parallele Haupt-Aktivitäten | Workload |
| :--- | :--- | :--- |
| **Vorarbeitung & Konzeption** | • **AP0:** Systemarchitektur, Hardware-Recherche & Anforderungsanalyse | 40 h |
| **Sprint 1: Core Systems & Firmware** | • **AP1:** Hardware-Layout, Gehäuse-3D-Druck & ESP32-Firmware<br>• **AP2:** Max 9 Framework, OSC-Parsing & JS-Kepler-Prototyp | 72 h |
| **Sprint 2: Physics & Spatial Core** | • **AP2:** Mathe-Verfeinerung (Inertia Engine) & UI-Design<br>• **AP3:** SPAT5-HOA-Decoder, Orbit-Mapping & Sprach-Ankerpunkte | 48 h |
| **Sprint 3: Audio Synthesis & Storytelling** | • **AP3:** Dante DVS Multi-Channel Setup<br>• **AP4:** Sprachsample-Schnitt, Dramaturgie & Ducking-Routing<br>• **AP5:** DSP-Synthese (CMB, Shepard-Ton & Black-Hole-Palette) | 48 h |
| **Sprint 4: Integration & Lab Testing** | • **AP5:** Partikel-Polarisation & Parameter-Kopplung<br>• **AP6:** Erste Einmessungen & Haptik-Fieldtests im 3D-Audio-Labor | 24 h |
| **Sprint 5: Polishing & Deployment** | • **AP6:** Raumakustischer Feinschliff & Usability-Evaluation<br>• **AP7:** Standalone-Export, Projekthandbuch & Open-Source-Prep | 48 h |
| **Gesamt** | **Iterative Entwicklung über alle Arbeitspakete (AP0–AP7)** | **280 h** |

---

#### Agiles Gantt-Diagramm

```mermaid
%%{init: {
  'gantt': {
    'useWidth': 1200,
    'leftPadding': 220,
    'rightPadding': 50,
    'tickInterval': '1w'
  }
}}%%
gantt
    dateFormat YYYY-MM-DD
    axisFormat KW %V

    section Vorbereitung & Sprint 0
    AP0 - Konzeption & Recherche              :2026-09-19, 2026-10-25
    AP0 - Recherche (Live-Systeme besuchen)   :2026-11-11, 2026-12-01
    Sprint - Konzeption & Pitch               :crit, 2026-09-28, 2026-10-03
    Sprint - Projekthandbuch                  :crit, 2026-10-19, 2026-10-30
    Sprint - Projekthandbuch                  :crit, 2026-11-12, 2026-11-16

    section Sprint 1 & 2 (Hardware & Core)
    AP1 - Hardware & Firmware                 :active, 2026-10-24, 2026-12-01
    Sprint 1 - Review (Core & FW)             :crit, 2026-11-22, 2026-12-01
    AP2 - Max 9 & JS-Inertia                  :active, 2026-10-24, 2026-12-20
    Sprint 2 - Review (Physics)               :crit, 2026-12-07, 2026-12-13

    section Sprint 3 & 4 (Audio & Lab)
    AP3 - Spatial Audio / SPAT5               :2026-11-25, 2027-01-03
    AP4 - Storytelling & Sprachsamples        :2026-11-25, 2026-12-27
    AP5 - Sounddesign & Synthese              :2026-11-25, 2027-01-03
    Sprint 3 - Review (Synthesis)             :crit, 2026-12-28, 2027-01-03
    AP6 - Lab-Tests & Polishing               :2026-12-13, 2027-01-10
    Sprint 4 - First Lab Test                 :crit, 2026-12-14, 2026-12-18
    Sprint 4 - Review (Lab Test)              :crit, 2027-01-04, 2027-01-10

    section Sprint 5 (Release)
    AP7 - Doku & Deployment                   :2027-01-11, 2027-01-19
    Sprint 5 - Review & Release               :crit, 2027-01-11, 2027-01-19
```

---

## Ressourcenplanung

### Materialien & Software-Lizenzen

| Benötigte Ressourcen | Begründung | Kosten |
| --- | --- | --- |
| Seeed Studio XIAO ESP32-C6 | Controllerboard (Wi-Fi 6, BLE 5.3) | 18,44 € |
| Adafruit 9-DOF IMU Fusion Breakout (BNO085) | Orientierungssensorik (Quaternions, Gyro) | 38,40 € |
| LiPo-Akku 3,7 V, 1200 mAh | Stromversorgung des Hand-Controllers | 14,11 € |
| ELEGOO Matte PLA Filament (Schiefergrau, 1kg) | 3D-Druck des Sputnik/Vanguard-Gehäuses | 19,15 € |
| Audinate Dante Virtual Soundcard | Multi-Channel Audio-Routing auf Betriebssystem-Ebene | 50,00 € |
| Cycling '74 Max 9 Lizenz | Entwicklungs- und Standalone-Export-Plattform | 199,00 € |
| **Gesamtsumme** | | **339,10 €** |

### Räume

| Raum | Zweck | Verfügbarkeit |
| --- | --- | --- |
| 3D-Audio-Labor (USTP) | Einmessen des HOA-Setups, Spatial Audio Testing (7.1.4 Array) | Nach Vereinbarung |
| Makerlab / Werkstatt | Lötarbeiten, 3D-Druck, Montage des Controllers | Jederzeit |

### Literatur und Recherche

| Quelle | Thema | Verfügbarkeit |
| :--- | :--- | :--- |
| Brian Clegg: *Gravitational Waves* | Wissenschaftliche Grundlagen der Raumzeit-Wellen | Fachliteratur / Privat |
| Misner, Thorne, Wheeler: *Gravitation* | Das Standardwerk für die Grundlagen der Gravitation und Raumzeit-Wellen | Fachliteratur / Privat |
| Roger N. Shepard: *Circularity in Judgments of Relative Pitch* | Psychoakustische Grundlagen der Shepard-Ton-Illusion | Fachartikel / Online |
| LIGO Open Science Center / Caltech Archiv | Original-Tondokumente und sonifizierte Gravitationswellen-Ereignisse (GW150914) | Online / Open Access |
| Project Vanguard & Sputnik Dokumentation | Historische Design- und Konstruktionsreferenzen | Archivmaterial |
| IRCAM SPAT5 Dokumentation | Higher Order Ambisonics & Perceptual Spatialization | Online / Open Source |
| Besuch Technisches Museum Wien | Interaktive Exponat-Gestaltung & Vermittlungskonzepte | Vor Ort |
| Besuch Live-Systeme (Weltraum System Ars Electronica Center Linz) | Analyse von räumlicher Akustik und Live-Setups | Vor Ort |

### Inspiration

| Referenz / Quelle | Kernelement | Übertragung in *gravitationalWAVS* |
| :--- | :--- | :--- |
| **Public Service Broadcasting** – *Go!* ([YouTube](https://www.youtube.com/watch?v=an-9JHTpiLA)) & LIGO-Archiv (*„We did it“*, David Reitze) | Einbettung historischer Original-Zitate in musikalische Strukturen | Nutzung authentischer Sprachsamples als räumlich fixierte Ankerpunkte im Klangfeld |
| **Public Service Broadcasting** – Alben *The Race for Space* & *Sputnik / Korolev* | Kombination aus historischer Raumfahrt-Dokumentation, Funkverkehr und elektronischer Musik | Ästhetisches Vorbild für das Sputnik-Controller-Design und den dokumentarischen Erzählstil |
| **Shepard-Ton-Illusion** (Roger Shepard) | Psychoakustische Tonleiter mit endlos steigender oder fallender Tonhöhe | Klangliche Übersetzung der endlosen Kreisel- und Annäherungsbewegung (Inspiral) der Schwarzen Löcher |
| **The Eagles** – *Journey of the Sorcerer* (*Per Anhalter durch die Galaxis* Intro) | Markante, kosmisch anmutende 80er-Synthesizer-Ästhetik | Klangfarbliche Inspiration für synthetische Texturen und retro-futuristische Raumfahrt-Atmosphäre |
| **Räumliche Dramaturgie & Sprecher-Fokus** | Trennung zwischen statischer Erzählebene und dynamischer Effekt-Umgebung | Fixierung erklärender Stimmen im Raum, während Trägheit (Inertia) und Raumzeit-Verzerrungen um sie herum rotieren |

---

## Chancen und Risiken

- **Chance (Hohe Portabilität):** Durch die reine Max 9 Standalone-Architektur und Dante-Unterstützung kann das System ohne Software-Lizenzen an Museen und Universitäten weitergegeben werden.
- **Risiko (Latency & Wi-Fi-Dropouts):** Latenzen bei der OSC-Übertragung könnten das Gefühl der direkten Kontrolle beeinträchtigen. *Mitigation:* Verwendung des XIAO ESP32-C6 mit Wi-Fi 6 / 5 GHz sowie lokale Interpolationsfilter in JavaScript **[AP1/AP2]**.
- **Risiko (Psychoakustische Unschärfe):** Unnatürliche Lautsprechersprünge im Raum bei Orbits. *Mitigation:* Nutzung von Higher Order Ambisonics (HOA) über SPAT5 anstelle von vereinfachtem Lautsprecher-Panning **[AP3]**.

---

## Erwarteter Kompetenzgewinn

- **Advanced Spatial Audio:** Vertieftes Verständnis von Higher Order Ambisonics (HOA), Perceptual Panning und IRCAM SPAT5.
- **Embedded Engineering:** Entwurf kabelloser Sensorik (ESP32-C6, BNO085 IMU, OSC-Protokoll, Akku-Ladeschaltungen).
- **DSP & Software Engineering:** Entwurf kompilierbarer Standalone-Audio-Software in Max 9 unter Einsatz von JavaScript für physikalische Simulationen. Max 9 Standalone-Export und Integration in räumliche Audio-Setups. Sample-basierte Synthese und Echtzeit-Processing.
- **Wissenschaftsvermittlung:** Translation komplexer astrophysikalischer Phänomene in haptisch-akustische Exponate.

---

## Software

- **Max 9 (Cycling '74):** Hauptplattform für Logik, Synthese, UI und Standalone-Export **[AP2]**.
- **IRCAM SPAT5:** Paket für spatiales Panning, HOA-Decoding und Raumakustik-Simulation **[AP3]**.
- **Audinate Dante Virtual Soundcard (DVS):** Treiber zur verlustfreien Ansteuerung von 16+ Audio-Kanälen über Netzwerk **[AP3]**.
- **Arduino IDE / VS Code (PlatformIO):** C++ Entwicklung für den ESP32-C6 Controller **[AP1]**.

---

## Hardware

- **Sputnik-Gyro-Controller:** Eigenbau-Exponat mit ESP32-C6, BNO085 9-DOF IMU, 1200 mAh LiPo-Akku und USB-C Ladeport **[AP1]**.
- **MacBook Pro M2 Max:** Host-Rechner für die Ausführung des Max 9 Standalone-Patches.
- **Audio-Hardware:** Dante-fähiges Audio-Interface / Digitalmischpult und 7.1.4 Lautsprecher-Array im 3D-Audio-Labor und binauralem Setup für Projektvernissage **[AP3/AP5]**.

---

## Werbung

![Poster](images/poster.png){: style="width:50%"}