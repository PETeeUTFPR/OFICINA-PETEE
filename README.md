# Oficina PET-EE: Controle de LED com ESP32, Botão e App Inventor

Bem-vindo ao repositório da oficina do PET-EE! Este projeto demonstra como criar um sistema interativo com a placa ESP32, onde controlamos e monitoramos componentes de duas formas:

1.  **Controle Físico:** Através de um botão/switch físico conectado à placa.
2.  **Controle e Monitoramento Remoto:** Usando um aplicativo de celular (criado no MIT App Inventor) para:
    * Ligar o LED via Bluetooth.
    * Receber o status do botão físico (pressionado ou solto) em tempo real.

---
[Clique aqui para baixar os Slides em PDF](SLIDES DA APRESENTAÇÃO.pdf)


## 🔌 Circuito

A montagem do circuito é simples. Você precisará conectar um botão ou switch de 3 pinos entre o pino **GPIO 4** e o **GND** do ESP32.

* O **pino do meio** do switch (comum) deve ser conectado ao **GPIO 4**.
* Um dos **pinos do canto** deve ser conectado ao **GND**.



      |                         |
      |       ESP32 DEVKIT      |
      |                         |
      |                  GND o--|---- FIO 1 (CANTO) ----+
      |                         |                      |
      |                   .     |                      |
      |                   .     |                  [SWITCH]
      |                   .     |                      |
      |                GPIO 4 o-|---- FIO 2 (MEIO) -----+
      |                         |
     



## 📱 Aplicativo (MIT App Inventor)

O aplicativo será nossa central de controle e monitoramento. Ele terá duas funções principais: enviar comandos e receber status.

### 1. Enviar Comandos para o ESP32

-   **Ligar o LED:** Teremos um botão virtual no aplicativo. Ao pressioná-lo, o celular enviará um comando de texto (ex: `"ACIONAR_VIRTUAL"`) via Bluetooth para o ESP32. O ESP32, ao receber este comando, irá acionar o LED.

### 2. Receber Status do ESP32

-   **Função "Receber" no Aplicativo:** O aplicativo estará constantemente "ouvindo" as mensagens enviadas pelo ESP32 via Bluetooth.
-   **Status do Botão Físico:** Quando você mover o switch físico, o ESP32 enviará uma mensagem de texto para o aplicativo.
    -   Se o switch for ativado, o ESP32 envia `"BOTAO_PRESSIONADO"`. O aplicativo, ao receber isso, mudará um texto na tela para "Status: Ativado".
    -   Se o switch for desativado, o ESP32 envia `"BOTAO_SOLTO"`. O aplicativo atualizará a tela para "Status: Desativado".

Dessa forma, criamos uma comunicação completa: o celular comanda o ESP32, e o ESP32 reporta o estado de seus componentes de volta para o celular.
```eof
