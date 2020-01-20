# int trigPin = 5;
int echoPin = 6;
int ledPin = 3;
int x = 400;
int y = 1;

void setup() {
  pinMode (7, OUTPUT);
  Serial.begin(9600);
  pinMode(2, OUTPUT);

  delay(1000);
  servoLeft.attach(11);
  servoRight.attach(10);

  pinMode (6 , INPUT);
  pinMode (5, OUTPUT);


  Serial.begin(9600);  // initialize serial communication @ 9600 baud:
  pinMode (3, INPUT);
}// end void setup

void loop() {
  checkping();
  forward();
  checkflame();
 if (distance < 20) {
    turnRight();
    delay(3);
  } else {
    forward();
  }
}

void forward(){
 
  servoLeft.writeMicroseconds(1300);
  servoRight.writeMicroseconds(1700);
  delay(100);

}

void turnRight(){
  servoLeft.writeMicroseconds(1300);
  servoRight.writeMicroseconds(1300);
  delay(1500);
}
void turnLeft(){
  servoLeft.writeMicroseconds(1700);
  servoRight.writeMicroseconds(1700);
  delay(100);
}

  void backward(){
  servoLeft.writeMicroseconds(1700);
  servoRight.writeMicroseconds(1300);
  delay(100);
}

void disableServos(){
  servoLeft.detach();
  servoRight.detach();
  delay(1000);
 
}

void checkflame() {

  digitalWrite (trigPin, LOW);
  delayMicroseconds(2);
  int sensorReading = analogRead(A0);

int range = map(sensorReading, sensorMin, sensorMax, 0, 3);
Serial.println(range);
 switch (range) {
  case 0:     // A fire closer than 1.5 feet away.
  Serial.println("** Close Fire **");
  tone(7,500,500);
  break;
  case 1:    // A fire between 1-3 feet away.
  Serial.println("** Distant Fire **");
  tone(7,500,500);
  break;
  case 2:    // No fire detected.
  Serial.println("No Fire");

  break;    
}

  //tone(7,x); // put your main code here, to run repeatedly:
  //if (x>700){

  //

 
}
void checkping() {

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);  // Sets the trigPin on HIGH state for 10 micro seconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);   // Calculating the distance
  distance = duration * 0.034 / 2;   // Prints the distance on the Serial Monitor
  Serial.print("Distance: ");
  Serial.println(distance);
}
