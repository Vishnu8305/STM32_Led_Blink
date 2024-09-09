For your detailed README explanation with the steps you provided, here’s a draft that goes in-depth into the STM32 programming process:

---

# STM32_LED_Blink Project

Welcome to the STM32 LED Blink project! To start with STM32 programming, it is essential to understand how to read and interpret the **datasheet** of the STM32 microcontroller you are working with. This project demonstrates a basic LED on/off functionality using STM32.

## Steps Involved to Make the Code Work:

### STEP 1: Identifying the Communication Bus

- The first step is to identify the **bus** responsible for interacting with the peripheral (in this case, the **GPIO** that controls the LED). STM32 microcontrollers have multiple buses that connect various peripherals, and for GPIO, we often use the **RCC (Reset and Clock Control)** to enable the peripheral's clock.

- For this project, we use the **RCC_AHB2ENR** register. This register is located on the **Advanced High-Performance Bus (AHB2)**. The **AHB2** bus provides the communication channel between the main memory and the GPIO ports (e.g., GPIOA, GPIOB).

- **Tip**: You can find this information in the **STM32 reference manual** or your development board's documentation. The following image shows how the bus interacts with different peripherals:

![image](https://github.com/user-attachments/assets/334586df-b0c8-4dfe-a4cd-649f01688893)

### STEP 2: Memory Mapping

- Once you've identified the bus, it's time to **find the base address** of the **RCC** in the STM32 memory map. The memory map provides details about which address is assigned to which peripheral.

- For example, in this project, the **RCC base address** is `0x40021000`. We are specifically interested in the **RCC_AHB2ENR** register, which has an **offset of 0x4C**. So, the full address for enabling the GPIOA peripheral clock will be:

  
      Base address: 0x40021000
      Offset:       0x4C
      Final address: 0x4002104C
      

- **Why is this important?** Understanding memory mapping is crucial because it tells you exactly where to go in the memory to interact with the peripherals. Here's an example of the RCC memory map:

![image](https://github.com/user-attachments/assets/c6519c0c-80f1-4370-a80a-867a1abc3c7e)

### STEP 3: Enabling the GPIOA Clock

- Now that you have the final address, the next step is to write code to enable the GPIOA clock using the RCC_AHB2ENR register. In this register, setting **bit 0** will enable the clock for GPIOA.

      
      uint32_t *pClkCtrlReg = (uint32_t*)0x4002104C;  // RCC_AHB2ENR register address
      *pClkCtrlReg |= (1 << 0);                       // Set bit 0 to enable GPIOA clock

### STEP 4: Configuring the GPIO Pins

- After enabling the GPIOA clock, the next step is to configure the **GPIO mode** for **PA0** and **PA15** as output pins. This is done by accessing the **GPIOA_MODER** register.

- The **GPIOA_MODER** register has two bits for each pin to define its mode. Setting the mode to **01** configures the pin as an output.

      uint32_t *pPortAModeReg = (uint32_t*)0x48000000;  // GPIOA_MODER register address
      *pPortAModeReg &= ~(3 << 0);                      // Clear mode bits for PA0
      *pPortAModeReg |= (1 << 0);                       // Set PA0 to output mode
      *pPortAModeReg &= ~(3 << 30);                     // Clear mode bits for PA15
      *pPortAModeReg |= (1 << 30);                      // Set PA15 to output mode

  **Memory Mapping Reference for GPIOA:**

  ![image](https://github.com/user-attachments/assets/b9f21264-ab5b-4f2b-8474-004b5ed48b5a)


### STEP 5: Controlling the Output (Turning the LEDs ON)

- With PA0 and PA15 configured as output pins, you can now turn the LEDs on by setting the corresponding bits in the **GPIOA_ODR (Output Data Register)**.

      uint32_t *pPortAOutReg = (uint32_t*)0x48000014;  // GPIOA_ODR register address
      *pPortAOutReg |= (1 << 0);                       // Set PA0 high to turn on LED
      *pPortAOutReg |= (1 << 15);                      // Set PA15 high to turn on LED

  ![image](https://github.com/user-attachments/assets/190462f2-8b1f-418e-9363-2f2d661831c6)
  ![image](https://github.com/user-attachments/assets/f55a0091-b2fe-4d6c-a07d-086a779efdae)
  ![image](https://github.com/user-attachments/assets/0bf1ca3d-c282-4a7f-8ba2-1a4128285ea5)




### STEP 6: Infinite Loop

- Finally, the program enters an **infinite loop** to keep the LEDs on.

      while(1);  // Keep the program running
      

### Summary

In this project, we demonstrated how to configure GPIO pins as outputs and control them to turn on LEDs connected to PA0 and PA15. We also learned how to enable the GPIO peripheral clock using the RCC_AHB2ENR register.

---

This detailed README will help beginners understand the step-by-step process involved in configuring GPIO pins on the STM32 and provide useful references to memory mapping and register configuration. Would you like to add anything else?
