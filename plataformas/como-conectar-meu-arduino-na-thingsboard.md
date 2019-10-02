# Como Conectar meu Arduino na ThingsBoard ?

### Descrição do tutorial 

Vamos construir um sisteminha simples que controla um led por meio de uma dashboard

Material Utilizado 

| Quantidade | Descrição |
| :--- | :--- |
| 1 | Arduino |
| 2 | leds\(azul e amarelo\) |
| 2  | resistores |
| 1 | shield ethernet |

![https://alselectro.wordpress.com/2016/10/30/arduino-ethernet-shield-led-onoff-from-webpage/](../.gitbook/assets/image%20%286%29.png)

### Circuito



Adicionando um dispositivo na thingsboard

{% embed url="https://youtu.be/XQf1m4J8LBA" %}

* Meu TOKEN para este tutorial - IqXp6hWXDbtwub10oiDg

### Programando arduino com nosso token

```text
#include <ArduinoJson.h>
#include <PubSubClient.h>
#include <Ethernet.h>

#define TOKEN "IqXp6hWXDbtwub10oiDg" // ThingsBoard Device Auth Token
#define ID_DEVICE "NULL"
// PINOS DO ARDUINO 
#define GPIO2 2
 // PINOS DA THINGSBOARD 
#define GPIO2_PIN 1

void  printIPAddress();
void  reconnect();
void  on_message(const char* topic, byte* payload, unsigned int length);

// configurações de servidor e mac E
byte mac[]    = {  0xDE, 0xED, 0xBA, 0xFE, 0xFE, 0xED };
IPAddress server(200, 134, 31, 225);

// IMPORTANTE: para cada led um novo deve ser adicionado, caso queira addicionar novos leds 

boolean gpioState[] = {false};
EthernetClient ethClient;
PubSubClient client(server, 1883, on_message, ethClient);

// setup 

void setup() {
  Serial.begin(9600);

  pinMode(GPIO2, OUTPUT);

  delay(10);

  if (Ethernet.begin(mac) == 0) {
    Serial.println("Failed to configure Ethernet using DHCP");
  }

  delay(1500);
  printIPAddress();

  client.setServer( server, 1883 );


  client.setCallback(on_message);
}

// LOOP 

void loop() {
  if ( !client.connected() ) {
    reconnect();
  }

  client.loop();
}

/*
  recebe mensagens e trata para controle nas portas do arduino
*/
void on_message(const char* topic, byte* payload, unsigned int length) {

  Serial.println("On message");

  char json[length + 1];
  strncpy (json, (char*)payload, length);
  json[length] = '\0';

  Serial.print("Topic: ");
  Serial.println(topic);
  Serial.print("Message: ");
  Serial.println(json);

  // Decode JSON request
  StaticJsonBuffer<200> jsonBuffer;
  JsonObject& data = jsonBuffer.parseObject((char*)json);

  if (!data.success())
  {
    Serial.println("parseObject() failed");
    return;
  }

  // Check request method
  String methodName = String((const char*)data["method"]);

  if (methodName.equals("getGpioStatus")) {
    // Reply with GPIO status
    String responseTopic = String(topic);
    responseTopic.replace("request", "response");
    client.publish(responseTopic.c_str(), get_gpio_status().c_str());
    client.publish("v1/devices/me/attributes", get_gpio_status().c_str());

} else if (methodName.equals("setGpioStatus")) {
    // Update GPIO status and reply
    set_gpio_status(data["params"]["pin"], data["params"]["enabled"]);
    String responseTopic = String(topic);
    responseTopic.replace("request", "response");
    client.publish(responseTopic.c_str(), get_gpio_status().c_str());
    client.publish("v1/devices/me/attributes", get_gpio_status().c_str());
  }
}


/*
  Atualiza data string para valores dos pinos 
*/
String get_gpio_status() {
  // Prepare gpios JSON payload string
  StaticJsonBuffer<200> jsonBuffer;
  JsonObject& data = jsonBuffer.createObject();
  data[String(GPIO14_PIN)] = gpioState[0] ? true : false;
  char payload[256];
  data.printTo(payload, sizeof(payload));
  String strPayload = String(payload);
  Serial.print("Get gpio status: ");
  Serial.println(strPayload);
  return strPayload;
}



void set_gpio_status(int pin, boolean enabled) {
  switch(pin){
  case GPIO2_PIN:
    digitalWrite(GPIO2, enabled ? HIGH : LOW);
    gpioState[0] = enabled;
    break;
  
   }

}

/* 
  Função: Default para reconectar
*/

void reconnect() {
  // Loop until we're reconnected
  while (!client.connected()) {
    Serial.print("Attempting MQTT connection...");
    // Attempt to connect
    if (client.connect(ID_DEVICE, TOKEN, NULL)) {
      Serial.println("connected");
    } else {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      Serial.println(" try again in 5 seconds");
      // Wait 2 seconds before retrying
      delay(2000);
    }
    Serial.print("Connecting to ThingsBoard node ...");
    // Attempt to connect (clientId, username, password)
    if ( client.connect(ID_DEVICE, TOKEN, NULL) ) {
      Serial.println( "[DONE]" );
      // Subscribing to receive RPC requests
      client.subscribe("v1/devices/me/rpc/request/+");
      // Sending current GPIO status
      Serial.println("Sending current GPIO status ...");
      client.publish("v1/devices/me/attributes", get_gpio_status().c_str());
    } else {
      Serial.print( "[FAILED] [ rc = " );
      Serial.print( client.state() );
      Serial.println( " : retrying in 5 seconds]" );
      // Wait 5 seconds before retrying
      delay( 5000 );
    }
  }
}


void printIPAddress()
{
  Serial.print("My IP address: ");
  for (byte thisByte = 0; thisByte < 4; thisByte++) {
    // print the value of each byte of the IP address:
    Serial.print(Ethernet.localIP()[thisByte], DEC);
    Serial.print(".");
  }
 
  Serial.println();
}




```



### Construindo nossa dashboard





