# ADC conversion management data mode 

This option will set how the adc results will be handled. 
there are four options:

* Regular  Conversion data stored in DR register only
* MDF mode
* DMA one shot mode
* DMA circular mode
  

## Regular  Conversion data stored in DR register only

The data from ADC conversion store in ADC DR

## MDF mode

The data from ADC conversion send to MDF filter

## DMA one shot mode

The ADC will generate a DMA requests during first scan seqeunce. 
If ADC is in continuous mode the rest of the scan seqeunce will not generate DMA reqqeunsts

## DMA circular mode

The ADC will generate DMA reqeust for every regular conversion

