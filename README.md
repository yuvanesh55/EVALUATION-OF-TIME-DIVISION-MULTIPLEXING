# EVALUATION-OF-TIME-DIVISION-MULTIPLEXING

### Aim:
Study of TDM pulse amplitude modulation/ demodulation with transmitter block (clock) and channel identification information linked directly to the receivers.  

### Apparatus Required:

1)	Experimental kit DCL-02  
2)	Connecting chord  
3)	Power supply  
4)	20 MHz dual trace oscilloscope.  

### Theory:
In PAM, PPM the pulse is present for a short duration and for most of the time between the two pulses no signal is present. This free space between the pulses can be occupied by pulses from other channels. This is known as Time Division Multiplexing. Thus, time division multiplexing makes maximum utilization of the transmission channel. Each channel to be transmitted is passed through the low pass filter. The outputs of the low pass filters are connected to the rotating sampling switch (or) commutator.
It takes the sample from each channel per revolution and rotates at the rate of f s. Thus the sampling frequency becomes fs the single signal composed due to multiplexing of input channels. These channels signals are then passed through low pass reconstruction filters. If the highest signal frequency present in all the channels is fm, then by sampling theorem, the sampling frequency fs must be such that fs≥2fm. Therefore, the time space between successive samples from any one input will be  Ts=1/fs, and Ts =1/2fm.

### Procedure:

1)	Refer to the block diagram and carry out the following connections and switch setting. 
2)	Connect power supply in proper polarity DCL-02 and s it switch it on.  
3)	Connect 250hz, 500hz, 1khz and 2khz sine wave signals from the function generator to the multiplexer input channels CH0, CH1,CH3 by means of connecting chords.  
4)	Connect the multiplexer output txd of the transmitted section to the de multiplexer input rxd of the receiver section.  
5)	Connect the output of the receiver section CH0, CH1, CH2,CH3 to the IN0, IN1, IN2. IN3 of the filter section.  
6)	Connect the sampling clock TX CLK channel identification clock TXSYNC of the transmitter section to the corresponding RXCLK, RXSYNC of the receiver section respectively.  
7)	Set the amplitude of the input sine wave desired.   
8)	Take the observations as mentioned below.

### Kit Diagram
<img width="480" height="324" alt="image" src="https://github.com/user-attachments/assets/b2f8f171-ceff-4481-add2-bc4ef1c42506" />

### Model Graph
<img width="718" height="933" alt="image" src="https://github.com/user-attachments/assets/09c11b43-dc9c-4bf9-a04a-0728d0b0fea3" />

### Tabulation

<img width="672" height="448" alt="image" src="https://github.com/user-attachments/assets/05600b28-ba54-4cd4-9ff4-f088865e85ae" />

### Program
```
Fs = 56300;
t = 0:1/Fs:0.02;
m1 = sin(2*%pi200t); m2 = sin(2*%pi300t); m3 = sin(2*%pi400t); m4 = sin(2*%pi500t); m5 = sin(2*%pi600t); m6 = sin(2*%pi700t);

c1 = 3000; c2 = 6000; c3 = 9000; c4 = 12000; c5 = 15000; c6 = 18000;

carrier1 = cos(2*%pic1t); carrier2 = cos(2*%pic2t); carrier3 = cos(2*%pic3t); carrier4 = cos(2*%pic4t); carrier5 = cos(2*%pic5t); carrier6 = cos(2*%pic6t);

s1 = m1 .* carrier1; s2 = m2 .* carrier2; s3 = m3 .* carrier3; s4 = m4 .* carrier4; s5 = m5 .* carrier5; s6 = m6 .* carrier6;

s_total = s1 + s2 + s3 + s4 + s5 + s6;

// Demultiplex: multiply by carriers to shift each band back to baseband r1 = s_total .* carrier1; r2 = s_total .* carrier2; r3 = s_total .* carrier3; r4 = s_total .* carrier4; r5 = s_total .* carrier5; r6 = s_total .* carrier6;

// Simple FFT-based ideal low-pass filter (avoids butter/toolbox issues) function y = ideal_lowpass_fft(x, Fs, fc) N = length(x); X = fft(x); f = Fs*(0:N-1)/N; mask = (f <= fc) | (f >= Fs-fc); Y = X .* mask; y = real(ifft(Y)); endfunction

fc = 1000; dm1 = ideal_lowpass_fft(r1, Fs, fc); dm2 = ideal_lowpass_fft(r2, Fs, fc); dm3 = ideal_lowpass_fft(r3, Fs, fc); dm4 = ideal_lowpass_fft(r4, Fs, fc); dm5 = ideal_lowpass_fft(r5, Fs, fc); dm6 = ideal_lowpass_fft(r6, Fs, fc);

figure(1); subplot(3,2,1); plot(t,m1); title("Message Signal 1"); subplot(3,2,2); plot(t,m2); title("Message Signal 2"); subplot(3,2,3); plot(t,m3); title("Message Signal 3"); subplot(3,2,4); plot(t,m4); title("Message Signal 4"); subplot(3,2,5); plot(t,m5); title("Message Signal 5"); subplot(3,2,6); plot(t,m6); title("Message Signal 6");

figure(2); plot(t, s_total); title("Multiplexed FDM Signal");

figure(3); subplot(3,2,1); plot(t,dm1); title("Recovered Signal 1"); subplot(3,2,2); plot(t,dm2); title("Recovered Signal 2"); subplot(3,2,3); plot(t,dm3); title("Recovered Signal 3"); subplot(3,2,4); plot(t,dm4); title("Recovered Signal 4"); subplot(3,2,5); plot(t,dm5); title("Recovered Signal 5"); subplot(3,2,6); plot(t,dm6); title("Recovered Signal 6");
```
### Output

<img width="757" height="727" alt="image" src="https://github.com/user-attachments/assets/c6b439d1-6a6f-4f0d-917a-c1cca85648fe" />
<img width="759" height="722" alt="image" src="https://github.com/user-attachments/assets/6d866f70-839b-4d76-8f6e-4bd909e8ea08" />
<img width="761" height="721" alt="image" src="https://github.com/user-attachments/assets/6e4ba086-b906-4c2f-b25e-19c38e410f33" />




### Result
To Study of TDM pulse amplitude modulation/ demodulation with transmitter block (clock) and channel identification information linked directly to the receivers is verified.



