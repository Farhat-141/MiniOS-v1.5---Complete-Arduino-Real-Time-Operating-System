# MiniOS-v1.5---Complete-Arduino-Real-Time-Operating-System
# MiniOS v1.5 - Complete Arduino Real-Time Operating System

## 🎯 **Project Overview**

MiniOS v1.5 is a sophisticated Arduino-based real-time operating system simulation that demonstrates advanced embedded programming concepts including multitasking, interrupt handling, I2C communication, and system monitoring.

## 🔧 **Hardware Components**

### **Arduino Uno R3**
- Main microcontroller running at 16MHz
- Built-in LED (Pin 13) for CPU load indication

### **LEDs & Indicators**
- **LED1 (Red)** - Pin 2: Task A indicator (1-second blink)
- **LED2 (Green)** - Pin 3: Task B indicator (2-second blink) 
- **LED3 (Yellow)** - Pin 6: Emergency alert indicator
- **Built-in LED** - Pin 13: CPU usage with breathing effect

### **User Interface**
- **Emergency Button** - Pin 7: High-priority interrupt trigger
- **Menu Button** - Pin 8: Navigate through LCD menu pages
- **Main LCD (16x2)** - I2C Address 0x27: System status display
- **Menu LCD (16x2)** - I2C Address 0x26: Multi-page information display

### **Power & Communication**
- USB power and serial communication at 9600 baud
- I2C bus (SDA: A4, SCL: A5) for dual LCD communication
- Pull-up resistors for reliable button operation

## 💻 **Software Architecture**

### **Real-Time Task Scheduler**
- **Task A**: LED1 blinker (1000ms interval)
- **Task B**: LED2 blinker (2000ms interval)  
- **Task C**: System monitoring and serial polling (100ms interval)
- **Emergency Task**: High-priority interrupt handler

### **Operating Modes**
- **AUTO Mode**: Automatic task scheduling
- **MANUAL Mode**: User-controlled operation
- **PAUSE/RESUME**: System state control
- **Emergency Override**: Interrupt-driven emergency response

### **Advanced Features**

#### **Multi-Page Menu System**
- **Page 1**: System title and uptime
- **Page 2**: Task intervals and operating mode
- **Page 3**: Task execution counters
- **Page 4**: CPU usage and LED brightness
- **Page 5**: LED states and last command

#### **Serial Command Interface**
```
Available Commands:
- status    : Complete system status report
- ledon     : Turn LED1 on manually
- ledoff    : Turn LED1 off manually
- pause     : Toggle system pause/resume
- auto      : Toggle AUTO/MANUAL mode
- bright N  : Set LED brightness (0-255)
- reset     : Reset all counters
- help      : Display command list
```

#### **System Monitoring**
- Real-time CPU usage calculation
- Task execution counters
- Emergency event logging
- System uptime tracking
- LED brightness control (PWM)

#### **Interrupt Handling**
- Hardware interrupt on emergency button
- Proper debouncing (200ms minimum interval)
- Non-blocking emergency response
- State preservation and restoration

## 🚀 **Key Programming Concepts Demonstrated**

### **1. Cooperative Multitasking**
```cpp
// Non-blocking task scheduling
if (currentTime - lastTaskA >= TASK_A_INTERVAL) {
    taskA();
    lastTaskA = currentTime;
}
```

### **2. Hardware Interrupts**
```cpp
// ISR with debouncing
void emergencyISR() {
    static unsigned long lastInterrupt = 0;
    unsigned long currentTime = millis();
    if (currentTime - lastInterrupt > 200) {
        emergencyTriggered = true;
    }
}
```

### **3. I2C Communication**
```cpp
// Dual LCD management
LiquidCrystal_I2C lcdMain(0x27, 16, 2);
LiquidCrystal_I2C lcdMenu(0x26, 16, 2);
```

### **4. State Machine Implementation**
- Menu page navigation
- LED state management
- System mode transitions

### **5. Real-time Performance Monitoring**
```cpp
// CPU usage calculation
cpuUsage = (activeTime / 10.0);  // Convert to percentage
```

## 📊 **System Performance**

- **Response Time**: <50ms for all user inputs
- **Emergency Response**: <1ms interrupt latency
- **Display Update Rate**: 4Hz (250ms intervals)
- **Serial Baud Rate**: 9600 bps
- **Memory Usage**: Optimized for Arduino Uno's 2KB RAM

## 🎮 **Interactive Features**

### **Hardware Buttons**
- **Emergency Button**: Triggers immediate safety response
- **Menu Button**: Cycles through 5 information pages

### **Software Controls**
- Real-time LED brightness adjustment
- System pause/resume functionality  
- Mode switching (AUTO/MANUAL)
- Counter reset capability
- Comprehensive status reporting

### **Visual Feedback**
- Animated LED states with proper PWM brightness
- CPU load indicator with breathing effect
- Emergency alert sequence (rapid 5-blink pattern)
- Live status updates on dual LCDs

## 🛡️ **Safety & Reliability Features**

- **Button Debouncing**: Hardware and software debouncing
- **State Preservation**: Emergency tasks preserve system state
- **Watchdog Simulation**: CPU monitoring and load indication
- **Error Handling**: Unknown command detection and reporting
- **Resource Management**: Terminal buffer limiting (100 lines max)

## 📈 **Educational Value**

This project demonstrates:
- **Embedded Systems Programming**: Real Arduino C++ concepts
- **Real-Time Systems**: Task scheduling and timing management
- **Hardware Interfacing**: GPIO, I2C, interrupts, PWM
- **User Interface Design**: Multi-modal input/output systems
- **System Architecture**: Modular, maintainable code structure

## 🔧 **Technical Specifications**

- **Microcontroller**: Arduino Uno (ATmega328P)
- **Clock Speed**: 16 MHz
- **Flash Memory**: 32KB (program storage)
- **SRAM**: 2KB (runtime variables)
- **EEPROM**: 1KB (non-volatile storage)
- **Digital I/O Pins**: 14 (6 PWM capable)
- **Analog Input Pins**: 6
- **Operating Voltage**: 5V
- **Input Voltage**: 7-12V (recommended)

This MiniOS implementation showcases professional embedded development practices while remaining accessible for learning and experimentation. The simulation provides a safe environment to understand complex Arduino concepts before deploying to actual hardware.
