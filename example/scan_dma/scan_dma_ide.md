# Continuous scan mode and dma - CubeIDE

1. Add adc buffer for DMA

```c
/* USER CODE BEGIN PV */
volatile uint16_t value;
volatile int32_t temperature;
volatile uint16_t vbat;
volatile uint16_t vrefint;

uint16_t adc_buffer[6];
/* USER CODE END PV */
```

2. Start the DMA and ADC

```c
  /* USER CODE BEGIN 2 */
  HAL_ADC_Start_DMA(&hadc1, adc_buffer, 6);
  /* USER CODE END 2 */
```

3. Remove poll reading from while loop
   
```c
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	  temperature =__HAL_ADC_CALC_TEMPERATURE(hadc1.instance,3300,adc_buffer[0],ADC_RESOLUTION_14B);
    /* USER CODE END WHILE */
```
