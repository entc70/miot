# Install Raspberry Pi OS on a Raspberry Pi 3 Model B using Raspberry Pi Imager
### (Very Important - Take screenshot of every step's screen to put in Word file.)
## What you need

-   Raspberry Pi 3 Model B
-   microSD card (at least 8 GB; 16 GB or larger recommended)
-   microSD card reader
-   Windows, macOS, or Linux computer with internet access
-   Raspberry Pi power supply and a monitor/keyboard (optional for
    headless setup)

> **Important:** Writing the image erases everything currently stored on
> the microSD card. Back up any files you need before continuing.

## 1. Download and install Raspberry Pi Imager

1.  On your computer, open the official Raspberry Pi software page:
    <https://www.raspberrypi.com/software/>.
2.  Download **Raspberry Pi Imager** for your operating system.
3.  Install and launch Raspberry Pi Imager.

## 2. Insert the microSD card

1.  Insert the microSD card into your computer using the card reader.
2.  Make sure the computer detects the card.
3.  Close any file manager windows showing the card before writing the
    image.

## 3. Select the device and operating system

1.  In Raspberry Pi Imager, click **Choose Device** and select
    **Raspberry Pi 3** (or **Raspberry Pi 3 Model B**, if shown).
2.  Click **Choose OS**.
3.  Select **Raspberry Pi OS (32-bit)** for general use and broad
    compatibility with the Pi 3B.
    -   Don't choose **Raspberry Pi OS Lite (32-bit)**.
4.  If the exact option is not shown, select a currently offered
    Raspberry Pi OS image that lists Raspberry Pi 3 support.

## 4. Select the storage device

1.  Click **Choose Storage**.
2.  Carefully select the microSD card.
3.  Verify its capacity or device name so you do not accidentally select
    another drive.

## 5. Configure settings (optional)

Before writing, Raspberry Pi Imager may offer OS customisation settings.
Open **Edit Settings** or **OS Customisation** if available.

You can configure:

-   **Hostname:** for example, `raspberrypi`
-   **Username and password:** set a username and a strong password
-   **Wireless LAN:** enter your Wi-Fi network name (SSID), password,
    and country if you want wireless access
-   **Locale settings:** choose your time zone and keyboard layout
-   **Remote access:** enable SSH if you plan to access the Pi remotely

Save the settings. These options are optional; you can configure the
system after booting as well.

## 6. Write Raspberry Pi OS to the card

1.  Click **Next** or **Write**.
2.  Confirm the warning that the microSD card will be erased.
3.  Allow Raspberry Pi Imager to download and write the operating
    system.
4.  Wait for the write and verification process to finish. Do not remove
    the card while it is in use.
5.  When Imager reports that the process is complete, close the
    application and safely eject the microSD card.

## 7. Boot the Raspberry Pi 3B

1.  Ensure the Raspberry Pi is powered off.
2.  Insert the prepared microSD card into the Pi's microSD slot.
3.  Connect a monitor and keyboard if using the desktop or local setup.
4.  Connect Ethernet if preferred, or use the Wi-Fi details configured
    earlier.
5.  Connect the power supply. The Pi should start booting from the card.
6.  Complete any first-boot setup prompts that appear.

## Troubleshooting

-   **Pi does not boot:** Reinsert the card, check the power supply, and
    rewrite the image. Confirm that the selected OS image supports
    Raspberry Pi 3.
-   **No desktop appears:** You may have installed the Lite edition,
    which provides a command-line interface only or maybe it's problem with MicroHDMI.
-   **Imager cannot see the card:** Try another card reader or USB port,
    and check whether the card is detected by your computer.
-   **Card-writing error:** Try formatting the card or using another
    known-good microSD card, then write the image again.

------------------------------------------------------------------------

**Installation complete:** Raspberry Pi OS is now installed on the
microSD card and ready to use with your Raspberry Pi 3 Model B.

Official guide:
<https://www.raspberrypi.com/documentation/computers/getting-started.html>
