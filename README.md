
# MATLAB Assignment - Composite Signal Processing

This document contains the MATLAB code for the sequential tasks (a) to (e) as described in the assignment.

---

## (a) Produce the Composite Signal `sig`

```matlab
f_analog = 1000;
analog_t = 0:1/f_analog:1-1/f_analog;
sig = 30*sin(2*pi*3*analog_t) + 20*cos(2*pi*9*analog_t) + 15*sin(2*pi*15*analog_t);
```

---

## (b) Compute Frequency Domain Using `fft` and `fftshift`

```matlab
N = length(sig);
f_axis = (-N/2:N/2-1)*(f_analog/N);
sig_fft = fft(sig);
sig_fft_shifted = fftshift(abs(sig_fft));
```

---

## (c) Sample the Signal `sig`

```matlab
fs = 100;
samp_t = 0:1/fs:1-1/fs;
samp_sig = 30*sin(2*pi*3*samp_t) + 20*cos(2*pi*9*samp_t) + 10*sin(2*pi*15*samp_t);
```

---

## (d) Quantize the Sampled Signal Using 3-bit ADC

```matlab
bits = 3;
L = 2^bits;
max_val = max(samp_sig);
min_val = min(samp_sig);
delta = (max_val - min_val)/L;
quant_levels = min_val + delta/2 : delta : max_val - delta/2;
[~, idx] = min(abs(samp_sig' - quant_levels), [], 2);
quant_sig = quant_levels(idx)';
```

---

## (e) Plot All Signals Using `subplot`

```matlab
figure;

subplot(2,2,1);
plot(analog_t, sig);
title('Analog Signal in Time Domain');
xlabel('Time (s)');
ylabel('Amplitude');

subplot(2,2,2);
plot(f_axis, sig_fft_shifted);
title('Analog Signal in Frequency Domain');
xlabel('Frequency (Hz)');
ylabel('Magnitude');

subplot(2,2,3);
stem(samp_t, samp_sig);
title('Sampled Signal in Time Domain');
xlabel('Time (s)');
ylabel('Amplitude');

subplot(2,2,4);
stairs(samp_t, quant_sig);
title('Quantized Signal (3-bit ADC)');
xlabel('Time (s)');
ylabel('Amplitude');
```

---

Let me know if you want a PDF version or explanations included as comments.
