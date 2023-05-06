# robot
#include <Ultrasonic.h>
#include <Servo.h>
Servo myservo;
int pos = 0; 
#define in1 2
#define in2 3
#define in3 4
#define in4 5
Ultrasonic ultrasonic(12, 13);
int distance;
int flame = 8;
int pump = 9;
int flameValue = 0;
void setup() {
  Serial.begin(9600);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);
  pinMode(flame,INPUT);
  pinMode(pump, OUTPUT);
  digitalWrite(pump, 0);
  myservo.attach(6);
  delay(2000);
  digitalWrite(in1, LOW);
  digitalWrite(in2, LOW);
  digitalWrite(in3, LOW);
  digitalWrite(in4, LOW);
}
void loop() {
  flameValue = digitalRead(flame);
  distance = ultrasonic.read();
  Serial.println(flameValue);
  if(flameValue == 0){
    digitalWrite(pump, 1);
    for (pos = 0; pos <= 180; pos += 1) {
    myservo.write(pos);            
    delay(5);                      
  }
  for (pos = 180; pos >= 0; pos -= 1) {
    myservo.write(pos);             
    delay(5);                
  }
  }
else{
        digitalWrite(pump, 0);
  }
  Serial.print("Distance in CM: ");
  Serial.println(distance);
  if(distance > 45){
  digitalWrite(in1, LOW);
  digitalWrite(in2, HIGH);
  digitalWrite(in3, LOW);
  digitalWrite(in4, HIGH);
  }else if(distance <= 45){
    digitalWrite(in1, LOW);
  digitalWrite(in2, HIGH);
  digitalWrite(in3, LOW);
  digitalWrite(in4, LOW);
  } 
