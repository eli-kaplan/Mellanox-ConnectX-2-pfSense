# Mellanox ConnectX-2 pfSense Drivers
Pre-Compiled Kernel Modules for Mellanox ConnectX-2 / pfSense 2.4.4

For whatever reason, the drivers for this (very cost-effective) 10GBit SFP+ expansion card are not included in pfSense. Additionally, pfSense does not include the necessary compiler to build these modules from source. 

To get the ConnectX-2 working under pfSense, I had to build the kernel modules for it from source on a separate FreeBSD 11 machine. To potentially save someone else this hassle, I've decided to upload these pre-compiled kernel modules to GitHub. 

# Instructions:
- Unzip the `Mellanox.zip` file (under Releases) somewhere on your pfSense host.
- Copy all of the `*.ko` files within to /boot/kernel/
- `chmod 555 /boot/kernel/ml*.ko` and `chmod 555 /boot/kernel/linuxkpi.ko` to ensure the new modules have the proper permissons.
- `kldload mlx4en` to load the module - after doing this, pfSense should detect the card as a new interface
- After making sure the driver works properly, edit `/boot/loader.conf` and append `mlx4en_load="YES"` to load the driver on boot.
- Success!

# Compatibility
- Tested on pfSense 2.4.4 (FreeBSD 11.2-RELEASE-p3) amd64
- I cannot guarantee this will be compatible with your system, but it _should_ work on any pfSense release based on FreeBSD 11
- Tested with Mellanox ConnectX-2 but this set of kernel modules should also support the ConnectX-3 and ConnectX-4. To enable ConnectX-4 support, you'll probably have to change `mlx4en_load` to `mlx5en_load`.
