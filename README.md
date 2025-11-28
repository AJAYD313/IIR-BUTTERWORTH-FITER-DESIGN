# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN

## AIM: 

 To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
clc ;
close ;
wp=input('Enter the pass band frequency (Radians )= ' );
ws=input('Enter the stop band frequency (Radians )= ' );
alphap=input( ' Enter the pass band attenuation (dB)=' );
alphas=input( ' Enter the stop band attenuation(dB)=' );
T=input('Enter the Value of sampling Time=');
//Pre warping- Bilinear Transformation
omegap=(2/T)*tan(wp/2);
disp(omegap,'omegap=');
omegas=(2/T)*tan(ws/2);
disp(omegas,'omegas=');
//Order of the filter
N=log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegas/omegap));
disp(N,'N=');
N=ceil(N);
disp(N,'Round off value of N=');
//Cut off frequency
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N)));
disp(omegac,'omegac=');
disp('Normalised Analog LPF Transfer function H(S)=');
hs_Normalised = analpf(N,'butt',[0,0],1);
disp(hs_Normalised);
disp('Analog LPF Transfer function H(S)=');
hs= analpf(N,'butt',[0,0],omegac);
disp(hs);
z=poly(0,'z');//Defining variable z
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))// Bilinear Transformation
disp('Digital LPF Transfer function H(Z)=');
disp(Hz);
HW=frmag(Hz,512); // Frequency response
w=0:%pi/511:%pi ;
plot(w/%pi,abs(HW));
xlabel(' Normalized Digital Frequency w');
ylabel('Magnitude ');
title(' Frequency Response of Butterworth IIR LPF');



## PROGRAM (HPF): 
clc;
close;
wp = input('Enter the pass band frequency (Radians )= ');
ws = input('Enter the stop band frequency (Radians )= ');
alphap = input('Enter the pass band attenuation (dB)= ');
alphas = input('Enter the stop band attenuation (dB)= ');
T = input('Enter the Value of sampling Time= ');

// Pre-warping (Bilinear Transformation)
omegap = (2/T) * tan(wp/2);
disp(omegap, 'omegap=');
omegas = (2/T) * tan(ws/2);
disp(omegas, 'omegas=');

// Order of the filter
N = log10(((10^(0.1*alphas))-1) / ((10^(0.1*alphap))-1)) / (2*log10(omegas/omegap));
disp(N,'N=');
N = ceil(N);
disp(N,'Round off value of N=');

// Cut off frequency
omegac = omegap / (((10^(0.1*alphap))-1)^(1/(2*N)));
disp(omegac,'omegac=');

// Normalised Analog LPF Transfer function
disp('Normalised Analog LPF Transfer function H(S)=');
hs_Normalised = analpf(N,'butt',[0,0],1);
disp(hs_Normalised);

// Analog LPF Transfer function
disp('Analog LPF Transfer function H(S)=');
hs = analpf(N,'butt',[0,0],omegac);
disp(hs);

s = poly(0,'s');
hpf_s = horner(hs, omegac/s);   // substitute s → omegac/s
disp('Analog HPF Transfer function H(S)=');
disp(hpf_s);

// Bilinear Transformation to Digital
z = poly(0,'z'); // Defining variable z
Hz = horner(hpf_s,(2/T)*((z-1)/(z+1))); 
disp('Digital HPF Transfer function H(Z)=');
disp(Hz);

// Frequency Response
HW = frmag(Hz,512);
w = 0:%pi/511:%pi;
plot(w/%pi, abs(HW));

xlabel(' Normalized Digital Frequency w');
ylabel('Magnitude');
title(' Frequency Response of Butterworth IIR HPF');


## OUTPUT (LPF) : 
![WhatsApp Image 2025-11-25 at 16 03 15_621e7eb5](https://github.com/user-attachments/assets/fcdc68f5-a6f8-47af-8778-f4da1c682ceb)

## OUTPUT (HPF) : 
![WhatsApp Image 2025-11-25 at 16 22 41_32c6e219](https://github.com/user-attachments/assets/8fa54307-6e86-439a-ae30-bf98b79070b5)

## RESULT: 
Thus, design of Butterworth Low pass and high pass IIR filter waveforms were plotted and output wasverified.
