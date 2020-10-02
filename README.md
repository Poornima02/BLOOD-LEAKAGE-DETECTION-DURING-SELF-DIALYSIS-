# BLOOD-LEAKAGE-DETECTION-DURING-SELF-DIALYSIS
#include <ESP8266WiFi.h>;
#include <WiFiClient.h>;
#include <ThingSpeak.h>;

WiFiClient client;
const char* ssid = "Active Galaxy"; //Your Network SSID
const char* password = "Smilepls@8" ; //Your Network Password
unsigned long myChannelNumber = 993270; //Your Channel Number (Without Brackets)
const char * myWriteAPIKey = "L5E0L8HC5N9Z7LMO"; //Your Write API Key


void setup()
{
  pinMode(2,OUTPUT);pinMode(3,OUTPUT);pinMode(0,INPUT);pinMode(4,OUTPUT);
Serial.begin(9600);
delay(1000);
WiFi.begin(ssid, password);
ThingSpeak.begin(client);
Serial.println(" ");Serial.println("SMART DIALYSER SYSTEM");Serial.println(" ");

}


void loop()

{
int val=analogRead(A0);
ThingSpeak.writeField(myChannelNumber, 1,val, myWriteAPIKey); delay(1000); 
if(val>300)
{
  Serial.println(" ");Serial.println("You are not fit to this process.. contact hospital");Serial.println(" ");
digitalWrite(2,0);digitalWrite(3,0);Serial.println(" ");Serial.println("val");Serial.println(" ");
}
else
{
  
  
  int blo=digitalRead(0);Serial.println(blo);
  if(blo==1)
  {
  digitalWrite(4,1); digitalWrite(2,0);digitalWrite(3,0);Serial.println(" ");Serial.println("Blood leakage detected");Serial.println(" ");
  }
  else
  {
    digitalWrite(4,0);digitalWrite(2,1);digitalWrite(3,1);Serial.println(" "); Serial.println("Be relax");Serial.println(" ");
  }

}Serial.println(" ");Serial.println(" ");
