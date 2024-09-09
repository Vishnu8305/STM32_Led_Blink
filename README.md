# STM32_Led_Blink
TO start with the STM32 programing you  need to understand the given data sheet to write a program here is the basic code project for the STM32 with led on lets get to it

Steps Involved to make the code work are given as below :
  STEP1:
       -> You need to find the bus which is intera cting to your periferals as of for me the bus which is making communocation is RCC_AHB2ENR  you can get thes in your desiered board as which board you are using to            make your project  as ypu can find that by viewing that board arcitecture as in the archetecture you can find the which bus is interacting with the periferals .
        ![image](https://github.com/user-attachments/assets/34da58c7-b672-4d6f-9125-892f3db9b317)
     -> after identifing the which is interacting with you go to the page of the memory mapping and find the  base address  of the rcc  and then noteit down and also note the Address offset and multiply them and             note the results   
     ![image](https://github.com/user-attachments/assets/9e416625-ed87-4929-81ab-6a5d6d331ccc)  ![image](https://github.com/user-attachments/assets/20998375-97d8-47a8-9db6-9219ec66781a)
     

