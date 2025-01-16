
#include "DAVE.h"
#include "FREERTOS/task.h"
#include "FREERTOS/semphr.h"

#define PARK_SPACES 5

extern void initialise_monitor_handles(void);
uint32_t echo_in_counter, echo_out_counter, task_timer_counter;
uint32_t last_distance_in = 5;
uint32_t last_distance_out = 5;
uint8_t parked_cars = 0;

SemaphoreHandle_t xSemaphore;
QueueHandle_t xQueue;

void ProcessingTask(void *pvParameters);
void CommunicationTask(void *pvParameters);

int main(void)
{
  initialise_monitor_handles();
  DAVE_STATUS_t status;

  status = DAVE_Init();

  if (status != DAVE_STATUS_SUCCESS)
  {
	  printf("DAVE APPs initialization failed\n");

	  while(1U);
  }
  printf("Start\n");
  TIMER_Start(&TIMER_ECHO_IN);
  TIMER_Start(&TIMER_ECHO_OUT);

  xSemaphore = xSemaphoreCreateBinary();
  xQueue = xQueueCreate(5, sizeof(uint8_t));

  xTaskCreate(ProcessingTask, "Processing Task", 200, NULL, 2, NULL);
  xTaskCreate(CommunicationTask, "Communication Task", 200, NULL, 1, NULL);

  vTaskStartScheduler();

  while(1U);
}

void ProcessingTask(void *pvParameters)
{
    uint32_t start_time, end_time;
    task_timer_counter = 0;
	while (1)
	{
        start_time = task_timer_counter;
		check_entrance();
		check_exit();
		update_leds();

		end_time = task_timer_counter;

        printf("ProcessingTask duration: %lu us\n", (end_time - start_time)*1000);

		vTaskDelay(pdMS_TO_TICKS(100));
	}
}

void CommunicationTask(void *pvParameters)
{
    uint8_t occupied_spaces;
    char message[100];

    while (1)
    {
        if (xQueueReceive(xQueue, &occupied_spaces, portMAX_DELAY) == pdPASS)
        {
        	printf("occupied_spaces = %lu\n", occupied_spaces);
            sprintf(message, "Free spaces: %d\n", (PARK_SPACES - occupied_spaces));
            UART_Transmit(&UART_BLUETOOTH, (uint8_t *)message, strlen(message));
            if(occupied_spaces == PARK_SPACES)
            {
            	sprintf(message, "Entrance blocked!\n");
            	printf("Generated message: %s", message);
            	vTaskDelay(pdMS_TO_TICKS(10));
                UART_Transmit(&UART_BLUETOOTH, (uint8_t *)message, strlen(message));
            }
        }
    }
}

void check_entrance(void)
{
	uint32_t pulse_start = 0, pulse_stop = 0;
	echo_in_counter = 0;

	while (DIGITAL_IO_GetInput(&ECHO_IN) == 0);
	pulse_start = echo_in_counter;
	while (DIGITAL_IO_GetInput(&ECHO_IN) == 1 && (echo_in_counter - pulse_start) < 3);
	pulse_stop = echo_in_counter;

	printf("distance_in = %lu\n", pulse_stop - pulse_start);
//	printf("distance_in = %lu\n", echo_in_counter);

	if ((pulse_stop - pulse_start) < 2 && last_distance_in >= 2)
	{
		printf("\nCar In detected\n");
        if (parked_cars < PARK_SPACES)
        {
        	parked_cars++;
			xQueueSend(xQueue, &parked_cars, portMAX_DELAY);
        }
	}

	last_distance_in = pulse_stop - pulse_start;
}

void check_exit(void)
{
	uint32_t pulse_start = 0, pulse_stop = 0;
	echo_out_counter = 0;

	while (DIGITAL_IO_GetInput(&ECHO_OUT) == 0);
	pulse_start = echo_out_counter;
	while (DIGITAL_IO_GetInput(&ECHO_OUT) == 1 && (echo_out_counter - pulse_start) < 3);
	pulse_stop = echo_out_counter;

	printf("distance_out = %lu\n", pulse_stop - pulse_start);
//	printf("distance_out = %lu\n", echo_out_counter);

	if ((pulse_stop - pulse_start) < 2 && last_distance_out >= 2)
	{
		printf("\nCar Out detected\n");
		if (parked_cars > 0) {
			parked_cars--;
            xQueueSend(xQueue, &parked_cars, portMAX_DELAY);
		}
	}
	last_distance_out = pulse_stop - pulse_start;
}

void update_leds(void)
{
	if(parked_cars == PARK_SPACES)
	{
		DIGITAL_IO_SetOutputHigh(&RED_LED);
		DIGITAL_IO_SetOutputLow(&GREEN_LED);
	}
	else
	{
		DIGITAL_IO_SetOutputHigh(&GREEN_LED);
		DIGITAL_IO_SetOutputLow(&RED_LED);
	}
}

void EchoInPulse(void)
{
	echo_in_counter++;
	task_timer_counter++;
}

void EchoOutPulse(void)
{
	echo_out_counter++;
}
