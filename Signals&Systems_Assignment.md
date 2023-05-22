1. Continuous-time Signals : Sketch the following continuous-time signals in separate figures over the specified interval. For a complex valued signal, sketch magnitude and phase in the same figure separately.
   
   (a) For t ∈ [−10π 10π]
       x(t) = sin(πt) / πt for t ≠ 0
              = 1                  for t = 0

```matlab
%%%%%%%%%%%%%%%%%% Sinc Function %%%%%%%%%%%%%%%%%%%%%%%%%%
t = -10*pi:0.001:10*pi;
y = sin(pi*t)./(pi*t);
y(t==0) = 1;
title("Sinc Function")
plot(t,y)
xlabel("Time")
ylabel("Amplitude")
```

    b) x(t) = ∏(t) for t ∈ [−2 2]. The rect function is defined as 
        ∏ (t) = 0 for |t| >1/2

            and 1 for |t| < 1/2.

```matlab
x = -2:0.002:2;
y = zeros(1, length(x));
y(abs(x)<=0.5) = 1;
plot(x,y)
title("Rectangular Function")
xlabel("Time")
ylabel("Amplitude")
```

   (c) For 5 time periods
        x(t) = A1 cos(2πf1t + θ1) + A1 cos(2πf2t + θ1)
        Take A1 = 1,A2 = 2,f1 = 100 Hz,f2 = 500 Hz,θ1 = π/6 and θ2 = π/4.

```matlab
A1 = 1;
A2 = 2;
f1 = 100;
f2 = 500;
t1 = pi/6;
t2 = pi/4;
t = -0.025:0.0001:0.025;
x = cos(2*pi*f1*t+t1) + cos(2*pi*f2*t+t2);
plot(t,x)
xlabel("Time")
ylabel("Amplitude")
```

(d) x(t) = u(t) - u(t - 4) for t ∈ [0 10] where u(t) is the unit step signal.

```matlab
t = 0:0.001:10;
y = ones(1, length(t));
y(t>4) = 0;
plot(t,y)
title("u(t)-u(t-4)")
xlabel("Time")
ylabel("Amplitude")
```

(e) x(t) = (0.5)<sup>t</sup> e<sup>jπt/2</sup>  for t ∈ [-10 10] .

```matlab
t = -10:0.001:10;
x = 0.5^.t .* exp(j*pi*t/2);
plot(t,x);
xlabel("Time");
ylabel("Amplitude");
```
