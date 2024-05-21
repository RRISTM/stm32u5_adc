# Linked list dma CubeIDE

1. Into `main.c` addcall to `MX_YourQueueName_Config()`

```c
  /* USER CODE BEGIN 2 */
  MX_YourQueueName_Config();
  HAL_ADC_Start_DMA(&hadc1, adc_buffer, 6);
  /* USER CODE END 2 */
```

2. In `linked_list.c` add a array to toggle with LED

```c
/* USER CODE BEGIN PM */
uint32_t gpio_buffer[2]={0x00000080,0x00800000};// to toggle with PB7
/* USER CODE END PM */

```

3. In `main.c` add a queue

```c
/* USER CODE BEGIN PV */
volatile uint16_t value;
volatile int32_t temperature;
volatile uint16_t vbat;
volatile uint16_t vrefint;

uint16_t adc_buffer[6];

extern DMA_QListTypeDef YourQueueName;
/* USER CODE END PV */
```

4. Link queue to GPDMA channel and start GPDMA

```c
  /* USER CODE BEGIN 2 */
  MX_YourQueueName_Config();
  HAL_DMAEx_List_LinkQ(&handle_GPDMA1_Channel1, &YourQueueName);
  HAL_DMAEx_List_Start(&handle_GPDMA1_Channel1);
  HAL_ADC_Start_DMA(&hadc1, adc_buffer, 6);
  /* USER CODE END 2 */
```

5. Increase the ADC buffer to **12288** to have trigger to CH1 in 1s. 

```c
/* USER CODE BEGIN PV */
volatile uint16_t value;
volatile int32_t temperature;
volatile uint16_t vbat;
volatile uint16_t vrefint;

uint16_t adc_buffer[12288];

extern DMA_QListTypeDef YourQueueName;
/* USER CODE END PV */
```

```c
  /* USER CODE BEGIN 2 */
  MX_YourQueueName_Config();
  HAL_DMAEx_List_LinkQ(&handle_GPDMA1_Channel1, &YourQueueName);
  HAL_DMAEx_List_Start(&handle_GPDMA1_Channel1);
  HAL_ADC_Start_DMA(&hadc1, adc_buffer, 12288);
  /* USER CODE END 2 */
  ```

  6. Compile and run