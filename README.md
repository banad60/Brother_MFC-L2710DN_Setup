# Brother MFC-L2710DN Setup on Ubuntu

### Introduction
The Brother MFC-L2710DN is a reliable multifunction printer offering printing, scanning, and faxing capabilities. This guide provides clear, step-by-step instructions to set it up on Ubuntu 24.04, ensuring full functionality. It’s a cost-effective, Linux-compatible device perfect for home or small office use.

### Prerequisites
- Ubuntu 24.04 (or similar Linux distribution)
- Brother MFC-L2710DN connected via USB or network
- Internet access to download drivers

### Step 1: Install Printer Drivers
1. **Download the Driver Install Tool**: Visit the [Brother Support Page](https://support.brother.com/g/b/downloadtop.aspx?c=eu_ot&lang=en&prod=mfcl2710dn_eu) and download the "Driver Install Tool" for Linux.
2. **Extract the Tool**: Open a terminal and run:
   ```
   gunzip linux-brprinter-installer-*.gz
   ```
3. **Run the Installer**: Execute:
   ```
   sudo bash linux-brprinter-installer-* MFC-L2710DN
   ```
4. **Follow the Prompts**: Confirm the model name and connection type (USB or network). The installer will handle the rest.

### Step 2: Configure Scanner
1. **Install Scanner Drivers**: Use the Driver Install Tool or download `brscan4` from the Brother website.
2. **Add Scanner to SANE**: Run:
   ```
   sudo brsaneconfig4 -a name=MFC-L2710DN model=MFC-L2710DN ip=192.168.1.100
   ```
   Replace `192.168.1.100` with your printer’s IP address.
3. **Test Scanning**: Launch `simple-scan` or `xsane` to verify it works.

### Step 3: Set Up Fax Functionality
1. **Install Fax Driver**: Download `brmfcfaxdrv` from the Brother website and install it with:
   ```
   sudo dpkg -i brmfcfaxdrv-*.deb
   ```
2. **Verify Fax Printer**: Check the printer list:
   ```
   lpstat -p
   ```
   Look for `BRFAX`.
3. **Send a Fax**: Use the command line:
   ```
   brpcfax -o fax-number=xxxxxxxx -o PageSize=A4 sample.pdf
   ```
   Or print to `BRFAX` from LibreOffice and enter the fax number in the dialog.

### Troubleshooting
- **udev Rules Error**: If you see "Invalid key 'SYSFS'", edit `/etc/udev/rules.d/60-brother-brscan4-libsane-type1.rules`, replace `SYSFS` with `ATTRS`, and restart udev:
   ```
   sudo systemctl restart udev
   ```
- **Scanning App Issues**: For Snap-based apps like `simple-scan`, connect the desktop interface:
   ```
   snap connect simple-scan:desktop
   ```
- **HPLIP Conflict**: Remove HPLIP if fax errors occur:
   ```
   sudo apt remove hplip
   ```

### Conclusion
With these steps, the Brother MFC-L2710DN works seamlessly on Ubuntu for printing, scanning, and faxing. While it lacks an address book for faxing, manual entry or text files work as a workaround. Enjoy this Linux-friendly device!

[German Version](Howto_de.md)