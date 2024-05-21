# Simple ADC - CubeIDE

1. Add variable for ADC data 
To PV section add a variable `value` where we read the value from ADC. 

```c
/* USER CODE BEGIN PV */
volatile uint16_t value;
/* USER CODE END PV */
```

2. Start ADC and read data

```c
/* USER CODE BEGIN WHILE */
while (1)
{
  HAL_ADC_Start(&hadc1);
  HAL_ADC_PollForConversion(&hadc1, 0xFFFFFFFF);
  value= HAL_ADC_GetValue(&hadc1);
  /* USER CODE END WHILE */
```

3. Compile and run the code. 
4. Add value to Live variables
5. try to head the device. 


## Conver ADC data

1. Add temperature variable to PV section
```c
/* USER CODE BEGIN PV */
volatile uint16_t value;
volatile int32_t temperature;
/* USER CODE END PV */
```

2. Add a conversion after ADC reading

```c
/* USER CODE BEGIN WHILE */
while (1)
{
  HAL_ADC_Start(&hadc1);
  HAL_ADC_PollForConversion(&hadc1, 0xFFFFFFFF);
  value= HAL_ADC_GetValue(&hadc1);
  temperature =__HAL_ADC_CALC_TEMPERATURE(hadc1.instance,3300,value,ADC_RESOLUTION_14B);
  /* USER CODE END WHILE */
```

3. Now we can add the `temperature` variable to live watch