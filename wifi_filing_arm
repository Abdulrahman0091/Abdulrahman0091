#include <ESP8266WiFi.h>
int cupp = D0; 
int cupn = D1;    
int timerp = D2;  
int timern = D3;      
int Send = D4;
const char* ssid = "Mixologist";
const char* password = "22222222";
float c =0; 
float t =1000;
WiFiServer server(80);
void setup(void)
{ 
  
  Serial.begin(115200);
  delay(10);
  pinMode(cupp,OUTPUT); 
  pinMode(timerp, OUTPUT);
  pinMode(cupn,OUTPUT); 
  pinMode(timern, OUTPUT);
  pinMode(Send, OUTPUT);
  digitalWrite(Send,LOW);
  digitalWrite(cupp,LOW);
  digitalWrite(cupn,LOW);
  digitalWrite(timerp,LOW);
  digitalWrite(timern,LOW);
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);     
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("WiFi connected");
  server.begin();
  Serial.println("Server started");
  Serial.print("Use this URL to connect: ");
  Serial.print("http://");    //URL IP to be typed in mobile/desktop browser
  Serial.print(WiFi.localIP());
  Serial.println("/");
}
void loop() {
  WiFiClient client = server.available();
  if (!client) {return;} 
  Serial.println("new client");
  while(!client.available()){delay(1);}
  String request = client.readStringUntil('\r');
  Serial.println(request);
  client.flush();

   

  int value = LOW;
  int value1 = LOW;
  int value2 = LOW;
  if (request.indexOf("/Up=ON") != -1)  {
     c = c;
     t = t;
  }

  if (request.indexOf("/Cup=ON") != -1)  {   
    c=c+1;
    if(c>=3){c=3;}
    digitalWrite(cupp,HIGH);
    delay(300);
    digitalWrite(cupp,LOW);
    value = HIGH;
  }
  if (request.indexOf("/Cup=OFF") != -1)  {  
     c=c-1;
    if(c<=0){c=0;}
    digitalWrite(cupn,HIGH);
    delay(300);
    digitalWrite(cupn,LOW);
    value = LOW;
  }
 if (request.indexOf("/Timer=ON") != -1)  {   
    t=t+1000;
    if(t>=8000){t=8000;}
    digitalWrite(timerp,HIGH);
    delay(300);
    digitalWrite(timerp,LOW);
    value1 = LOW;
  }
  if (request.indexOf("/Timer=OFF") != -1)  {  
     t=t-1000;
    if(t<=1000){t=1000;}
    digitalWrite(timern,HIGH);
    delay(300);
    digitalWrite(timern,LOW);
    value1 = HIGH;
  }
  if (request.indexOf("/Send=ON") != -1)  {  
    digitalWrite(Send,HIGH);
    delay(300);
    digitalWrite(Send,LOW);
    value2 = HIGH;
    delay(300);
    value2 = LOW;
    c=0;
    t=1000;
  }
  client.println("HTTP/1.1 200 OK");
  client.println("Content-Type: text/html");
  client.println(""); 
  client.println("<!DOCTYPE html><html>");
  client.println("<head><meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">");
  client.println("<link rel=\"icon\" href=\"data:,\">");
  client.println("<style>html { font-family: Helvetica; display: inline-block; margin: 0px auto; text-align: center;}");
  client.println(".button { background-color: #195B6A; border: none; color: white; padding: 8px 50px;");
  client.println("text-decoration: none; font-size: 15px; margin: 1px; cursor: pointer;}");
  client.println(".button2 {background-color: #77878A;}</style></head>");
  client.println("<body><h1>Filling Arm Project</h1>");
  client.print("Cups Number =");
  client.println(c);
  client.println("<br>");
  client.print("Timer =");
  client.println(t);
  client.print(" ms");   
  client.println("<br>");  
  client.println("<br><br>");
  
  if(value == HIGH) 
    client.println("Cup+1");
   else 
    client.print("Cup-1");
  
  client.println("<br><br>");
  client.println("<a href=\"/Cup=ON\"\"><button>Cup+1 </button></a>");
  client.println("<a href=\"/Cup=OFF\"\"><button>Cup-1 </button></a><br />");
  client.println("<br><br>");
  
  if(value1 == HIGH) 
    client.println("Timer+1000");
   else 
    client.print("Timer-1000");
  
  client.println("<br><br>");
  client.println("<a href=\"/Timer=ON\"\"><button>Timer+1000 </button></a>");
  client.println("<a href=\"/Timer=OFF\"\"><button>Timer-1000 </button></a><br />");
 client.println("<br><br>");
  
  if(value2 == HIGH) 
  client.println("Send To Arm");
  client.println("<a href=\"/Send=ON\"\"><button>Send To Arm </button></a>");
  client.println("</html>");

  delay(1);
  Serial.println("Client disonnected");
  Serial.println("");
}
