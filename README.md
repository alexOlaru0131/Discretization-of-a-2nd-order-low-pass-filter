# Discretization-of-a-2nd-order-low-pass-filter-using-STM32

In this project I simulated the characteristics of a 2nd order low pass filter that uses only capacitors and resistors by discretizing it's transfer function using the Tustin method.

The transfer function in "s" domain is:

![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/H_FTJ.png)

which after discretization, in "z" domain it becomes:

![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/H_FTJ_t.png)

I placed it in the z^-1 form especially to get the parameters.

After that, I ran a simulation on Simulink to see what would be the result:
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/Simulink.png)
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/plot_Simulink.png)

It's a little bit of oversampling, but it's not a problem for our hardware part.

For the hardware part:
The filter was made using: an operational amplifier LM324N which didn't need differential power supply, 2x 10kOhms resistors for R1 and R2, 2x 100kOhms resistors for RA and RB, 4.7 microFarad capacitor for C1 and 1 microFarad capacitor for C2. It was all built on a breadboard:
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/byytP.png)
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/Filter.jpg)
After I've connected the input signal (sine wave) and the oscilloscope, I got the following result:
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/Filter_output.jpg)

