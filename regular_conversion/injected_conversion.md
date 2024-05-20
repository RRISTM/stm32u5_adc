# Injected conversion

The ADC1/2 have up to also seqeuncer and up 4 injected itens can be configured. 

Compared to regular channels the injected channels have own data registers but they dont have DMA cappability.

 ## Configuration

 ### Left but shift

 similar to regular channels it will shift sample resul to the left

 ### Injected oversampling 
 
 Same as regular channels oversamp[ling 1-1024

 ### Number of conversions

 The seqeunce length from 1-4

 ### Trigger

Injected conversion can be triggered

* Triggered by software
* Triggered by HW periphery 

### Injected conversion mode

* None
* Discontinous mode
* Auto injected mode

#### None

The injected conversion start on SW trigger or by HW trigger 

#### Discontinous mode

Each injected channel trigger will start 1 injected channel conversion

#### Auto injected mode

the injection sequence started automatically after regular conversion scan


