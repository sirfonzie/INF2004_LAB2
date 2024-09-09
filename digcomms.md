### I2C and SPI Communication Between Two Raspberry Pi Pico W Boards [optional]

#### Overview
In this lab, you will set up two Raspberry Pi Pico W boards to communicate with each other using I2C and SPI protocols. You will compile the example code from the `pico_examples` repository and observe how data is transmitted and received between the two Pico boards.

---

### Part 1: I2C Communication

#### 1.1. Objective
In this section, we will use the I2C protocol to establish communication between two Raspberry Pi Pico W boards, where one Pico acts as the I2C master and the other as the I2C slave.

#### 1.2. Materials
- 2 Raspberry Pi Pico boards
- Breadboard and jumper wires
- Computer with VSCode and Pico SDK installed
- USB cables

#### 1.3. Wiring Diagram
Connect the two Raspberry Pi Pico boards as follows:

### I2C Communication Wiring (Pico A to Pico B)

| **Pico A (Master)** | **Pico B (Slave)** |
|---------------------|--------------------|
| GP4 (SDA)           | GP4 (SDA)          |
| GP5 (SCL)           | GP5 (SCL)          |
| GND                 | GND                |

  
#### 1.4. Steps

1. **Set up the environment**:
   Ensure the Pico SDK and the `pico_examples` repository are properly set up on your machine.

2. **Create the project directory**:
   Create a folder named `i2c_lab` within your project workspace.

3. **Compile the I2C example**:
   Navigate to the `pico_examples/i2c/` directory. The example we will use is `i2c_master_slave`. Follow these steps:

   - Open a terminal in VS Code.
   - Run the following commands to configure and build the project:

   ```bash
   mkdir build
   cd build
   cmake ..
   make -j4
   ```

4. **Upload the code**:
   - Flash the `i2c_master` example to **Pico A** (Master).
   - Flash the `i2c_slave` example to **Pico B** (Slave).

5. **Run the I2C communication**:
   Once the code is uploaded, the two boards should begin communicating over I2C. The master will send data to the slave, and the slave will respond accordingly.

#### 1.5. Expected Observations
- The master Pico should send data (e.g., byte values) to the slave Pico.
- The slave Pico will receive the data and may respond with acknowledgment messages.
- Using a serial terminal, you can view the transmitted and received data between the two Picos.
  
---

### Part 2: SPI Communication

#### 2.1. Objective
In this section, we will use the SPI protocol to establish communication between two Raspberry Pi Pico boards, where one Pico acts as the SPI master and the other as the SPI slave.

#### 2.2. Materials
- 2 Raspberry Pi Pico boards
- Breadboard and jumper wires
- Computer with VS Code and Pico SDK installed
- USB cables

#### 2.3. Wiring Diagram
Connect the two Raspberry Pi Pico boards as follows:

### SPI Communication Wiring (Pico A to Pico B)

| **Pico A (Master)** | **Pico B (Slave)** |
|---------------------|--------------------|
| GP18 (SCK)          | GP18 (SCK)         |
| GP19 (TX)           | GP19 (RX)          |
| GP16 (CS)           | GP16 (CS)          |
| GND                 | GND                |


#### 2.4. Steps

1. **Create the project directory**:
   Create a folder named `spi_lab` within your project workspace.

2. **Compile the SPI example**:
   Navigate to the `pico_examples/spi/` directory. The example we will use is `spi_master_slave`. Follow these steps:

   - Open a terminal in VS Code.
   - Run the following commands to configure and build the project:

   ```bash
   mkdir build
   cd build
   cmake ..
   make -j4
   ```

3. **Upload the code**:
   - Flash the `spi_master` example to **Pico A** (Master).
   - Flash the `spi_slave` example to **Pico B** (Slave).

4. **Run the SPI communication**:
   Once the code is uploaded, the two boards should start exchanging data using the SPI protocol.

#### 2.5. Expected Observations
- The master Pico will send data (e.g., a sequence of bytes) to the slave Pico.
- The slave Pico will receive the data and may respond with its own data.
- Using a serial terminal, you can monitor the data exchange and confirm successful SPI communication.

---

### Conclusion

In this lab, you have set up two Raspberry Pi Pico boards to communicate using both I2C and SPI protocols. You have compiled the example codes, connected the boards, and observed how data is transmitted and received. These communication protocols are essential for interfacing various peripherals in embedded systems and will be helpful in many future projects.
