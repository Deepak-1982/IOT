#include <Wire.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_ADXL345_U.h>
#include <Servo.h>

Servo myservo;
Adafruit_ADXL345_Unified accel = Adafruit_ADXL345_Unified(12345);

void setup() {
  myservo.attach(9);
  accel.begin();
}

void loop() {
  sensors_event_t event;
  accel.getEvent(&event);
  
  int angle = map(event.acceleration.x, -10, 10, 0, 180);
  
  myservo.write(angle);
  delay(10);
}
