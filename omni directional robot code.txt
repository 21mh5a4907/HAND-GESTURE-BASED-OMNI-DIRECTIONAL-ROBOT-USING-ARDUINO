#include <Wire.h>
#include <Adafruit_MotorShield.h>

// Create the motor shield object with the default I2C address
Adafruit_MotorShield AFMS = Adafruit_MotorShield(); 

void setup() {
  Serial.begin(9600);           // set up Serial library at 9600 bps
  Serial.println("Adafruit Motorshield v2 - Omni-Directional Robot Test!");

  AFMS.begin();  // create with the default frequency 1.6KHz
  
  // Set up motor objects
  Adafruit_DCMotor *motor1 = AFMS.getMotor(1);
  Adafruit_DCMotor *motor2 = AFMS.getMotor(2);
  Adafruit_DCMotor *motor3 = AFMS.getMotor(3);
}

void loop() {
  int gestureValue = readGesture();

  if (gestureValue == GESTURE_FORWARD) {
    moveForward();
  } else if (gestureValue == GESTURE_BACKWARD) {
    moveBackward();
  } else if (gestureValue == GESTURE_LEFT) {
    moveLeft();
  } else if (gestureValue == GESTURE_RIGHT) {
    moveRight();
  } else {
    stopMoving();
  }

  delay(100);
}

void moveForward() {
  motor1->setSpeed(255);
  motor2->setSpeed(255);
  motor3->setSpeed(255);

  motor1->run(FORWARD);
  motor2->run(FORWARD);
  motor3->run(FORWARD);
}

void moveBackward() {
  motor1->setSpeed(255);
  motor2->setSpeed(255);
  motor3->setSpeed(255);

  motor1->run(BACKWARD);
  motor2->run(BACKWARD);
  motor3->run(BACKWARD);
}

void moveLeft() {
  motor1->setSpeed(255);
  motor2->setSpeed(255);
  motor3->setSpeed(255);

  motor1->run(BACKWARD);
  motor2->run(FORWARD);
  motor3->run(BACKWARD);
}

void moveRight() {
  motor1->setSpeed(255);
  motor2->setSpeed(255);
  motor3->setSpeed(255);

  motor1->run(FORWARD);
  motor2->run(BACKWARD);
  motor3->run(FORWARD);
}

void stopMoving() {
  motor1->setSpeed(0);
  motor2->setSpeed(0);
  motor3->setSpeed(0);

  motor1->run(RELEASE);
  motor2->run(RELEASE);
  motor3->run(RELEASE);
}

int readGesture() {
  // Replace this with your actual gesture reading code
  // You'll need to configure your sensor and read the gesture data
  // This function should return a value representing the detected gesture
  return analogRead(A0); // Replace with your actual code
}
