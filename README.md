# FDM
## AIM
To implement Frequency Division Multiplexing (FDM) for six different message signals using Scilab, generate the multiplexed signal, and perform demultiplexing to recover all the original message signals. The experiment also includes plotting the message signals, multiplexed signal, and demultiplexed signals.

## APPARATUS REQUIRED
Computer System
Scilab Software

## ALGORITHM
Set sampling frequency, time duration, and time vector.
Generate six message signals with different frequencies.
Assign six different carrier frequencies.
Perform DSB-SC modulation by multiplying each message with its carrier.
Add all modulated signals to form the multiplexed FDM signal.
For each channel, multiply the multiplexed signal with the same carrier (demodulation).
Apply a low-pass filter to extract the recovered message.
Plot message signals, multiplexed signal, and recovered s ignals.

## THEORY
Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a different carrier frequency. Each message modulates its own carrier, and all modulated signals are added to form the multiplexed signal. Since the carrier frequencies are well separated, the signals do not overlap in the frequency domain.

At the receiver, each signal is recovered by multiplying the multiplexed signal with the corresponding carrier (coherent demodulation) and passing it through a low-pass filter to extract the original baseband message. FDM is widely used in radio broadcasting, telephone systems, and cable TV.

## Program
```
clc;
clear;
close;

fs = 20000;
t = 0:1/fs:0.02;

fm = [100,150,200,250,300,350];
m = [];

for i = 1:6
    m(i, :) = sin(2*%pi*fm(i)*t);
end

fc = [2000, 3000, 4000, 5000, 6000, 7000];

fdm = zeros(1, length(t));
for i = 1:6
    c = cos(2*%pi*fc(i)*t);
    s = m(i, :) .* c;
    fdm = fdm + s;
end

scf(1);
clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, m(i, :));

end

scf(2);
clf;
plot(t, fdm);

demod = [];
for i = 1:6
    c = cos(2*%pi*fc(i)*t);
    x = fdm .* c;
    h = ones(1,100)/100;
    y = conv(x, h, 'same');
    demod(i, :) = y;
end

scf(3);
clf;
for i = 1:6
    subplot(6,1,i);
    plot(t, demod(i, :));
end

disp("FDM and Demultiplexing completed successfully!");
```

## Output

<img width="756" height="624" alt="image" src="https://github.com/user-attachments/assets/08c66968-5512-4659-ac42-c7be83e72073" />


<img width="760" height="626" alt="image" src="https://github.com/user-attachments/assets/90f9eb26-cd9f-499f-84ce-779d61ee7b2f" />


<img width="765" height="622" alt="image" src="https://github.com/user-attachments/assets/5c14dc1f-c495-45c8-a1fe-72bd16de9442" />

## Tabulation
![WhatsApp Image 2025-11-26 at 3 47 23 PM](https://github.com/user-attachments/assets/4e644e22-7c47-40fd-b8b4-2840ed569caa)

## Result
Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.
