# Oversample

possible to select 1-1024 oversampling for ADC12
and 1-256 for ADC4

The ovesample will collect 1-1024(256) sample and add them together. Then a rigth shift is managed. This can increase a resolution of adc. 
But it will increase a time needed for one final sample. 

## Regulvar overampling mode

Set ho oversampling mode is handled when paused by injected conversion. 

### Continuous mode
  Ovesampling result is maintaind and continue after injected conversion

### resumed mode

The oversampling starts from beginning when interrupted by injected conversion
