
# Task: 1 | Basic Traffic Light System

## Description
A simple Arduino-based traffic light control system with manual override functionality. The system simulates a traffic light sequence and includes a pedestrian crossing button feature.

### [https://www.tinkercad.com/things/4Nbed3UDcKw-basic-traffic-light-system/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=36e6Sg8WKUILylruRvb0-_ygLhJpl6Xzi8CYyDPojTk](LINK-1)

## Components Required
- Arduino board
- 3 LEDs (Red, Yellow, Green)
- 1 Push button
- Resistors (220Ω for LEDs, 10kΩ for button)
- Jumper wires
- Breadboard

## Pin Configuration
- Pin 4: Green LED
- Pin 3: Yellow LED
- Pin 2: Red LED
- Pin 8: Push Button Input

## Functionality
### Normal Mode
When no button is pressed, the traffic light follows this sequence:
1. Green light (2 seconds)
2. Yellow light (2 seconds)
3. Red light (2 seconds)

### Pedestrian Mode
When the button is pressed:
- The system immediately switches to Red light
- Red light stays ON for 7 seconds
- Returns to normal sequence

## Code
void setup()
{
  pinMode(4,OUTPUT);
  pinMode(3,OUTPUT);
  pinMode(2,OUTPUT);
  pinMode(8,INPUT);
  
}
void loop()
{
  if (digitalRead(8) == HIGH)
  {
    digitalWrite(2,HIGH);
    delay(7000);
    digitalWrite(2,LOW);
    
  
  }
    
  
 
  else
  {
     digitalWrite(4,HIGH);
  delay(2000);
  digitalWrite(4,LOW);
  
  digitalWrite(3,HIGH);
  delay(2000);
  digitalWrite(3,LOW);
  
  digitalWrite(2,HIGH);
  delay(2000);
  digitalWrite(2,LOW);
}
}


# Task: 2 | Sensor Based Traffic Light System

## Description
A Sensor and Arduino-based traffic light control system with manual override functionality. The system simulates a traffic light sequence and includes a pedestrian crossing button feature.

### [https://www.tinkercad.com/things/2C45CZ7M4Qv-smart-traffic-light-with-sensor/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=lMaKXqiLYGT3jCKAtNqX5a-GIO_O3l8dbRdwHHyf_VE](LINK 2)

## Components Required
- Arduino board
- 3 LEDs (Red, Yellow, Green)
- HC-SR04 Ultrasonic Sensor
- Resistors (220Ω for LEDs)
- Jumper wires
- Breadboard

## Pin Configuration
- Pin 4: Green LED
- Pin 3: Yellow LED
- Pin 2: Red LED
- Pin 8: ECHO Pin of HC-SR04
- Pin 7: TRIG Pin of HC-SR04

## Operating Logic

- Distance >100cm: Red light ON
- Distance =< 100cm: Usual Traffic light

## Code
int triggerpin=7;
int echopin=8;
int redpin=2;
int yellowpin=3;
int greenpin=4;

void setup(){
  Serial.begin(9600);
  pinMode(triggerpin,OUTPUT);
  pinMode(echopin,INPUT);
  pinMode(redpin,OUTPUT);
  pinMode(yellowpin,OUTPUT);
  pinMode(greenpin,OUTPUT);
  
  
}

void loop(){
  long duration,inches,cm;
  
  
  digitalWrite(triggerpin,LOW);
  delayMicroseconds(2);
  digitalWrite(triggerpin,HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerpin,LOW);
  
  duration=pulseIn(echopin,HIGH);
  inches=microsecondsToinches(duration);
  cm=microsecondsTocentimeters(duration);
  
  
  Serial.print(cm);
  Serial.print("cm");
  Serial.println();  
  delay(100);
  if (cm>100)
  { digitalWrite(redpin,HIGH);
  }
  else
  { 
    digitalWrite(greenpin,HIGH);
    delay(3000);
    digitalWrite(greenpin,LOW);
    digitalWrite(redpin,HIGH);
    delay(3000);
    digitalWrite(redpin,LOW);
    digitalWrite(yellowpin,HIGH);
    delay(3000);
    digitalWrite(yellowpin,LOW);
  }
  
}
long microsecondsToinches(long microseconds){
  return microseconds/74/2;
}
long microsecondsTocentimeters(long microseconds){
  return microseconds/29/2;



  
}
  

}

