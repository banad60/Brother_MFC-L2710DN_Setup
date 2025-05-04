# Brother MFC-L2710DN Setup auf Ubuntu

### Einführung
Der Brother MFC-L2710DN ist ein zuverlässiger Multifunktionsdrucker, der Drucken, Scannen und Faxen unterstützt. Diese Anleitung beschreibt die Einrichtung auf Ubuntu 24.04 Schritt für Schritt, damit alle Funktionen genutzt werden können. Das Gerät bietet ein hervorragendes Preis-Leistungs-Verhältnis und ist Linux-kompatibel.

### Voraussetzungen
- Ubuntu 24.04 (oder ähnliche Linux-Distribution)
- Brother MFC-L2710DN via USB oder Netzwerk verbunden
- Internetzugang für Treiber-Downloads

### Schritt 1: Druckertreiber installieren
1. **Driver Install Tool herunterladen**: Besuchen Sie die [Brother Support-Seite](https://support.brother.com/g/b/downloadtop.aspx?c=eu_ot&lang=de&prod=mfcl2710dn_eu) und laden Sie das "Driver Install Tool" für Linux.
2. **Tool entpacken**: Führen Sie im Terminal aus:
   ```
   gunzip linux-brprinter-installer-*.gz
   ```
3. **Installer starten**: Geben Sie ein:
   ```
   sudo bash linux-brprinter-installer-* MFC-L2710DN
   ```
4. **Anweisungen befolgen**: Bestätigen Sie Modellname und Verbindungstyp (USB oder Netzwerk).

### Schritt 2: Scanner einrichten
1. **Scanner-Treiber installieren**: Nutzen Sie das Driver Install Tool oder laden Sie `brscan4` von der Brother-Website.
2. **Scanner zu SANE hinzufügen**: Führen Sie aus:
   ```
   sudo brsaneconfig4 -a name=MFC-L2710DN model=MFC-L2710DN ip=192.168.1.100
   ```
   Ersetzen Sie `192.168.1.100` durch die IP-Adresse Ihres Druckers.
3. **Scannen testen**: Starten Sie `simple-scan` oder `xsane`.

### Schritt 3: Fax-Funktion einrichten
1. **Fax-Treiber installieren**: Laden Sie `brmfcfaxdrv` von der Brother-Website und installieren Sie es:
   ```
   sudo dpkg -i brmfcfaxdrv-*.deb
   ```
2. **Fax-Drucker prüfen**: Überprüfen Sie:
   ```
   lpstat -p
   ```
   Suchen Sie nach `BRFAX`.
3. **Fax senden**: Per Kommandozeile:
   ```
   brpcfax -o fax-number=xxxxxxxx -o PageSize=A4 sample.pdf
   ```
   Oder wählen Sie `BRFAX` in LibreOffice und geben Sie die Nummer ein.

### Problemlösungen
- **udev-Regeln-Fehler**: Bei "Invalid key 'SYSFS'" bearbeiten Sie `/etc/udev/rules.d/60-brother-brscan4-libsane-type1.rules`, ersetzen `SYSFS` durch `ATTRS` und starten udev neu:
   ```
   sudo systemctl restart udev
   ```
- **Probleme mit Scan-Apps**: Bei Snap-Apps wie `simple-scan`:
   ```
   snap connect simple-scan:desktop
   ```
- **HPLIP-Konflikt**: Entfernen Sie HPLIP bei Fax-Problemen:
   ```
   sudo apt remove hplip
   ```

### Fazit
Der Brother MFC-L2710DN funktioniert auf Ubuntu einwandfrei. Auch ohne Adressbuch für Faxe können Nummern manuell eingegeben werden. Ein tolles, Linux-taugliches Gerät!
