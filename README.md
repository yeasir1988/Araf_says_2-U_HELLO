# Araf_says_2-U_HELLO
Just learning
https://github.com/
#include <SoftwareSerial.h>
int FierpinA = A1;
int FierStateA = 0; 
int LEDpinA = 12;
//Create software serial object to communicate with SIM800L
SoftwareSerial mySerial(2,8); //SIM800L Tx & Rx is connected to Arduino #3 & #2
void setup()
{
  pinMode(FierpinA,INPUT);
  pinMode(LEDpinA,OUTPUT);
}
  void loop()
{
  FierStateA = digitalRead(FierpinA);
  if(FierStateA == LOW){
  digitalWrite(LEDpinA,HIGH);
  delay(100);
  digitalWrite(LEDpinA,LOW);
  Serial.print(FierStateA);
              //Begin serial communication with Arduino and Arduino IDE (Serial Monitor)
  Serial.begin(9600);
              //Begin serial communication with Arduino and SIM800L
  mySerial.begin(9600);
  Serial.println("Initializing..."); 
  delay(1000);
  mySerial.println("AT"); //Once the handshake test is successful, i t will back to OK
  updateSerial();
  mySerial.println("ATD+ +8801789333514;"); //  change ZZ with country code and xxxxxxxxxxx with phone number to dial
  updateSerial();
  delay(20000); // wait for 20 seconds...
  mySerial.println("ATH"); //hang up
  updateSerial();
} 
}
  void updateSerial()
{
  delay(500);
  while (Serial.available()) 
{
  mySerial.write(Serial.read());//Forward what Serial received to Software Serial Port
}
  while(mySerial.available()) 
{
  Serial.write(mySerial.read());//Forward what Software Serial received to Serial Port
}
  int FierStateA = 1; 
}
