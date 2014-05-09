# FilterClientSystemArch patch for Dual DHCP DNS Server

This is a patch repository of Dual DHCP DNS Server (DualServerSourceV7.12.zip) as published at https://sourceforge.net/projects/dhcp-dns-server/.

This patch supports for filtering a RANGE_SET by booting in EFI or Legacy BIOS mode. Client System Architecture Type (option 93) is sent by a client from booting in EFI mode.

## Patch file

- [[PATCH] Add support for filtering a RANGE_SET by booting in EFI or Legacy BIOS mode](https://github.com/jfut/dualserver-filter-arch-patch/commit/11ea6a58932b1f994b1ab45078a1f6bb4a5827c0.patch)

## Compile

On Cygwin environment:

    i686-pc-mingw32-g++.exe -o DualServer.exe DualServer.cpp -lwsock32 -liphlpapi -lws2_32 -static-libgcc -static-libstdc++

## Config example

The client from booting in EFI mode is sent 00:07 value.

Select BootFileName:

- Legacy BIOS mode: /Boot/pxeboot.n12
- EFI mode: /bootmgfw.efi

DualServer.ini:

```
[SERVICES]
DHCP

[LOGGING]
DHCPLogLevel=All

[HTTP-INTERFACE]
127.0.0.1:6789

[TIMINGS]
AddressTime=43200

[RANGE_SET]
DHCPRange=192.168.200.11-192.168.200.100
SubnetMask=255.255.0.0
BootFileName=/Boot/pxeboot.n12

[RANGE_SET]
FilterClientSystemArch=00:07
DHCPRange=192.168.200.101-192.168.200.200
SubnetMask=255.255.0.0
BootFileName=/bootmgfw.efi

[GLOBAL_OPTIONS]
NextServer=192.168.1.112
```

## Copyright

* License: GPLv2
