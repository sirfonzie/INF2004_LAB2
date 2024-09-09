# LAB 2: GPIO and Digital Communication

**OBJECTIVES**
- To better understand and use library functions.
- Configuring GPIO as input and output
- Configuring UART communication.
- To setup a new blank project.

**EQUIPMENT** 
1.	A laptop that has the Pico C/C++ SDK installed
2.	Raspberry Pico W
3.	Micro-USB Cable
4.	F-F Jumper wire (at least 3)

> [NOTE]
> Only students wearing fully covered shoes are allowed in the SR6A lab due to safety.

## **INTRODUCTION** 

In this lab, our primary focus will be on the General Purpose Input/Output (GPIO) capabilities of the Raspberry Pi Pico. GPIO allows us to interact with various external components, such as LEDs, buttons, and sensors, by setting pins as __inputs__ or __outputs__ to read or write values to them. It's the foundational building block for many microcontroller-based projects. We will delve into Serial Communication, an essential communication protocol that aids in the seamless transfer of data between Picos. With these topics, we'll embark on a hands-on exploration to deepen our understanding of the Pico C SDK's capabilities including creating your own project from blank. Let's begin our journey!

## **DEFINES and MACROS** 

Preprocessor directives like defines and macros are often used when programming embedded systems to make the code more readable and easier to maintain.  In C programming, #define is a preprocessor directive used to create "macros." While they're often discussed interchangeably, #define is the mechanism, and the macro is the result. Macros can represent values or pieces of code and are a form of text substitution done __before compilation__. They're not true functions or variables, so they don't have types or memory allocations. Though they can make code more efficient, they might also introduce complexity or errors if not used cautiously.

```
#define PI 3.14159
#define MIN(a, b) ((a) < (b) ? (a) : (b))
```
In the above example, PI is a simple macro representing the value 3.14159, and MIN is a macro that computes the minimum of two values.

## **GPIO - INPUT** 

We will be building the [blink](https://github.com/raspberrypi/pico-examples/blob/master/pico_w/wifi/blink/picow_blink.c) sample code for the Pico W. This time, we have a better understanding of GPIO and what we need to do to configure an LED. Unfortunately, the user cannot use the button on the Pico W (its for boot select only). Now that we are using the Pico W together with the Maker board, we have access to three buttons. In this example, we will demonstrate how to use a button connected to GP20. These buttons are connected via a pull-up circuit, so they need to be configured accordingly.

The modified code, [picow_blink_button](picow_blink_button.c), configures GP20 as an input with a pull-up resistor. When the button connected to GP20 is not pressed, the pin remains in a high state. Pressing the GP20 button will pull the pin low, causing the LED to stop blinking (as defined in the code). Releasing the button returns the pin to a high state, allowing the LED to resume blinking.

However, if the button circuitry is supposed to be active-high, then the GPIO pin must be configured to a pull-down mode.

The images below illustrate how a pull-up configuration would be used as a GP20 button on the Pico W.

![Screenshot of Pull-up NOT Pressed](img/pullup_notpress2.png)

![Screenshot of Pull-up Pressed](img/pullup_press2.png)

## **GPIO - OUTPUT** 

This [code](pulse.c) demonstrates generating a custom signal using a GPIO pin on a Raspberry Pi Pico. The GPIO pin connected to an LED is programmed to create a bespoke pulse by turning the LED on for 1 second (representing a "high" signal) and then turning it off for 2 seconds (representing a "low" signal). This is then repeated using the while loop. Various pulses can be generates using this method.



## **SERIAL COMMUNICATIONS**

In this task, you will work in pairs. Pico A will compile and run the sample code for [hello_uart](https://github.com/raspberrypi/pico-examples/blob/master/uart/hello_uart/hello_uart.c), which will send character data via the serial pins (instead of the USB cable). As explained in the next section, Pico B will compile and run [uart_rx](uart_rx.c) using a new project.

To successfully exchange data between the two Pico W boards, it is essential to connect **Pico A**'s GP0 (TX) to **Pico B**'s GP1 (RX), and vice-versa. Here's why:
- Connecting GP0 of **Pico A** to GP1 of **Pico B**: GP0 on Pico A is configured as the transmit pin (TX), which sends data. GP1 on **Pico B** is configured as the receive pin (RX), which listens for incoming data. **Pico A** can send data that **Pico B** will receive by connecting them. Additionally, you should connect **Pico B**'s GP0 (TX) to **Pico A**'s GP1 (RX), allowing data transmission in both directions (if needed).
Ground (GND) connection: Both Pico W boards must share a common ground (**GND**) to establish a reliable electrical connection. Without connecting the GNDs of both boards, the voltage levels may be inconsistent, potentially causing communication issues or data corruption. By linking the grounds, you ensure both boards have the same reference point for voltage, enabling stable and correct data transmission.

Please ensure that **Pico A** includes a while-loop so the sender continuously transmits characters to **Pico B**. The image below illustrates the correct wiring setup for connecting the two Pico W boards via UART, showing the TX and RX cables swapped between the boards.
![Screenshot of Connecting 2 Pico W Together](img/p2puart.png)

## **Creating your own Project (in VSC)** 

Go ahead and create a directory to house your new project. As in the previous task, we compiled a pico example project called [hello_uart](https://github.com/raspberrypi/pico-examples/blob/master/uart/hello_uart/hello_uart.c) that will send three characters (one at a time) via the UART_TX located on pin 0 on the Raspberry Pi Pico.  In this task, we shall create a folder (under Explorer) within the UART as shown below.

![Screenshot of New Folder](img/new_folder.png)

![Screenshot of create_folder](img/create_folder.png)

Add a C file with the name uart_rx.c

![Screenshot of add_cfile](img/add_cfile.png)

Add a text file with the name ["CMakeLists.txt"](CMakeLists.txt). Ensure the filename is correct. A mistake here will lead to errors.

![Screenshot of add_CMakeLists](img/add_CMakeLists.png)

Go to uart's folder CMakeLists.txt (see below) and include the "add_subdirectory(uart_rx)" into the file in line #5.

![Screenshot of update_main_CMakeLists](img/update_main_CMakeLists.png)

Once you have saved this CMakeList.txt file, it will configure the project and create the build folder.

![Screenshot of wait](img/wait.png)

![Screenshot of build_folder_magically_created](img/build_folder_magically_created.png)

Now, you can go to CMake tool and build your new project.
![Screenshot of goto_CMake](img/goto_CMake.png)
> [NOTE]> There is an error in the screenshot above. Do use the correct [CMakeLists.txt](CMakeLists.txt) file in the repository.
## **EXERCISE**

The application uses UART communication via GPIO pins GP8 (TX) and GP9 (RX) on UART1 for data transmission and reception. It also includes conditional logic based on the state of button GP22. The functionality can be explained as follows:
- When button GP22 is **not pressed**: The software sends the numeric value '1' through UART1 every 1 second.
- When button GP22 is **pressed**: The software transmits uppercase English alphabet characters sequentially, starting from 'A' to 'Z', with a 1-second delay between each character. After reaching 'Z', it loops back to 'A'. For example, if GP22 is pressed, the output would be 'A', then 'B', and so on, with a new letter sent every 1 second.

For data reception, the software utilizes the UART1 receiver. When it reads incoming data (see Note #1):
- If the data is an uppercase alphabet character (e.g., 'A', 'B'), the software converts it to the corresponding lowercase character (e.g., 'a', 'b'). The transformed character is then printed to the serial terminal.
- If the received data is '1', the software will print the number '2' instead.
![Screenshot of New Folder](img/ex2v2.png)

 > [NOTE 1]: By connecting GP8 to GP9, we effectively create a UART loopback, meaning the transmitted data from the TX pin (GP8) is immediately received by the RX pin (GP9). This allows the Pico to both send and receive data in a self-contained loop, which is useful for testing and debugging the UART functionality.

 > [NOTE 2]: If you're experiencing random character outputs in your lab exercise, try replacing stdio_init_all() with stdio_usb_init().
