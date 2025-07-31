# 🤖 Industrial Intelligent Line Follower Robot

This repository contains the code, documentation, and circuit design for an **intelligent industrial-grade line following robot**. Designed for warehouse automation and material handling applications, the robot uses IR sensors and PID control for high-precision line tracking.

---

## 🚀 Features

- Smooth and stable line tracking using PID control
- Modular code structure with tunable PID parameters
- IR sensor array for line position detection
- Works on curves, junctions, and high-speed paths
- L298N motor driver support
- Easily scalable for industrial paths

---

## 🧠 Working Principle

1. Five IR sensors detect the black line on a white surface.
2. The Arduino calculates the robot’s position relative to the center of the line.
3. A PID algorithm adjusts the speed of both motors to correct direction.
4. The robot maintains its path precisely, even at turns.

---

## 🛠️ Hardware Required

- Arduino UNO
- IR Sensor Array (5 sensors)
- L298N Motor Driver
- 2 DC Motors + Wheels
- Power Supply (7.4V Li-ion or 9V)
- Jumper wires, chassis

---

## 📐 Circuit Diagram

<img width="1314" height="713" alt="Image" src="https://github.com/user-attachments/assets/c98e3a4f-e325-4d8d-a58e-e30bfadc9d3d" />

## 💻 Code Overview

#define IR_SENSOR_RIGHT 13
#define IR_SENSOR_LEFT 12
#define MOTOR_SPEED 180

//Right motor
int enableRightMotor=10;
int rightMotorPin1=4;
int rightMotorPin2=5;

//Left motor
int enableLeftMotor=11;
int leftMotorPin1=6;
int leftMotorPin2=7;

void setup()
{
  
  TCCR0B = TCCR0B & B11111000 | B00000010 ;     //This sets PWM frequecny as 7812.5 hz.
  
  
  pinMode(enableRightMotor, OUTPUT);
  pinMode(rightMotorPin1, OUTPUT);
  pinMode(rightMotorPin2, OUTPUT);
  
  pinMode(enableLeftMotor, OUTPUT);
  pinMode(leftMotorPin1, OUTPUT);
  pinMode(leftMotorPin2, OUTPUT);

  pinMode(IR_SENSOR_RIGHT, INPUT);
  pinMode(IR_SENSOR_LEFT, INPUT);
  rotateMotor(0,0);   
}


void loop()
{

  int rightIRSensorValue = digitalRead(IR_SENSOR_RIGHT);
  int leftIRSensorValue = digitalRead(IR_SENSOR_LEFT);

  //If none of the sensors detects black line, then go straight
  if (rightIRSensorValue == LOW && leftIRSensorValue == LOW)
  {
    rotateMotor(MOTOR_SPEED, MOTOR_SPEED);
  }
  //If right sensor detects black line, then turn right
  else if (rightIRSensorValue == HIGH && leftIRSensorValue == LOW )
  {
      rotateMotor(-MOTOR_SPEED, MOTOR_SPEED); 
  }
  //If left sensor detects black line, then turn left  
  else if (rightIRSensorValue == LOW && leftIRSensorValue == HIGH )
  {
      rotateMotor(MOTOR_SPEED, -MOTOR_SPEED); 
  } 
  //If both the sensors detect black line, then stop 
  else 
  {
    rotateMotor(0, 0);
  }
}


void rotateMotor(int rightMotorSpeed, int leftMotorSpeed)
{
  
  if (rightMotorSpeed < 0)
  {
    digitalWrite(rightMotorPin1,LOW);
    digitalWrite(rightMotorPin2,HIGH);    
  }
  else if (rightMotorSpeed > 0)
  {
    digitalWrite(rightMotorPin1,HIGH);
    digitalWrite(rightMotorPin2,LOW);      
  }
  else
  {
    digitalWrite(rightMotorPin1,LOW);
    digitalWrite(rightMotorPin2,LOW);      
  }

  if (leftMotorSpeed < 0)
  {
    digitalWrite(leftMotorPin1,LOW);
    digitalWrite(leftMotorPin2,HIGH);    
  }
  else if (leftMotorSpeed > 0)
  {
    digitalWrite(leftMotorPin1,HIGH);
    digitalWrite(leftMotorPin2,LOW);      
  }
  else 
  {
    digitalWrite(leftMotorPin1,LOW);
    digitalWrite(leftMotorPin2,LOW);      
  }
  analogWrite(enableRightMotor, abs(rightMotorSpeed));
  analogWrite(enableLeftMotor, abs(leftMotorSpeed));    
}


