# FPGAprog

Unofficial port of the `fpgaprog` utility to work on OSX, which can be used to
flash or load bit files to the Pipistrello board from Saanlima.

## Installation

You need to install both `libftdi` and `libusb-1.x`, for example, using
HomeBrew:

    $ brew install libftdi libusb

Compilation is simply a matter of running `make`:

    $ make
    ...
    $ ls fpgaprog
    fpgaprog

To flash bitfiles to the flash memory of your Pipistrello, you need to provide
the correct `bscan_spi` bit file. Copy the file `bscan_spi_lx45_csg324.bit` to
a place for later access.

For libftdi to work, you need to unload the FTDI serial driver that is loaded
automatically by OSX:

    $ sudo kextunload -b com.FTDI.driver.FTDIUSBSerialDriver

## Usage

The `fpgaprog` program takes the following options:

    -v                   Enable verbose output;
    -j                   Detect JTAG chain, nothing else;
    -d                   FTDI device name;
    -f <bitfile>         Main bit file;
    -b <bitfile>         bscan_spi bit file (enables spi access via JTAG);
    -s [e|v|p|a]         SPI Flash options: e=Erase Only, v=Verify Only, p=Program Only or a=ALL (Default);
    -c                   Display current status of FPGA;
    -C                   Display STAT Register of FPGA;
    -r                   Trigger a reconfiguration of FPGA;
    -a <addr>:<binfile>  Append binary file at addr (in hex);
    -A <addr>:<binfile>  Append binary file at addr, bit reversed.

To load (not flash) a bit file:

    fpgaprog -v -f <bit_file>

To flash a bit file, you need to enable the SPI port to the flash chip through
the JTAG port:

    fpgaprog -v -f <bit_file> -b path/to/bscan_spi_lx45_csg324.bit -sa -r

## License

The code is licensed under GPLv2. All modifications made by me (JaWi) are
licensed under GPLv2 as well.

## About

This code is based on the source code provided by Magnus Karlsson from Saanlima
and can be found here:

<http://pipistrello.saanlima.com/index.php?title=Welcome_to_Pipistrello#Fpgaprog_utility_program_download>

