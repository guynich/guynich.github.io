TL;DR: Use **Apple Configurator** to downgrade a 2018 Mac Mini to macOS **Mojave—don’t use USB installation**.

I run automated 32-bit apps on macOS using an older Mac Mini. Since macOS Mojave
was the last version to support 32-bit apps, anything newer breaks my workflow.

The last Mac Mini model that can technically run 32-bit apps is the **2018 Intel
Mac Mini**. I found a high-spec unit on sale—at under 15% of the original price.
With a **6-core Intel i7, 32GB RAM, 1TB SSD, and 10Gbps Ethernet**, it’s a
serious upgrade. It arrived running macOS Sonoma.

To get my 32-bit apps working, I attempted a USB installation of
`Install macOS Mojave` from the App Store. That seemed promising... until I hit
problems:

* The Mojave installer would boot, but Recovery Mode wouldn’t.
* I got cryptic errors like `-1000F` during boot to recovery.
* The **T2 chip** blocked older 32-bit apps due to its security settings.
* But those settings couldn’t be changed—because Recovery didn’t work.

Total Catch-22.

Solution:
Use Apple Configurator (from the App Store) on another Mac. Then:

- 1. Connect the two Macs with a stock Apple USB-C to USB-C white cable (the one from a charger).
- 2. Use the Restore function in Configurator to wipe and reflash the 2018 Mac Mini.
- 3. After the restore, boot into Recovery and install macOS Mojave.
- 4. Now Recovery works, T2 settings can be adjusted, and 32-bit apps run.

Sharing this in case it saves someone else the headache.
