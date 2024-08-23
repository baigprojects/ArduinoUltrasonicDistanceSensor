const int trigPin = 13;
const int echoPin = 12;

const int buzzer = 11; 

const int greenLED = 10;
const int yellowLED  = 9;
const int redLED = 8;

long duration;
double distance;
double smoothedDistance = 0;
const int numSamples = 5; 

double maxDistanceInches = 12; 
void setup() {
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPin, INPUT); // Sets the echoPin as an Input
  pinMode(buzzer, OUTPUT);
  pinMode(greenLED, OUTPUT);
  pinMode(yellowLED, OUTPUT);
  pinMode(redLED, OUTPUT);
  digitalWrite(buzzer, LOW); // Set all outputs low
  digitalWrite(greenLED, LOW);
  digitalWrite(yellowLED, LOW);
  digitalWrite(redLED, LOW);
  Serial.begin(9600); // Starts the serial communication
}

void loop() {
  // Clears the trigPin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  // Sets the trigPin on HIGH state for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  
  // Calculating the distance in cm
  distance = duration * 0.034 / 2;
  
  // Convert cm to inches
  distance = distance / 2.54;

  // Smoothing
  smoothedDistance = (smoothedDistance * (numSamples - 1) + distance) / numSamples;

  // Light up lights depending on distance
  if (smoothedDistance < maxDistanceInches && smoothedDistance > 1) {
    digitalWrite(greenLED, HIGH);
  } else {
    digitalWrite(greenLED, LOW);
  }
  
  if (smoothedDistance < (maxDistanceInches * 0.66) && smoothedDistance > 1) {
    digitalWrite(yellowLED, HIGH);
  } else {
    digitalWrite(yellowLED, LOW);
  }
  
  if (smoothedDistance < (maxDistanceInches * 0.33) && smoothedDistance > 1) {
    digitalWrite(redLED, HIGH);
    digitalWrite(buzzer, HIGH); // If too close to sensor, sound the alarm!!
  } else {
    digitalWrite(redLED, LOW);
    digitalWrite(buzzer, LOW); // If not close, turn off alarm
  }
  
  // Prints the distance on the Serial Monitor
  Serial.print("Distance: ");
  Serial.println(smoothedDistance);

  delay(50); // Small delay to stabilize the loop
}
