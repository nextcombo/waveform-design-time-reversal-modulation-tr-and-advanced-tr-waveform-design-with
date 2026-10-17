# Waveform Design: Time Reversal Modulation (TR) and Advanced TR Waveform Design [With MATLAB Code]

I. Research Foundation: The construction of Discrete Time Baseband Equation Channel Model
1. The ideal AWGN channel model starts with the additive white Gaussian noise (AWGN) channel and employs a root raised cosine (RRC) filter as both the transmitter and receiver filters. Based on the characteristics of the RRC filter, it is capable of achieving uncoded intersymbol interference (ISI) transmission, while ensuring the Nyquist frequency through up-sampling and down-sampling. Tested with BPSK, QPSK, 16QAM, and other modulation schemes, the simulation of symbol error rate (SER) closely matches the theoretical values, verifying the effectiveness of the model.
2. Research on linear equalizers: Multipath propagation can cause signal distortion and intersymbol interference (ISI), which requires equalization through an equalizer. This study compares two types of linear equalizers.
•  
Zero-IF Filter (ZFE): The core is to eliminate residual ISI, but when the zero of channel transfer function (CTR) is close to the unit circle, noise will be amplified significantly, leading to a sharp performance drop. Moreover, when implementing FIR, only a limited range can ensure an ideal impulse response, and outside this range, large interference values are prone to occur.
•  
Minimum Mean Square Error Linear Equalizer (MMSE-LE): It balances ISI elimination and noise suppression, significantly lowering the bit error rate at medium to low signal-to-noise ratio (SNR) compared to ZF. At high SNR, its performance approaches that of ZF, but in low SNR, it may cause channel transmission function distortion due to noise filtering (with a bias), but this can be mitigated by amplifying symbols back onto the correct constellation, without affecting the effectiveness of noise suppression.
3. Multipath Channel Modeling: To make the simulation more realistic, two types of multipath channel models have been constructed.
•  
Simple Exponential Channel Model: The channel impulse response (CIR) coefficients follow a circular symmetric complex Gaussian distribution, with path gain energy exhibiting exponential decay. This model is concise and suitable for preliminary analysis and simulation.
•  
802.15.4a Indoor Channel Model: Saleh-Valenzuela (SV) Model for More Accurate Reproduction of Realistic Scenarios
Taking residential environments as an example, the model distinguishes between line-of-sight (LOS) and non-line-of-sight (NLOS) scenarios, taking into account cluster delay, ray arrival rate, and other parameters to verify the reliability of simple models.

II. Core Research: Performance Analysis of TR Single User and Multi-User Models Based on the aforementioned channel model
The research team has developed TR single user and multi-user models based on the above channel model, focusing on analyzing the impact of key parameters on system performance.
1. TR Single User Model (Downlink Only):
Core Design: The transmit filter adopts the time-reversal conjugate form of CIR without requiring a receive filter or equalizer, only requiring a single tap detection, significantly reducing terminal complexity. A rate reversion factor (D) is introduced to control the transmission rate (D=1 has the highest rate, increasing D results in inserting zeros between symbols to extend the symbol period), and a power control factor (β) is used to adjust the receive signal constellation diagram, without affecting the signal-to-noise ratio (SNR).
Performance Pattern: By analyzing the average Signal-to-Interference-plus-Noise Ratio (SINR), it is found that when the transmission rate decreases (D increases) or the richness of multipaths improves (such as when the system bandwidth is widened, allowing more paths to be perceived), SINR significantly improves. This is because increasing D can reduce symbol overlap and reduce Intersymbol Interference (ISI), while enhancing the freedom of position-specific signatures due to the richness of multipaths.
2. TR Multi-User Model (Analysis of Uplink and Downlink Transmissions)
Downlink transmission: The base station sends the combined signals of all users through a single antenna, utilizing the TR spatial focusing characteristic to allow each user to only receive their focused signal. Using average reachability and rate as indicators, it is found that although increasing D can reduce ISI and improve signal quality, it also reduces symbol rate; an increase in user number (N) leads to more concurrent data streams but also exacerbates user-to-user interference (IUI), resulting in a decrease in single user rate. It is necessary to balance the signal quality with the total system rate between D and N.
Uplink transmission: multiple users simultaneously send signals to the base station, which extracts the target signal through user-specific signature waveforms. Although there are structural differences between the uplink and downlink models, mathematical derivations and simulations indicate that the uplink also possesses spatiotemporal focusing characteristics, with performance similar to that of the downlink. Therefore, subsequent waveform design research will focus solely on downlink scenarios.
III. Performance Optimization: In scenarios where high transmission rates (small D) and high user density (large N) are present, ISI and IUI can severely degrade system performance. For example, when D=1 and N increases from 5 to 15, the average throughput of the system barely improves, necessitating waveform design optimization.
1. The introduction of pre-equalization technology moves the equalizer from the user side to the base station side (pre-equalization), avoiding noise amplification through the equalizer. Both ZFE and MMSE-LE pre-equalization methods were employed, and results showed that both improved SER, with MMSE-LE pre-equalization showing superior performance. However, even so, SER could not meet practical requirements at high transmission rates (e.g., D=1).
2. Optimal Waveform Design: With the goal of minimizing Mean Square Error (MSE), we solve for the optimal waveform through convex optimization (Karush-Kuhn-Tucker conditions). Breakthroughs are achieved in different scenarios.
•  
Single user scenario: The optimized waveform can significantly suppress ISI. For example, when D=1, the interference component of channel transmission function (CTR) is significantly reduced; when D=3, although the energy of non-interference points is higher, due to the symbol interval being 3 time units, it does not affect other symbols, and the SER is further reduced compared to pre-equalization technology.
•  
Multi-user scenario: Integrate all user waveforms into vector solutions, which not only enhances the time focusing effect of individual users' signals (reducing ISI) but also reduces interference to other users (enhancing spatial focusing and reducing IUI). The larger D, the more significant the performance improvement (D=3, 5 outperforms D=1), but as the number of users increases, it still limits the performance ceiling. The average throughput at N=5 is higher than in scenarios with N=10 or 15.
3. Challenges and Future Directions in Waveform Optimization
The current optimal waveform design has three limitations: First, it does not consider the power emission constraints, which may result in excessive waveform energy in extreme cases; second, the matrix operation complexity is extremely high under multi-user scenarios (e.g., when there are 10 users and the CIR length is 100, it requires processing a 1000×1000 matrix for inverse calculation); third, strict synchronization requirements lead to strong interference due to synchronization deviations.
Four directions for future research can be explored: Trying more complex equalizers or combinations of equalizers; incorporating power constraints into the optimization model; developing low-complexity optimization solving algorithms; and introducing interference pre-elimination concepts to further suppress ISI.
Conclusion 1:
TR transmission systems, with their spatiotemporal focusing characteristics, can achieve low complexity and high energy efficiency communication, showing great potential in the 5G and IoT fields. However, issues such as ISI and IUI need to be addressed in scenarios with high transmission rates and high user densities.
Conclusion 2:
Pre-equalization technology can improve system performance while controlling terminal complexity. The MMESE-LE pre-equalization outperforms ZFE pre-equalization.
Conclusion 3:
Optimal waveform design based on minimum mean square error can further enhance performance, but it needs to overcome power, complexity, and synchronization challenges, providing clear directions for the practical application of subsequent TR technologies.
End

## Images

![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](01.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](02.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](03.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](04.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](05.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](06.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](07.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](08.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](09.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](10.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](11.jpg)
![(Waveform Design)Time Reversal Modulation (TR) and Advanced TR Waveform Design [with MATLAB Code]](12.jpg)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
