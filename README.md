# linux_libnfc-nci
This is a fork of the official NXP Linux NFC Stack (https://github.com/NXPNFCLinux/linux_libnfc-nci)
Modifications made are
1. Ability to set the library configuration programmatically 
2. Ability to retrive tag ATQA/B response data

## Setting library configuration
To set the library configuration, you will need to
1. Deinitialise the NFC Stack by calling `nfcManager_doDeinitialize`
2. Set the configuration by calling `setConfigValue`
3. Initialise the NFC Stack by calling `nfcManager_doInitialize`

An example to set the config value of HOST_LISTEN_TECH_MASK to 0x02:
```c
unsigned long techMask = 0x02;
setConfigValue("HOST_LISTEN_TECH_MASK", &techMask, sizeof (techMask));
nfcManager_doInitialize();
```

## Retriving ATQB information
To retrive the ATQB information, you will need to access the field `add_data` in the `nfc_tag_info_t` struct  
The ATQB information will be thr first 11 bytes of `add_data`  
ATQA information retrival is currently not complete.  


linux_libnfc-nci
================
Linux NFC stack for NCI based NXP NFC Controllers (PN7150, PN7120).

Information about NXP NFC Controller can be found on [NXP website](https://www.nxp.com/products/identification-and-security/nfc/nfc-reader-ics:NFC-READER).

Further details about the stack [here](https://www.nxp.com/doc/AN11697).

Release version
---------------
R2.4 includes dynamic adaptation to the NFC Controller, multiple tags support, and some bug fixes (refer to the [documentation](https://www.nxp.com/doc/AN11697) for more details).

R2.2 includes support for alternative to pn5xx_i2c kernel driver and some bug fixes (refer to the [documentation](https://www.nxp.com/doc/AN11697) for more details).

R2.1 includes support for PN7150 NFC Controller IC and some bug fixes (refer to the [documentation](https://www.nxp.com/doc/AN11697) for more details).

R2.0 includes LLCP1.3 support and some bug fixes (refer to the [documentation](https://www.nxp.com/doc/AN11697) for more details).

R1.0 is the first official release of Linux libnfc-nci stack

Possible problems, known errors and restrictions of R2.4:
---------------------------------------------------------
LLCP1.3 support requires OpenSSL Cryptography and SSL/TLS Toolkit (version 1.0.1j or later)
