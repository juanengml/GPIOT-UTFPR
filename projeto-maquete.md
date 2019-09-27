# Projeto Maquete



### **Documentação** 

{% embed url="https://github.com/juanengml/Maquete\_Home\_UTFPR" %}

### **Levantar os problemas da versão 1.0 da maquete**

* Servo motor não funciona como esperado
* Entrada e recebimento de mensagem em ações de entrada ou saída classifica errado se placa está offline na dashboard
* interação com mais de 14 entradas o arduino não consegue organizar em fila qual status enviar
* tempo de resposta entre o controlador e o shield com a plataforma para múltiplos acessos

### **I**nvestigar soluções para o problema do servo \(quem sabe testar o ESP32, mas o mega já é tão potente quanto o ESP, não?\)

Hipótese, pelo fato do arduino não conseguir fazer múltiplas  instruções apenas uma instrução por vez e que quando a instrução do servo é feita o tempo de resposta com a plataforma é estendido e ocorre uma perda de pacote visto que o tempo minimo de envio é em milésimos de segundo com a interação do servo esse tempo é estendido não efetivando a sincronização com a plataforma e por isso a plataforma classificando como dispositivo offline.  

Teste para validação, com um novo dispositivo adicionado o comportamento do servo foi isolado para ser feito por outro dispositivo separado dos demais, criando assim um ambiente com 2 dipositoivos uma para controle do servo é o outro para controle dos leds e de

