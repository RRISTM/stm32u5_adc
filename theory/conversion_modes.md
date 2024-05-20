# ADC (regular) conversion modes

In this part we will focus on three options:
* SCAN mode
* CONT mode (continuous)
* DISC mode (discontinous)

# Single conversion

Setup:
* SCAN = 0 
* CONT = 0
* DISC = 0

Only one conversion is performed then adc is stopped

![single conversion](./img/single_conversion.svg)

# Single continuous conversion

Setup:
* SCAN = 0 
* CONT = 1
* DISC = 0

the same channel is continously samples, adc newer stops


![continuous conversion](./img/continuous_conversion.svg)


# Scan Conversion Mode

Setup:
* SCAN = 1
* CONT = 0
* DISC = 0

A scheduler is used to configue order of conversions. 
ADC 1/2 up to 16 item seqeunce


![scan conversion](./img/scan_conversion.svg)

# Continuous Scan Conversion Mode

Setup:
* SCAN = 1 
* CONT = 1
* DISC = 0

Same as previous but repead the schedule


![continuous scan conversion](./img/continuous_scan_conversion.png)


# Discontinous Conversion Mode

Setup:
* SCAN = 1 
* CONT = 1
* DISC = 1

A mode when scan stop after set number of conversion in seqeunce and wait for new start/triffer. 

![discontinous conversion](./img/discontinous_conversion.svg)


