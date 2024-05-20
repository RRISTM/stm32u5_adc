# ADC overrun

On the ADC can offuc a overrun condition. 
That ADC converted new value but the previous was not read. 
This can easely happen in scan mode without DMA. 

The for this we can set two behaviours

* Overrrun data preserved
* Overrun data overwritten

## Overrun data preserved

The old data a re kept in ADC registers.
The new data are lost

## Overrrun data overwritten

The old data are lost 
New data are preserved

