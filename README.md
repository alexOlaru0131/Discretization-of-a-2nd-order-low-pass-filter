# Discretization-of-a-2nd-order-low-pass-filter-using-STM32

In this project I simulated the characteristics of a `2nd order low pass filter` that uses only `capacitors` and `resistors` by discretizing it's transfer function using the `Tustin method`.

The transfer function in `continuous domain` is:

![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/H_FTJ.png)

which after discretization, in "z" domain it becomes:

![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/H_FTJ_t.png)

I placed it in the z^-1 form especially to get the parameters.

After that, I ran a simulation on Simulink to see what would be the result:
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/Simulink.png)
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/plot_Simulink.png)

It's a little bit of oversampling, but it's not a problem for our hardware part.

For the hardware part:
The filter was made using: an operational amplifier LM324N which didn't need differential power supply, 2x 10kOhms resistors for R1 and R2, 2x 100kOhms resistors for RA and RB, 4.7 microFarad capacitor for C1 and 1 microFarad capacitor for C2. The power supply for the whole circuit (including the board) cam be adjusted up to 24V, but I chose 5V to compare directly to the maximum possible output of the microcontroller.

![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/byytP.png)
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/Filter.jpg)
After I've connected the input signal (sine wave) and the oscilloscope, I got the following result:
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/Filter_output.jpg)

For the simulation on the microcontroller (STM32 NUCLEO-G071RB) , I used a timer (TIM16) with it's prescaler adjuested to get 779 ms (to cover the whole sampling period) and for it's interrupt routine to not encounter any possible delays on the calculations. The values from the transfer functions were initialized as floats to get a precise result. In the routine I read the input with the ADC, calculate the output and transport it to the oscilloscope using the DAC. After connecting the oscilloscope, I got the following result:
![alt text](https://github.com/alexOlaru0131/Discretization-of-a-2nd-order-low-pass-filter-using-STM32/blob/main/Photos/STM_output.jpg)

The output differ a little because of the possible delays on the microcontroller or for a so low sampling time that physically almost can't be achieved on a microcontroller like this, but they look mostly the same. The discrete output can be seen too.
