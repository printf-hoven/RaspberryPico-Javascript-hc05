picow_hc05.uf2 is the compiled file that should be copied to the raspberry picow as explained in the video below. The board MUST be a PicoW - wireless, any version, because the LED configured is the LED on the PicoW board.

Write to us for any modifications and customizations - our contact can be found in the youtube video linked below, or the website https://hoven.in

Youtube Explanation: https://youtu.be/zgtEQqa-_Lg

 ========self notes for future needs====================
 
    case UART_GOTCHAR: {

      uint8_t data[] = { 0, '\n' };

      // only one byte expected, containing 0 or 1
      // let's clear the buffer, keep the last byte
      while (uartx.has_byte()) {

        data[0] = uartx.get_byte();

#ifdef HDEBUG
        printf("Byte received: %u ('%c')\n", data[0], data[0]);
#endif

      }

      if (data[0] == '2') {
       
       // this is a query of the state
        data[0] = cyw43_arch_gpio_get(CYW43_WL_GPIO_LED_PIN) ? '1' : '0';
       
      }

      cyw43_arch_gpio_put(CYW43_WL_GPIO_LED_PIN, '1' == data[0]);

      // echo back
      uartx.write_bytes(data, 2);
    }
                     break;
