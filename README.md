# 🧠 Baremetal Embedded OS — On Arduino

## 📌 Overview

This project is a guided journey to building a **tiny operating system** for an **8-bit AVR-based Arduino** (e.g., Uno, Nano, ATmega328P). From the bare metal up — including task scheduling, context switching, and device abstraction.

---

## 🛠 Requirements

* **Hardware**: Arduino Uno / Nano (ATmega328P)
* **Toolchain**:

  * `avr-gcc`
  * `avrdude` (for flashing)
  * Optional: `simavr` for simulation
* **Editor**: VS Code, Vim, or any C-friendly IDE

---

## 📚 Learning Milestones

| Milestone                         | Description                               |
| --------------------------------- | ----------------------------------------- |
| ✅ **M1: Blinky Bare Metal**       | Write C code without Arduino libraries    |
| ✅ **M2: Timer Interrupts**        | Setup Timer0/1/2 interrupts manually      |
| ✅ **M3: Cooperative Scheduler**   | Run tasks one after another (round-robin) |
| ✅ **M4: Preemptive Multitasking** | Context switching using timer ISR         |
| ✅ **M5: Stack Management**        | Per-task stack, switching SP              |
| ✅ **M6: Semaphores & Mutexes**    | Basic inter-task synchronization          |
| ✅ **M7: IPC (Message Queues)**    | Lightweight queue-based communication     |
| ✅ **M8: Device Drivers**          | Abstract GPIO, UART, timers               |
| ✅ **M9: CLI Shell over UART**     | Interact with tasks, monitor OS           |
| ✅ **M10: Power Management**       | Sleep, wakeup tasks, energy modes         |

---

## 🏁 Project Structure

```bash
Baremetal-arduino-OS/
├── src/
│   ├── main.c                # Boot and OS start
│   ├── task.c                # Task management
│   ├── scheduler.c           # Scheduler logic
│   ├── isr.c                 # Timer interrupts
│   ├── context_switch.s      # Assembly for context save/restore
│   ├── drivers/
│   │   ├── gpio.c            # GPIO HAL
│   │   ├── uart.c            # UART driver
│   └── kernel/
│       ├── os.c              # OS-level API
│       └── sync.c           # Semaphores, mutexes
├── include/
│   └── *.h                  # Headers
├── build/
├── Makefile
└── README.md
```

---

## 🧪 Milestone Tasks Breakdown

### ✅ M1: Bare Metal Blinky

* No `digitalWrite()`, no `delay()`
* Use `PORTB`/`DDRB` for GPIO

### ✅ M2: Setup Timer0

* Configure CTC mode
* Set up compare match ISR
* Blink LED using timer ticks

### ✅ M3: Cooperative Scheduler

* Create `Task` struct
* `os_schedule()` runs each task sequentially
* Tasks must yield

### ✅ M4: Preemptive Multitasking

* Set up Timer ISR to preempt
* Save/restore context (`context_switch.s`)
* Store task state (SP, regs) in TCB

### ✅ M5: Stack Management

* Allocate stack for each task
* On task create: set SP to top of task stack

### ✅ M6: Semaphores

* Implement binary/semaphore counters
* Use in producer/consumer pattern

### ✅ M7: Message Queues

* Fixed-size circular buffer
* `os_queue_send()`, `os_queue_recv()`

### ✅ M8: Device Drivers

* Abstract GPIO: `gpio_write(pin, val)`
* UART: `uart_send()`, `uart_recv()`

### ✅ M9: UART CLI Shell

* Type `tasks` → see all task IDs and states
* Implement command parser

### ✅ M10: Power Management

* Put CPU in `SLEEP_MODE_IDLE`
* Wake on timer/interrupt

---

## 🎯 Example Goals

* Blink three LEDs at different rates using preemptive tasks
* Send temperature readings over UART every 5s
* Let UART command pause/resume tasks
* Use semaphores to control LED flashing from button press

---

## 📘 Resources

* [ATmega328P Datasheet (PDF)](https://ww1.microchip.com/downloads/en/devicedoc/atmel-8271-8-bit-avr-microcontroller-atmega48a-88a-168a-328-328p_datasheet.pdf)
* [AVR Instruction Set Manual](https://ww1.microchip.com/downloads/en/AppNotes/AVR-Instruction-Set-Manual-DS40002198A.pdf)
* [simavr GitHub (AVR Emulator)](https://github.com/buserror/simavr)

---

## 🚀 Getting Started

```bash
make flash            # Compile and upload to Arduino
make monitor          # Open serial monitor (if using UART)
```

---
