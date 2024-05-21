# Linked list dma CubeMX

We will create a list queue with one node which willl write data to GPIO register to toggle with led

1. Set GPIO PB2 as output
2. Set GPDMA1 set `channel 1` as **linked list**
2a. Set `Execution Mode `to **Circular** 
3. Go to LINKEDLIST periphery
4. Add new list
5. Select Queueu, set it to **curcular**
6. Set channel as **GPDMA**
7. Set Loop node as **YourNodeName**
8. Select `YourNodeName`

9.  Set `Source address increment after transfer `to **ENABLE**
10. Set `Source data width` to **Word**
11. Set `Destination data width` to **Word**
12. Set `trigger configuration` to **rising edge**
13. Set `Trigger mode` to **single/burst**
14. Set `Trigger selection` to GPDMA used for ADC (CH0)
15. Set `Source address` to **(uint32_t)gpio_buffer**

```c
(uint32_t)gpio_buffer
```

16. Set `Destination address` to **&GPIOB->BSRR**

```
&GPIOB->BSRR
```

17. Set `data size` to **8** 

```c
8
```

18. Generate code