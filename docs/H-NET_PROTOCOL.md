
## Physical Level
The Home Bus System, originally developed in Japan for residential automation, forms the physical layer foundation for various protocols—including Hisense’s H-net communication system, which adopts this medium to interconnect its HVAC units and controllers.
The Home Bus relies on a single twisted-pair cable in a bus configuration. In the standard ET-2101 version, the maximum bus length is 200 meters, while the Extended Home Bus specification expands this to 1 kilometer, suitable for larger residential complexes or multi-apartment installations.
A notable feature is that the same wire pair carries both data and power (up to 36 V). Power is coupled onto the bus inductively by the controller. The data lines, designated H⁺ and H⁻, invert their polarity with each transmitted bit, maintaining DC balance and ensuring stable operation regardless of common-mode voltage offsets.
Communication operates at 9.6 kbaud ±0.13% using a baseband technique. Extended versions of the standard allow higher throughput. Data encoding uses Alternative Mark Inversion (AMI) with negative logic and a 50% duty cycle: each logic “0” toggles the line polarity between H⁺ and H⁻, opposite to conventional AMI.
Signal thresholds are tightly defined: a logical “0” corresponds to 0.6 V (Vₗₗ), and a logical “1” corresponds to 1.4 V (receive) or 2.5 V (transmit) across the line pair. This ensures robust recognition of symbols across all devices on the bus.
Bus access arbitration follows Carrier Sense Multiple Access with Collision Detection (CSMA/CD), similar to Ethernet, preventing data corruption when multiple devices attempt transmission simultaneously.
Finally, the system uses start-stop framing—like UARTs—for synchronization, since there is no dedicated clock signal on the line. Each character frame is composed of 11 bits, transmitted least significant bit first, with even parity for error detection.

# Data Frame
