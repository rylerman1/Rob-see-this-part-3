Rob-see-this-part-3
===================

Further Code changes

// Arduino PWM Speed Control：
// Pin definitions for PWM speed control using 
// DFRobot Arduino Compatible Motor Shield (2A):

#include "MotorRobotBase.h"
#include "Sensor.h"

#define Motor MotorRobotBase

void forward (Motor &m1, Motor &m2) 
{
  delay(5000);
  int speed; 
  // speed up
  for (speed = 0; speed <= 255; speed += 5) {
    m1.forward(speed);
    m2.forward(speed);
    delay(30); 
  }
  // speed down
  for (speed = 255; speed >= 0; speed -= 5) {
    m1.forward(speed);
    m2.forward(speed);
    delay(30);
  }
}

void backward (Motor &m1, Motor &m2) 
{
  int speed; 
  // speed up
  for (speed = 0; speed <= 255; speed += 5) {
    m1.reverse(speed);
    m2.reverse(speed);
    delay(30); 
  }
  // speed down
  for (speed = 255; speed >= 0; speed -= 5) {
    m1.reverse(speed);
    m2.reverse(speed);
    delay(30);
  }
}

Motor right_motor(Motor::MOTOR_1);
Motor left_motor(Motor::MOTOR_2);
Sensor light(Sensor::SENSOR_0);

int avg_illumination = 511;

void setup () 
{ 
  int ii;
  int current_level;
  
  Serial.begin(9600);
  
  right_motor.setup();
  left_motor.setup();
  light.setup();
  light.set_mode(Sensor::SIMPLEX_MODE);
  light.calibrate();

} 

void loop () 
{
  int light_level = 1023;
  char light_str[255];
  
  light.read(light_level);

//light_level = light.get_light_level();
  if (light_level < (light.get_light_level() - 20)) {
     Serial.write("low\n"); 
     left_motor.forward(0);
     right_motor.forward(0);
  }  else {
     left_motor.reverse(500);
     right_motor.reverse(500);
     Serial.write("normal\n");     
  }
/*

  if (light_level > 1000) {  
    Serial.write("1000\n");    
  } else  if (light_level > 900) {  
    Serial.write("900\n");    
  } else  if (light_level > 800) {  
    Serial.write("800\n");    
  } else  if (light_level > 700) {  
    Serial.write("700\n");    
  }  else  if (light_level > 600) {  
    Serial.write("600\n");    
  }  else  if (light_level > 500) {  
    Serial.write("500\n");    
  }  else  if (light_level > 400) {  
    Serial.write("400\n");    
  }  else  if (light_level > 300) {  
    Serial.write("300\n");    
  }  else  if (light_level > 200) {  
    Serial.write("200\n");    
  }  else  if (light_level > 100) {  
    Serial.write("100\n");    
  }   else  { 
    Serial.write("00\n");    
  } 
  */
  
  delay(500);
}
Rob we deleted any and all turns
