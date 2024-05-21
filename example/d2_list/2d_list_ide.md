

1. In main.c create adc_buffer2 and external queueu

```c
/* USER CODE BEGIN PV */
volatile uint16_t value;
volatile int32_t temperature;
volatile uint16_t vbat;
volatile uint16_t vrefint;

uint16_t adc_buffer[12288];
uint16_t adc_buffer2[4096];

extern DMA_QListTypeDef YourQueueName;
extern DMA_QListTypeDef YourQueueName2;
/* USER CODE END PV */
```

2. Add queue init, ling queue and start queue

```c
  /* USER CODE BEGIN 2 */
  MX_YourQueueName_Config();
  MX_YourQueueName2_Config();
  HAL_DMAEx_List_LinkQ(&handle_GPDMA1_Channel12, &YourQueueName2);
  HAL_DMAEx_List_Start(&handle_GPDMA1_Channel12);
  HAL_DMAEx_List_LinkQ(&handle_GPDMA1_Channel1, &YourQueueName);
  HAL_DMAEx_List_Start(&handle_GPDMA1_Channel1);
  HAL_ADC_Start_DMA(&hadc1, adc_buffer, 12288);
  /* USER CODE END 2 */
```

3. In linklist.c add buffers

```c
/* USER CODE BEGIN PM */
uint32_t gpio_buffer[2]={0x00000080,0x00800000};// to toggle with PB7
extern uint16_t adc_buffer[];
extern uint16_t adc_buffer2[];
/* USER CODE END PM */
```

4. Correct wrong MX generation

```c
/* USER CODE BEGIN PM */
uint32_t gpio_buffer[2]={0x00000080,0x00800000};// to toggle with PB7
extern uint16_t adc_buffer[];
extern uint16_t adc_buffer2[];

DMA_NodeTypeDef YourNodeName;
DMA_QListTypeDef YourQueueName;

/* USER CODE END PM */
```


```c
HAL_StatusTypeDef MX_YourQueueName_Config(void)
{
  HAL_StatusTypeDef ret = HAL_OK;
  /* DMA node configuration declaration */
  DMA_NodeConfTypeDef pNodeConfig;

  /* Set node configuration ################################################*/
  pNodeConfig.NodeType = DMA_GPDMA_LINEAR_NODE;
  pNodeConfig.Init.Request = DMA_REQUEST_SW;
  pNodeConfig.Init.BlkHWRequest = DMA_BREQ_SINGLE_BURST;
  pNodeConfig.Init.Direction = DMA_MEMORY_TO_MEMORY;
  pNodeConfig.Init.SrcInc = DMA_SINC_INCREMENTED;
  pNodeConfig.Init.DestInc = DMA_DINC_FIXED;
  pNodeConfig.Init.SrcDataWidth = DMA_SRC_DATAWIDTH_WORD;
  pNodeConfig.Init.DestDataWidth = DMA_DEST_DATAWIDTH_WORD;
  pNodeConfig.Init.SrcBurstLength = 1;
  pNodeConfig.Init.DestBurstLength = 1;
  pNodeConfig.Init.TransferAllocatedPort = DMA_SRC_ALLOCATED_PORT0|DMA_DEST_ALLOCATED_PORT0;
  pNodeConfig.Init.TransferEventMode = DMA_TCEM_BLOCK_TRANSFER;
  pNodeConfig.TriggerConfig.TriggerMode = DMA_TRIGM_SINGLE_BURST_TRANSFER ;
  pNodeConfig.TriggerConfig.TriggerPolarity = DMA_TRIG_POLARITY_RISING;
  pNodeConfig.TriggerConfig.TriggerSelection = GPDMA1_TRIGGER_GPDMA1_CH0_TCF;
  pNodeConfig.DataHandlingConfig.DataExchange = DMA_EXCHANGE_NONE;
  pNodeConfig.DataHandlingConfig.DataAlignment = DMA_DATA_RIGHTALIGN_ZEROPADDED;
  pNodeConfig.SrcAddress = (uint32_t)gpio_buffer;
  pNodeConfig.DstAddress = &GPIOB->BSRR;
  pNodeConfig.DataSize = 8;

  /* Build YourNodeName2 Node */
  ret |= HAL_DMAEx_List_BuildNode(&pNodeConfig, &YourNodeName);

  /* Insert YourNodeName2 to Queue */
  ret |= HAL_DMAEx_List_InsertNode_Tail(&YourQueueName, &YourNodeName);

  ret |= HAL_DMAEx_List_SetCircularMode(&YourQueueName);

   return ret;
}
```

Now the ADC data are decoded and data from temp sensor are sotred in adc_buffer2