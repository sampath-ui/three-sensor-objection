# three-sensor-objection
//we can use this mechanism to detect vehicle in  EV VEHICLES like ADAS EV
#include <LiquidCrystal_I2C.h>
int trig1=4;
int trig2=6;
int trig3=9;
int echo1=3;
int echo2=5;
int echo3=8;
int led=7;
int distance1,distance2,distance3;
int duration1,duration2,duration3;


//define I2C address......
LiquidCrystal_I2C lcd(0x27,16,2);


void setup() {
  lcd.init();
  lcd.clear();
  lcd.backlight();


  pinMode(trig1,OUTPUT);
  pinMode(trig2,OUTPUT);
  pinMode(trig3,OUTPUT);
  pinMode(echo1,INPUT);
  pinMode(echo2,INPUT);
  pinMode(echo3,INPUT);
  pinMode(led,OUTPUT);
  Serial.begin(9600);
  
  lcd.setCursor(2,0);
  lcd.print(" hello sam ");

  

}

void loop() {

  //first sensor;
  digitalWrite(trig1,LOW);
  delayMicroseconds(2);
  digitalWrite(trig1,HIGH);
  delayMicroseconds(10);
  digitalWrite(trig1,LOW);


  duration1 = pulseIn(echo1, HIGH);
  distance1=((duration1*0.034)/2);
  Serial.println("ditance1:");
  Serial.println(distance1);
  delay(1000);
//second sensor
  digitalWrite(trig2,LOW);
  delayMicroseconds(2);
  digitalWrite(trig2,HIGH);
  delayMicroseconds(10);
  digitalWrite(trig2,LOW);


  duration2 = pulseIn(echo2, HIGH);
  distance2=((duration2*0.034)/2);
  Serial.println("ditance2:");
  Serial.println(distance2);
  delay(1000);

  //third sensor
  digitalWrite(trig3,LOW);
  delayMicroseconds(2);
  digitalWrite(trig3,HIGH);
  delayMicroseconds(10);
  digitalWrite(trig3,LOW);


  duration3 = pulseIn(echo3, HIGH);
  distance3=((duration2*0.034)/2);
  Serial.println("ditance3:");
  Serial.println(distance3);
  delay(1000);


  if(distance1<=50)
{
  digitalWrite(led,HIGH);
  delay(1000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("obj is near");
}

if(distance2<=50)
{
  digitalWrite(led,HIGH);
  delay(1000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("obj near rightside");
}
if(distance3<=50)
{
  digitalWrite(led,HIGH);
  delay(1000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("obj near left side");
}







}
