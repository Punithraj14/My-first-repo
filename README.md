# My-first-repo
This is my first git Repository

Smart dustbin using ultrasonic sensor
Automatically opens the dustbin lid when someone approaches.
Uses an ultrasonic sensor to detect distance and a servo motor to open/close the lid.

Components:

Arduino Uno
Ultrasonic Sensor (HC-SR04)
Servo Motor (SG90)
Jumper Wires, Breadboard


Code (smart_dustbin.ino)
#include <Servo.h>
Servo lidServo;
int trigPin = 9;
int echoPin = 10;
long duration;
int distance;

void setup() {
  lidServo.attach(3);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  if (distance < 15) {
    lidServo.write(90);  // open
    delay(3000);
  } else {
    lidServo.write(0);   // close
  }
  delay(500);
}
