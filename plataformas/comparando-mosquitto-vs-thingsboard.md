# Comparando MOSQUITTO vs THINGSBOARD

## Comparativos de Pro e Contra de cada Plataforma

Pontos levados em consideração serão

* Interface gráfica
* Aplicabilidade
* Implementação

## 1\) Interface gráfica

### Thingsboard - interface gráfica {^\_^} 

**Tela de Login**

![](../.gitbook/assets/image%20%2812%29.png)

### MOSQUITTO - GUI ?

![N&#xE3;o existe tela grafica apenas terminal](../.gitbook/assets/image%20%281%29.png)

GUI Alternativa -  Não Oficial para MOSQUITTO desenvolvida pela comunidade

{% embed url="https://github.com/sanjeshpathak/Mosquitto-Dashboard" %}

## 2\) Aplicabilidade 

**Thingsboard - É uma plataforma mais efetiva para gerenciar e construir metricas de automação e otimizando tempo na implementação de dispositivos conectados, sua interação consiste em seguir seus tutoriais e passo a passo bem definidos tais com as seguintes etapas:**

1. Cadastrar dispositivos na plataforma
2. Ter em mãos token e ID do dispositivos
3. Implementar token e ID no Código do dispositivo físico
4. Criar uma Dashboard
5. Sincronizar o dispositivo na Dash 
6. FIM



**Mosquitto - Um serviço de Broker muito conhecido pela simplicidade em instalação e facil interação com terminal como bash e PowerShell, sua interação consiste em linhas de comando para interagir com bibliotecas como paho-mqtt do python e também em comando puro como os comandos mosquitto\_pub e mosquito\_sub um publica e o outro recebe. Em linha de comando poderiamos testar da seguinte forma:**

mosquitto\_pub -h 192.168.0.9 -t /home/QUARTO/01 -m "OFF"

**mosquitto\_pub - paramentros** 

**-h - define o host ou numero IP**

**-t - O tópico para envio** 

**-m - a mensagem a ser transmitida**

mosquitto\_sub -h 192.168.0.9 -t /home/QUARTO/\#

**O paramentro \# seguinifica que tudo que for enviado depois do barra \# será recebido em todas os quartos.**

mosquitto\_sub -h 192.168.0.9 -t /home/QUARTO/01/\#

**Nesse caso apelas os dispositivos do quarto 01** 

## 3\) Implementação

### **Thingsboard** 

No arduino é utilizado as pibliotecas bista na parte de protocolos e comunicação, PubSubCliente, Ethernet caso tenha shield e  mqtt.

No ESP32 ou ESP8266 é nescessario PubSub e MQTT.

No Raspberry utiliza-se a biblioteca paho-mqtt

Ambas as placas utilizam os Tokens e IDs para sua integração com a plataforma.

\*\*\*\*

### **Mosquitto** 

  
No Arduino basta utilizar as libs PubSubClient, Ethernet e MQTT.h

No ESP32 ou ESP8266 é nescessario PubSub e MQTT.

No Raspberry utiliza-se a biblioteca paho-mqtt

Não é necessário token para validação em implementações mais simples, em estruturas mais complexas é utilizado um sistema de SSL e TLS para autenticação**.**

\*\*\*\*

## \*\*\*\*





