=================================================
NFC A/B/F Technologies
=================================================

.. list-table:: Overview of NFC Technologies
   :widths: 25 30 45
   :header-rows: 1

   * - Technology
     - Standard
     - Key Characteristics & Applications

   * - **NFC-A**
     - ISO/IEC 14443-3A
     - - Widely used for its simplicity and low cost.
       - **Modulation:** Miller encoding with 100% ASK.
       - **Applications:** Contactless payment cards, access control, and e-ticketing.

   * - **NFC-B**
     - ISO/IEC 14443-3B
     - - Known for security and reliability.
       - **Modulation:** Manchester encoding with 10% ASK.
       - **Applications:** E-passports, national ID cards, and industrial automation.

   * - **NFC-F**
     - ISO/IEC 18092 (FeliCa)
     - - High-speed technology, renowned for fast transaction times.
       - **Modulation:** Manchester encoding.
       - **Applications:** High-volume transactions, public transport ticketing (e.g., Suica) and electronic money in Asia.

Why NFC-F is faster in practice
==================================

The key difference isn't just the raw data transfer speed, but how quickly a connection is established and the data is exchanged.

- Faster Polling: NFC-F (FeliCa) uses a more streamlined "polling" process, which is the time it takes for the reader to detect and initiate communication with a card. This is much quicker than the protocols used by NFC-A and NFC-B.

- Less Overhead: NFC-F's protocol is designed for high-speed, high-volume transactions, such as those used in public transit systems. It requires less data to be sent for command and response cycles, reducing the overall transaction time.

- Optimized for Quick Transactions: The technology was specifically developed for applications where speed is critical, such as paying for a train ticket by simply tapping a card or phone on a reader. The fast-polling and efficient protocol allow the entire transaction to be completed in a fraction of a second, making it feel much faster to the user even if the peak data rate is similar.

In short, while the top-end data transfer rate might be the same on paper, NFC-F's protocol is more efficient, leading to a faster and more responsive experience for the user.

NFC-A modulation and load modulation
============================================

Here are the explanations for NFC-A modulation and load modulation.

- Modulation Poller to Listener – NFC-A

    In NFC, the **poller** (the active device, like a smartphone or card reader) generates a continuous 13.56 MHz radio frequency (RF) field to power the passive **listener** (like an NFC tag or card). To send data to the listener, the poller uses a technique called **Amplitude Shift Keying (ASK)**.

    Specifically for NFC-A, this is done with **Miller encoding** and **100% ASK**. The poller changes the amplitude of its RF field according to the data it wants to send. When a "0" is sent, the field is turned off for a specific duration, which is a 100% change in amplitude. This modulated signal is what the listener detects to receive the data. 



- Load Modulation Listener to Poller (only for NFC-A)

    Since the listener is a passive device without its own power source, it can't generate its own RF field to send data back to the poller. Instead, it "modulates" or alters the poller's existing field. This technique is called **load modulation**.

    The listener does this by changing the electrical load on its own antenna. This causes a tiny, measurable change in the voltage and current of the poller's antenna, which the poller can then detect and demodulate to read the data. In NFC-A, this process is used by the listener to send its response, such as a card's unique ID, back to the poller. This is a fundamental concept for all passive NFC communication and is a key part of the ISO/IEC 14443-3A standard.

    -   How It Works

        #. Power from the Poller: The listener has no internal battery. It gets all its power from the poller's strong 13.56 MHz RF field. This field induces an alternating current in the listener's antenna coil through electromagnetic induction.


        #. Rectification: This alternating current is passed through an on-chip rectifier circuit which converts it into a stable direct current (DC) voltage.

        #. Powering the IC: This rectified DC power is then used to operate the NFC controller IC and any other components on the tag. The IC's power management circuit ensures there's enough stable voltage to function.

        #. Load Modulation for Data Transmission: To send data back, the IC switches a resistive load on and off across the antenna. When the load is switched on, it momentarily draws power from the antenna, causing a small, but detectable, change in the poller's RF field.

        #. Poller Detection: The poller's receiver is sensitive enough to detect these tiny fluctuations in its own field. It decodes these changes as the binary data being sent by the listener.