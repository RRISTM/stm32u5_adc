# DMA 2D list

Based on 
(Link)[https://rristm.github.io/tomas_materials_v2/RRISTM/stm32u5_workshop/master/5_gpdma_handson_2d_address_intro.md/2]

1. Open MX 
2. Set GPDMA1 set `channel 12` as **linked list**
3. Set `Execution Mode `to **Circular** 
4. Go to LINKEDLIST periphery
5. Add new list
6. Select Queue, set it to **curcular**
7. Set Queue name as **YourQueueName2**
8. Set channel as **GPDMA**
9. Set Loop node as **YourNodeName2**
10. Select `YourNodeName`
11. Rename `YourNodeName` to **YourNodeName2**

12. Set `Source address increment after transfer `to **ENABLE**
13. Set `Source data width` to **Word**
14. Set `Destination address increment after transfer `to **ENABLE**
15. Set `Destination data width` to **Word**
16. Set `trigger configuration` to **rising edge**
17. Set `Trigger mode` to **single/burst**
18. Set `Trigger selection` to GPDMA used for ADC (CH0)
19. Set `2D addressing` to `ENABLE`
20. Set `source data offset` to **4**

21. Set `Source address` to **(uint32_t)adc_buffer**



```c
(uint32_t)adc_buffer
```

16. Set `Destination address` to **adc_buffer2**

```
adc_buffer2
```

17. Set `data size` to **(4096*2)** 

```c
(4096*2)
```

18. Generate code