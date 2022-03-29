# tinkercad-code

#include <LiquidCrystal.h>

LiquidCrystal lcd = LiquidCrystal(2, 3, 4, 5, 6, 7); // parameters: (RS, E, D4, D5, D6, D7):
const int trigPin = 11;
const int echoPin = 12;
float time, distance;

void setup() 
{
   lcd.begin(16, 2); // LCD size
   pinMode(trigPin, OUTPUT);
   pinMode(echoPin, INPUT);

   pinMode(10, OUTPUT);//LEDs 
   pinMode(9, OUTPUT);
   pinMode(8, OUTPUT);

   pinMode(13, OUTPUT);//Piezo

   Serial.begin(9600);
}

void loop() {
digitalWrite(trigPin, LOW);
    delay(200);
digitalWrite(trigPin, HIGH);
    delay(1000);
digitalWrite(trigPin, LOW);

time = pulseIn(echoPin, HIGH);

distance = (time*.0343)/2;

// serial monitor
Serial.print("Distance:CM ");
Serial.println(distance);

 //LCD display
lcd.setCursor(0,0);
lcd.print("Distance in CM");
lcd.setCursor(0,1);
lcd.print(distance);

  if(distance > 20)
    digitalWrite(8, HIGH);
  else
    digitalWrite(8, LOW);

  if(distance > 11 && distance < 20)
    digitalWrite(9, HIGH);
  else
    digitalWrite(9, LOW);

  if(distance < 10){
    digitalWrite(10, HIGH);
      tone(13,440,1000);
      }
  else
    digitalWrite(10, LOW);
}
