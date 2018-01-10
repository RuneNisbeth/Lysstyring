#include <ESP8266WiFi.h>
#include <ThingSpeak.h>
#include <SimpleTimer.h>

// replace with your Network details
const char* ssid = "Runes telefon";
const char* password = "burn5133";
WiFiClient client; 
SimpleTimer timer;

unsigned long channelID = 399915; //your channel
const char* myWriteAPIKey = "JGBT8HLGK1ASWQS7"; //Your API
const char* server = "api.thingspeak.com"; 
const int postingInterval = 20*1000; //20 sekunder

void transmit(){
  ThingSpeak.setField(2, 2); //"1" is the first channel og "2" er variablen. 
  ThingSpeak.writeFields(channelID, myWriteAPIKey); //ChannelID: 399915, APIKey: "JGBT8HLGK1ASWQS7"
  client.stop();
  Serial.println("Hej");
  //delay(postingInterval); //wait 20 sekunder.
}

void speak(){
  Serial.println("hej");
}

void setup() {
  Serial.begin(9600);
  ThingSpeak.begin(client);
  WiFi.begin(ssid, password);
  Serial.println("START");
  timer.setInterval(20000, transmit );
}

void loop() {
  timer.run();
  //transmit();
  //delay(20000);
}


