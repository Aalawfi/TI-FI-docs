#######
Startup
#######

| **Power up sequence**:
| The power-up sequence for the hardware is simple from the user’s perspective. Before
| any power is applied to either board, it is important that the connection between the
| daughterboard and the main board is securely made. The header pin connectors are not keyed
| in any way, so it is very important to double-check the orientation of the daughterboard as it
| plugs into the main board – visual cues will be included on the top silkscreen layer of the
| daughterboard to reduce the risk of misalignment. The user will also need to plug the PIR sensor
| into its corresponding connector on the daughterboard and the additional sensor to the STEMMA
| QT port if it is being used. It is never okay to hot plug any part of the system.

Once the user ensures the daughterboard is securely mated to the mainboard and the PIR
sensor and generic sensor (if being used) are connected, they will then connect the main board
to 5V power with the micro USB port. This power can be sourced from a computer but will likely
come from a 5V wall adapter when deployed. Any source is fine provided it adheres to the USB
specification for power delivery (5 Vdc, 2.5 W max).
When 5V is supplied to the main board, its buck regulator will begin ramping up its output
to produce a stable 3.3Vdc, which all logic runs from. The regulator begins switching after 50 μs
and output voltage rises at about 25 mV / μs, yielding an approximate turn-on time of 0.2 ms.
Because our system’s operation is all derived from the 3.3V supply, there is no need to sequence
delivery of varying voltages.

After the 3.3V supply has stabilized, the digital ICs each have their own respective
power-up times coming out of a hard reset. For the VOC sensor, the SGP40, this time is typically
0.4 ms, with a max of 0.6 ms. For the humidity sensor, SHT40, this time is a max of 1 ms. The
other ICs all have their own turn-on times which are on the same order of magnitude except for
the microcontroller, which has a much longer power-up sequence due to its complexity. The
hardware wake-up time alone is typically 25 ms, followed by a 17 ms hardware initialization, and
then somewhere on the order of a 1/10th of a second to load the application code. This is good
because the total time to full operation is barely perceptible, and there is no need to add software
waits for the peripherals to finish initializing before communicating with them because the
microcontroller takes far longer to initialize anyway.
For powering down, the only action required is removing the micro USB cable. This should
be done before any disassembly. It is always crucial that the USB power is the last thing added
and the first thing removed when interacting with the hardware.

.. note::

   This project is under active development.
