# TO GENERATE A 1 MS DELAY 
# 8051 Program

## AIM
To write an assembly language program for the 8051 microcontroller to generate a 1 ms delay using Timer 0 in Mode 1 (16-bit timer mode).


## APPARATUS REQUIRED
- Personal computer
- Keil μVision IDE

## ALGORITHM
1.Start the program execution at address 00H.
2.Initialize Timer 0 in Mode 1 (16-bit timer mode) by loading the value #01H into the TMOD register.
3.Start the main loop (label REPEAT) to continuously blink the LEDs connected to Port 2.
4.Load Timer 0 registers with initial values TH0 = 0FCH and TL0 = 018H to generate approximately 50 ms delay.
5.Turn ON all LEDs by sending #0FFH to Port 2.
6.Start Timer 0 by setting TR0 = 1.
7.Wait for Timer 0 overflow by checking the Timer Flag TF0.
8.Stay in the loop (WAIT1) until TF0 becomes 1.
9.Stop Timer 0 and clear overflow flag TF0 after delay is complete.
10.Turn OFF all LEDs by sending #00H to Port 2.
11.Reload Timer 0 again with TH0 = 0FCH and TL0 = 018H for the next delay period.
12.Start Timer 0 again (TR0 = 1).
13.Wait for the second delay in loop WAIT2 until TF0 is set.
14.Stop Timer 0 and clear TF0 again.
15.Repeat the entire process from step 4 continuously using SJMP REPEAT.
16.End the program.
## PROGRAM
```asm
ORG 00H              
MAIN: 
    MOV TMOD,#01H;   
REPEAT:
    MOV TH0,#0FCH; 
    MOV TL0,#018H; 
    MOV P2,#0FFH; 
    SETB TR0;
WAIT1:
    JNB TF0,WAIT1; 
    CLR TR0; 
    CLR TF0; 
    MOV P2,#00H; 
    MOV TH0,#0FCH; 
    MOV TL0,#018H
    SETB TR0         
WAIT2:
    JNB TF0,WAIT2;
    CLR TR0;
    CLR TF0;
    SJMP REPEAT; 
END

```
## OUTPUT
<img width="1920" height="1200" alt="nithish(sk2)" src="https://github.com/user-attachments/assets/a5cbce9e-1bc1-4a91-bfa6-34464d0bfa33" />

## RESULT
The program successfully generate 1ms delay using timer 0 in mode 1(16-bit timer mode
