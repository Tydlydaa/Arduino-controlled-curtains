#define BLYNK_PRINT Serial

// libraries 
#include <ESP8266WiFi.h> // wifi module library
#include <BlynkSimpleEsp8266.h>  // Blynk App Library

// You should get Auth Token in the Blynk App.
// Go to the Project Settings (nut icon).
char auth[] = "691efdb2f6604e2c85502676d797a2a8";

// Your WiFi credentials.
// Set password to "" for open networks.
char ssid[] = "yourWifiName";
char pass[] = "yourWifiPassword";

// defines pins numbers
const int stepPin = D7; // control of stepper motor driver 
const int dirPin = D8; // control of stepper motor driver
const int MS1 = D2 ; // control of stepper motor driver//
const int MS2 = D3 ; // control of stepper motor driver
const int MS3 = D4 ; // control of stepper motor driver
const int TLACW = D5 ; // push button for move of curtains 
const int TLACH = D0; // push button for reading of point zero of the curtains
const int ENABLE = D1; // control of stepper motor driver
long long stav = 0;
/*int basic is zero*/

bool startup = true;
bool moving = true;
int steps = 0;
int direct = 1;
int pinData = 0; 

void setup() {
  // Sets the two pins as Outputs
  Serial.begin(9600) ;
  pinMode(stepPin, OUTPUT);
  pinMode(dirPin, OUTPUT);
  pinMode(MS1, OUTPUT);
  pinMode(MS2, OUTPUT);
  pinMode(MS3, OUTPUT);
  pinMode(TLACW, INPUT_PULLUP);
  pinMode(TLACB, INPUT_PULLUP);
  pinMode(TLACH, INPUT_PULLUP);
  pinMode(ENABLE, OUTPUT);

  digitalWrite(MS1, HIGH);
  digitalWrite(MS2, HIGH);
  digitalWrite(MS3, LOW);

  Blynk.begin(auth, ssid, pass);
 digitalWrite(ENABLE, 1);

}

void movemove(uint32_t howmuch, int dircetionn) {
  digitalWrite(ENABLE, 0);
  delayMicroseconds(100);
  digitalWrite(dirPin, directionn);
  for (uint32_t x = 0; x < howmuch; x++) {
    digitalWrite(stepPin, HIGH);
    delayMicroseconds(100);
    digitalWrite(stepPin, LOW);
    delayMicroseconds(100);
  }
  digitalWrite(ENABLE, 1);
}

BLYNK_WRITE(V0) //Button Widget is writing to pin V1
{
  pinData = param.asInt(); 
}


void loop() {
  Blynk.run();
  
  // HOME 
  if (startup == true) {
    //Serial.println(digitalRead(TLACH));
    if (digitalRead(TLACH) != LOW){
 //     digitalWrite(ENABLE, 1);
      movemove(100, 1);
      return;
    }
    else {
      startup = false;
      moving = false;
   //   digitalWrite(ENABLE, 0);
    }
  }
  
  /// BUTTON LOGIC
  // if you press the button (true) motor will make 22 steps
  if (moving != true) {
    if (digitalRead(TLACW) == 0 || pinData == 1){
      direct = (direct + 1) % 2;
      moving = true;
  //    digitalWrite(ENABLE, 1);
    }
  }

  if (moving == true) {
    if (steps >= 22 ){
      steps = 0;
      moving = false; 
     // digitalWrite(ENABLE, 0);
    } 
    else if ( steps < 22 ) {
      movemove(1600, direct);
      steps += 1 ;
    }
  }
}
