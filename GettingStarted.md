Now that you have the max speed of the single PCI slot we need to understand this number represents the max speed of the bus if nothing else is using the PCI bus. Since all PCI cards and built on-board chips use the same bus then they must also be taken into account. If we have two network cards each using a 64bit, 133MHz slot then each slot will get to use 50% of the total speed of the PCI bus. Each card can do 133\*64/8= 1064 Megabytes/second and if both network cards are being used at once, like on a firewall, then each card can use 1064/2= 532 Megabytes/second max. This is still well above the maximum speed of a gigabit connection which can move 1000/8= 128 Megabytes/second.

PCI Express is a newer technology which elevates bus bandwidth from hundreds of megabytes per second to many gigabytes per second. This allows a single machine to support multiple gigabit ports per interface card or even multiple 10 gigabit ports. The PCIe link is built around dedicated unidirectional couples of serial (1-bit), point-to-point connections known as lanes. This is in sharp contrast to the earlier PCI connection, which is a bus-based system where all the devices share the same bidirectional, 32-bit or 64-bit parallel bus. PCIe's dedicated lanes allow for an incredible increase in bandwidth.

```
These values were collected from the PCIe Wikipedia page:

(type)      (bus speed) *  (bus width)    / 8 = (speed in Megabytes/second)

PCI            66 MHz   *  32 bit         / 8 =   264 MB/s
PCIe v1      2500 Mhz   *  32 1 bit lanes / 8 =   250 MB/s (minus 20% overhead)
PCIe v2 x1   5000 Mhz   *   1 1 bit lane  / 8 =   500 MB/s (minus 20% overhead)
PCIe v2 x2   5000 Mhz   *   2 1 bit lanes / 8 =  1000 MB/s (minus 20% overhead)
PCIe v2 x4   5000 Mhz   *   4 1 bit lanes / 8 =  2000 MB/s (minus 20% overhead)
PCIe v2 x8   5000 Mhz   *   8 1 bit lanes / 8 =  4000 MB/s (minus 20% overhead)
PCIe v2 x16  5000 Mhz   *  16 1 bit lanes / 8 =  8000 MB/s (minus 20% overhead)
PCIe v2 x32  5000 Mhz   *  32 1 bit lanes / 8 = 16000 MB/s (minus 20% overhead)
PCIe v3 x32  5000 Mhz   *  32 1 bit lanes / 8 = 19700 MB/s (minus 1.5% overhead)
```

We highly recommend getting an interface card supporting PCIe due to their high bandwidth and low power usage. Note, PCIe version 2.x has a 20% bandwidth overhead which PCIe version 3.x does not. PCIe 2.0 delivers 5 GT/s (GT/s is Gigatransfers per second), but employs an 8b/10b encoding scheme which results in a 20 percent overhead on the raw bit rate. PCIe 3.0 removes the requirement for encoding and uses a technique called "scrambling" in which "a known binary polynomial" is applied to a data stream in a feedback topology. Because the scrambling polynomial is known, the data can be recovered by running it through a feedback topology using the inverse polynomial and also uses a 128b/130b encoding scheme, reducing the overhead to approximately 1.5%, as opposed to the 20% overhead of 8b/10b encoding used by PCIe 2.0.

Look at the specifications or motherboard you expect to use and the above equation to get a rough idea of the speeds you can expect out of the box. Hardware speed is the key to a fast firewall. Before setting up your new system and possibly wasting hours wondering why it is not reaching your speed goals, make sure you understand the limitations of the hardware. Do not expect throughput out of your system hardware that it is _not_ capable of.

For example, when using a four port network card on a machine, consider the bandwidth of the adapter slot you put it into. Standard PCI is a 32 bit wide interface and the bus speed is 66MHz or 133 MHz. This bandwidth is shared across all devices on the same bus. PCIe v1 is a serial connection with 2.5 GHz frequency in both directions for a 1x slot. The effective maximum bandwidth is 250MB/s bidirectional. So, if you decide to support 4, 1Gbps connections on one card it might be best to do it with a PCIe v2 8x or faster slot and card.



[label](http://domain/page)