
## PSRAM/HyperRAM controller for Tang Nano 9K

This is an open source PSRAM/HyperRAM controller for the [Tang Nano 9K](https://wiki.sipeed.com/hardware/en/tang/Tang-Nano-9K/Nano-9K.html) FPGA board. The chip is Gowin GW1NR-LV9QN88PC6/15.

Overview

* Supports both word (16-bit) and byte based access. No bursting is used.
* 1:1 clock design. Memory and main logic work under the same clock. Max clock frequency is 83Mhz.
* I'm mostly aiming for low access latency. Write latency is 7 cycles (1x) or 10 cycles (2x). Read latency is 12 cycles (1x) or 15 cycles(2x). HyperRAM needs 2x latency now and then for automatic DRAM refreshes. In my test, 2x latency happens about 0.05% of time. 
* Uses Gowin's ODDR/IDDR primitives. This removes the need to use double frequency clocks. A PLL is used to generate the phase-shifted clock needed by HyperRAM.
* Code is simple. 200 lines of Verilog. Resource usage: <200 logic units, vs ~1000 for official IP. 

Usage
* `psram_controller.v` is the controller. See comments for usage.
* Also read the test bench `psram_test_top.v` for an actual example. It works at 81 Mhz, uses byte-based access, and writes its results to UART at 115200 bps.

See also
* [An example](https://github.com/zf3/some-tang-nano-9k-examples) using the official Gowin HyperRAM IP. The official IP uses bursting access (writes/reads >= 16 bytes a time). So it is higher throughput, but also higher latency. And it is encrypted verilog. :(
* [Tang 20K official examples](https://github.com/sipeed/TangPrimer-20K-example), where the UART module comes from.

Feng Zhou, 2022.8
