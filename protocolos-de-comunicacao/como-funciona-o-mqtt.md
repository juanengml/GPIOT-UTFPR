---
description: MQTT - Protocolos para IoT
---

# Como funciona o MQTT ?

## O que é ?

![](../.gitbook/assets/image%20%2810%29.png)

_Message Queuing Telemetry Transport_ \(MQTT\) é um protocolo de mensagens destinado a sensores e pequenos dispositivos móveis. Seu principal uso é fazer as máquinas trocarem informações, modalidade de comunicação conhecida como _Machine-to-Machine_ \(M2M, ou em português, de máquina para máquina\).

## Como funciona ?

A comunicação entre aparelhos é assíncrona, isso significa que os dados podem ser transmitidos com intervalos em um fluxo estável. Isso ocorre porque ele utiliza um paradigma de publishers \(publicadores\) e subscribers \(assinantes\) baseado em TCP/IP, cliente e servidor/broker.

Seu funcionamento não é complicado: o publicador envia a mensagem ao broker, que enfileira,ordena e envia as informações recebidas aos assinantes \(que podem ser vários aparelhos\). Esses últimos recebem as mensagens que possuem interesse. O TCP/IP citado é uma forma de identificação entre os dispositivos.



