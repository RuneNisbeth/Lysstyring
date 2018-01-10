

/*
//Mapping for nodeMCU
D0 = 3
D1 = 1
D2 = 16
D3 = 5
D4 = 4
D5 = 0
D6 = 2
D7 = 14
D8 = 12
D9 = 13
D10 = 14
D11 = 13
D12 = 12
D13 = 14
D14 = 4
D15 = 5
*/
#include <ESP8266WiFi.h>
#include <ThingSpeak.h>
#include <SimpleTimer.h>

#define trigPin 16 //Define trigger pin
#define echoPin 5 //Define echo pin
#define LEDPin 4 //Define LED output pin 

SimpleTimer timer; 
WiFiClient Client;

int timer;

void setup() {
  Serial.begin (9600); // Initialize serial
  pinMode(trigPin, OUTPUT); //Set trigger pin to output
  pinMode(echoPin, INPUT); //Set echo pin to input
  pinMode(LEDPin, OUTPUT); //set LED pin to output
  timer = millis();
}

void loop() {
  long duration, distance; //Defines duration and distance vars
  //Send ultrasonic signal
  digitalWrite(trigPin, LOW);  //Set trigger pin to LOW - Just to be sure nothing is transmitting
  delayMicroseconds(2); // Wait 2 microsec before transmitting the "ping"
  digitalWrite(trigPin, HIGH); //Set trigger pin to HIGH - Transmit ping
  delayMicroseconds(20); //Wait 10 microsec - Just to generate a reliable ping
  digitalWrite(trigPin, LOW); //Set trigger pin to LOW - Stop transmitting
  
  //Listen for the ping echo
  duration = pulseIn(echoPin, HIGH); //Get duration before the ping echo is heard
  distance = (duration / 2) / 29.1; //Convert duration to centimeters

  //Print distance in centimeters to serial console
  Serial.print(distance);
  Serial.println(" cm");

  //Set the distance of the readed from the Ultrasound sensor as a light dimmer for an LED.
  analogWrite(LEDPin, distance);
  
  //delay(500); //Wait 500 ms before making a new ping
  /*
  if ( 150 < distance && distance < 300 ){
    analogWrite(3, 10);
    Serial.println("===");
  }
  if( 50 < distance && distance <130 ){
    analogWrite(3, 50);
    Serial.println("============");
  }
  if( distance < 50 ){
    analogWrite(3, 200);
    Serial.println("====================================");
  }*/

}







