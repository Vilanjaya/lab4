![1_Page_1](https://user-images.githubusercontent.com/111475831/185472566-f484f294-8bf5-4de0-8bd9-d45a0972e4ba.jpg)


 ![1_Page_2](https://user-images.githubusercontent.com/111475831/185472686-b4bff46d-d4d7-40a2-857d-e0c45df13c7a.jpg)


### INTRODUCTION

A water tank level control system is a device that automatically manages pumps and other systems
to maintain consistent water levels in water storage tanks and other uses. It does this by monitoring
the water level for us. This little water level control system was created using a pic16f877a
microcontroller, interrupts in a PIC microcontroller, microcontroller programming in C, and
additional hardware techniques currently under investigation. The main goal of this lab is to use
the understanding of interrupts and other programming techniques of the pic16f877a to build a
simple water level controlling system for a water tank. For a better result, knowledge of PCB
fabrication is also used to this project. A printed circuit board, or PCB, is used to mechanically
retain electronic components and electrically connect them via conductive channels made from
copper that are cut into and adhered to an insulating substrate.

#### OBJECTIVE

The main objective of this lab is for you to develop a small water level controlling system of a
water tank using the knowledge of interrupts and other programming techniques of PIC16f877a
from all the labs we did throughout the course.

#### TASK

Below is a water tank that has two DC motors where the motor one is used to pump the water into
the tank the motor two is used to suck the water out from the water tank and there are three sensors
that are used to measure the water level of the tank. Since Proteus doesn’t have water level sensors,
it’s better to use the active latched switches instead. The operations of the two DC motors
according to the switch state is given in a table right after the diagram.

![tank](https://user-images.githubusercontent.com/111475831/185471141-1a96092c-616f-4fe8-b7d1-cc54157e67a7.jpg)

#### OPERATION TABLE

![truth](https://user-images.githubusercontent.com/111475831/185471766-7ae732ac-9a5e-49d2-a3c4-d4c9b6b80e9c.jpg)



#### APPARATUS OF EXPERIMENT

1. PIC16F877A Microcontroller

The Microchip PIC16F877a is a 40-pin PIC microcontroller with RISC architecture that is utilized
in embedded projects. From Port A to Port E, there are five ports on it. It contains three timers,


two of which are 8-bit timers and one of which is a 16-bit timer. A PIC microcontroller known as
the PIC16F877a is frequently utilized in embedded projects like home automation systems and
bank security systems. It is quite easy to code or program this microcontroller, and it is also very
convenient to use. The fact that it employs FLASH memory technology is one of its key advantages
because it allows for unlimited write-erase cycles.

2. Two DC Motors

A DC motor is any of a class of rotary electrical motors that converts direct current (DC)
electrical energy into mechanical energy.

3. Crystal oscillator

A crystal oscillator is a circuit of the electric oscillator type that establishes its frequency using a
crystal resonator. In order to provide a reliable clock signal and in particular situations where a
high-frequency reference is needed, crystal oscillators are primarily employed in digital
integrated circuits.

4. L293D Motor driver

Based on the L293 IC, the L293D shield is a driver board that can simultaneously operate two
stepper or servo motors and four DC motors. The L293D is a 16-pin motor driver IC that has the
ability to simultaneously operate two DC motors in either direction.

5. Ultrasonic sensor

The time gap between the emission and reception is measured by ultrasonic sensors to determine
the target's distance. Most often, proximity sensors are combined with ultrasonic sensors. They
are present in anti-collision safety systems and self-parking automotive technologies. Robotic
obstacle detection systems and manufacturing technology both use ultrasonic sensors.


6. Resistors
7. Capacitors (47uF & 470uF)
8. LED’s
9. Power input (12V DC

# PCB DESIGN

![pcb](https://user-images.githubusercontent.com/111475831/185471849-7691622b-73c3-4d8f-b7c0-555ec892269c.jpg)


![img 1](https://user-images.githubusercontent.com/111475831/185471940-2cb7dcd4-51da-4da9-9ed5-3ae9bb283128.jpg)


![img 2](https://user-images.githubusercontent.com/111475831/185472001-c7b36774-d74e-4758-aa95-7fa6b9f1cc3c.jpg)


#### CODE

// PIC16F877A Configuration Bit Settings
// 'C' source line config statements

##### // CONFIG

#pragma config FOSC = EXTRC // Oscillator Selection bits (RC oscillator)

#pragma config WDTE = OFF // Watchdog Timer Enable bit (WDT disabled)

#pragma config PWRTE = OFF // Power-up Timer Enable bit (PWRT disabled)

#pragma config BOREN = OFF // Brown-out Reset Enable bit (BOR disabled)

#pragma config LVP = OFF // Low-Voltage (Single-Supply) In-Circuit Serial Programming

Enable bit (RB3 is digital I/O, HV on MCLR must be used for programming)

#pragma config CPD = OFF // Data EEPROM Memory Code Protection bit (Data EEPROM
code protection off)

#pragma config WRT = OFF // Flash Program Memory Write Enable bits (Write protection
off; all program memory may be written to by EECON control)

#pragma config CP = OFF // Flash Program Memory Code Protection bit (Code protection
off)

// #pragma config statements should precede project file includes.
// Use project enums instead of #define for ON and OFF.

#define _XTAL_FREQ 20000000

#include<xc.h>

#include<htc.h>

void main(void){

// INTCONbits.GIE = 1; // Global Interrupt Enable bit

// INTCONbits.PEIE = 1; // Peripheral Interrupt Enable bit

// INTCONbits.INTE = 1; // RB0/INT External Interrupt Enable bit


// OPTION_REGbits.INTEDG = 1; //Interrupt Edge Select bit

TRISC0 = 0; // PORTC pin 0 AS OUTPUT - Green LED

TRISC1 = 0; // PORTC pin 1 AS OUTPUT - Red LED

TRISB0 = 1;// SW3 // PORTB pin 0 AS INPUT - Push Button 1

TRISB1 = 1;// SW

TRISB2 = 1;// SW

while(1){

if (!PORTBbits.RB0){

if(!PORTBbits.RB2){

if(PORTBbits.RB1){

PORTCbits.RC1 = 0; // RED LED OFF

PORTCbits.RC0 = 1; // GREEN LED ON

}else{

PORTCbits.RC1 = 0; // RED LED OFF

PORTCbits.RC0 = 0;

}
}else{

if(PORTBbits.RB1){

PORTCbits.RC1 = 0; // RED LED OFF

PORTCbits.RC0 = 1; // GREEN LED ON

}else{

PORTCbits.RC1 = 0; // RED LED OFF

PORTCbits.RC0 = 0;

}

}
}else{

if(PORTBbits.RB1 && PORTBbits.RB2){


PORTCbits.RC1 = 1; //Turn ON the RED LED

PORTCbits.RC0 = 0; //Turn off the Green LED

__delay_ms(500);

PORTCbits.RC1 = 0;

while(PORTBbits.RB0);
}
}
}
return;
}
/*void __interrupt() isr(void){

if (INTCONbits.INTF == 1){ // Checking RB0/INT External Interrupt Flag bit

PORTCbits.RC1 = 1; //Turn ON the RED LED

PORTCbits.RC0 = 0; //Turn off the Green LED

__delay_ms(500);

INTCONbits.INTF = 0; // Setting External Interrupt Flag bit to a logic low after 10
seconds

}

} */

##### ********


