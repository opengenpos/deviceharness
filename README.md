# deviceharness
Repository containing old NHPOS/GenPOS peripheral interfaces for POS devices such as scales, scanners, printers.

Prior to Rel 2.0.0 and the retirement of the NCR 7448 terminal, NHPOS used peripheral interface software
which allowed the point of sale to use peripherals such as scales, scanners, and printers through a
Serial Communications port interface rather than using OPOS components.

## Brief overview

With the first release of the OpenGenPOS source code, we are removing legacy source code that currently has no
use. However these peripheral interface software components are interesting to review and may prove useful in the
future. There is also something of a historical value to this source code as it shows an implementation of interfaces
that implement several different device communication protocol standards.

Each different peripheral type has its own Windows DLL. There is a standard DLL interface which in some ways mimics
the OPOS Control Object interface. However the build products are Windows DLLs rather than the COM objects of OPOS.

The procedure for using the device DLL is to use the `LoadLibrary()` Windows API function to load the DLL into memory
and then use the `GetProcAddress()` Windows API function to obtain a pointer to each of the device interface functions
the DLL exports, placing the function pointer into a `struct` which is then used to access the functions of the DLL.

Once the device interface DLL is no longer needed, the FreeLibrary() Windows API function is used to unload the DLL
from memory and free up the resources it uses.

These device DLLs were written to use an RS-232 compatible Serial Communications port and required either the Serial
Communications port hardware connector or something that looked like a Serial Communications port. This then required
that a USB connected device either used an installed and configured Virtual Serial Port device driver or a hardware
converter cable that converted between USB and RS-232 electrical signals and logic.

A future innovation would be to provide the necessary interfaces for direct USB communication and/or Bluetooth
communications and/or Ethernet LAN communications.
