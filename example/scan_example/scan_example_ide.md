# Scan ADC - CubeIDE


1. Add variables for vbat and vrefint

```c
/* USER CODE BEGIN PV */
volatile uint16_t value;
volatile int32_t temperature;
volatile uint16_t vbat;
volatile uint16_t vrefint;
/* USER CODE END PV */
```




2. Read the ADC for new values


 ```c
  /* USER CODE BEGIN WHILE */
  while (1)
  {
	  HAL_ADC_Start(&hadc1);
	  HAL_ADC_PollForConversion(&hadc1, 0xFFFFFFFF);
	  value= HAL_ADC_GetValue(&hadc1);
	  temperature =__HAL_ADC_CALC_TEMPERATURE(hadc1.instance,3300,value,ADC_RESOLUTION_14B);
	  HAL_ADC_PollForConversion(&hadc1, 0xFFFFFFFF);
	  vbat= HAL_ADC_GetValue(&hadc1);
	  HAL_ADC_PollForConversion(&hadc1, 0xFFFFFFFF);
	  vrefint= HAL_ADC_GetValue(&hadc1);
    /* USER CODE END WHILE */

```

3. Start debug
4. chack results in live watch


5. You can try to disable Low power Auto wait. And check the results