# Gain compensation

ADC1/2

It will correct the gain. 

Basially it will multiply the ADC result with set value

DATA = DATA_adc_result * (GCOMPCOEFF /4096)


Must be enabled by HAL/LL function by default disabled
