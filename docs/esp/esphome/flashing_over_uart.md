# Flashing over UART

## Procedure to Connect ESP32 via UART to USB Adapter

1. **Prepare Components**: ESP32 board, USB-to-UART adapter, and jumper wires.
2. **Connections**:
   - Connect the adapter's **TX** to ESP32's **RX**.
   - Connect the adapter's **RX** to ESP32's **TX**.
   - Connect **GND** on the adapter to **GND** on the ESP32.
   - Connect **VCC** (3.3V or 5V, depending on your ESP32, usually 3.3V) to the adapter's power pin.
3. **Connect to PC**: Plug the USB adapter into your computer.
4. **Test Connection**: Open a terminal and run the command:
   ```bash
   picocom -b 115200 /dev/ttyUSB0
    ```

5. **Enter Programming Mode**:
   - Press and hold the **BOOT** button on the ESP32.
   - While holding **BOOT**, press and release the **EN/RESET** button.
   - Release the **BOOT** button.

   You should see the following logs in the terminal:
   ```
   rst:0x1 (POWERON_RESET),boot:0x3 (DOWNLOAD_BOOT(UART0/UART1/SDIO_REI_REO_V2))
   waiting for download
   ```
6. Flash e.g. from docker

    ```
    root@sw-A5-K1:/config# esphome run --device /dev/ttyUSB0 esp32-test.yaml
    ```
7. Reset with click **EN/RESET** button after all when seeing that
    ```
    Hard resetting via RTS pin...
    INFO Successfully uploaded program.
    INFO Starting log output from /dev/ttyUSB0 with baud rate 115200
    ```
