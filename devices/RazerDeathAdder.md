# Razer DeathAdder 3.5G

This device requires a kernel driver to access its configurable features.

As opposed to some other devices, there is more than one driver that can fit the job.

## Choice of driver

Depending on your situation, you may want choose between the Synapse 2 driver or the legacy (standalone) driver.

I would generally advise using the legacy driver, but if you have Razer Synapse 2 already installed and working, Exo will work with its drivers. (And you won't be required to log in 🤭)

### Legacy driver

The legacy DeathAdder driver seems to be the one which works the best, and offering the most capabilities. It should also be the lightest.

It can be downloaded from here: https://download.cnet.com/razer-deathadder-3-5g-windows-driver/3000-18491_4-77542908.html

This driver works perfectly with Exo, but it will not work if you have more than one supported mouse on the system. (At least, I don't know how it would)

The driver package include support apps.
Once the driver package has been installed, you can extract the kernel driver from the installation directory, then uninstall the support apps and reinstall the driver only.

(NB: It might be possible to just extract the driver without installing. I didn't try it)

### Synapse 2 driver

The Synapse 2 driver can be obtained from an installation of Razer Synapse 2 with the mouse connected (so that Synapse downloads the drivers).

This driver is in some ways more capable than the legacy one, but also quite bloated, as it is composed of multiple KMDF drivers interacting together and we don't need the extra features and device support.
It is also harder to get working and may fail to work at all on some computers.

However, this driver will support multiple mouses at the same time, and Exo can work with it.
