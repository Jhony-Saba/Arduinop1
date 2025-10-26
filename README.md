# Arduinop1
.org 0x00
rjmp REST

REST:
ldi R16 , 0xFF
out DDRD , R16


main:
ldi R17 ,0b0111111 // Display number 0
call SHOW

ldi R17 ,0b0000110 // Display number 1
call SHOW

ldi R17 ,0b1011011 // Display number 2
call SHOW

ldi R17 ,0b1001111 // Display number 3
call SHOW

ldi R17 ,0b1100110 // Display number 4
call SHOW

ldi R17 , 0b1101101 // Display number 5
call SHOW

ldi R17 ,0b1111101 // Display number 6
call SHOW

ldi R17 ,0b0000111 // Display number 7
call SHOW

ldi R17 ,0b1111111 // Display number 8
call SHOW

ldi R17 ,0b1101111 // Display number 9
call SHOW

JMP main

SHOW:
out portD , R17
CALL delay
ret


delay:

LDI R16,HIGH(3036) 

STS TCNT1H,R16 

LDI R16,LOW(3036) 

STS TCNT1L,R16 

LDI R16,0

STS TCCR1A,R16 

LDI R16,4

STS TCCR1B,R16 // use internal clock with prescaler value = 256

again:

SBIS TIFR1,TOV1 // Skip next instruction if TOV1 == 1 

JMP again 

LDI R16,0

STS TCCR1B,R16 

SBI TIFR1,TOV1 

RET 
.
