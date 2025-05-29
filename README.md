# OBJETOS-INTELIGENTES-CONECTADOS
# 🌐 Sistema de Monitoramento e Controle IoT com ESP32 e MQTT

Este projeto implementa um sistema de automação baseado em ESP32 com sensores e atuadores controlados remotamente via protocolo MQTT. Permite monitorar temperatura e umidade do ar, além de controlar um LED, um servo motor e uma tira de LEDs WS2812 via comandos pela internet.

## 📌 Descrição do Funcionamento

O sistema se conecta a uma rede Wi-Fi e realiza as seguintes funções:

- Leitura de **temperatura e umidade** do ar via sensor **DHT22**
- Publicação periódica desses dados no tópico MQTT `"Tempdata"`
- Controle remoto de:
  - **LED** simples (GPIO 26)
  - **Servo motor** (GPIO 2), controlado por ângulos de 0 a 180°
  - **Tira de LEDs WS2812** (GPIO 4), controlada por cores RGB via string

É ideal para protótipos IoT, sistemas educacionais e automação doméstica básica.

## 🧠 Software e Código

O código foi desenvolvido na **WOKWI** utilizando as bibliotecas:

- `WiFi.h` para conectividade
- `PubSubClient.h` para MQTT
- `DHT_U.h` e `Adafruit_Sensor.h` para o DHT22
- `ESP32Servo.h` para controle de servo motor
- `FastLED.h` para controle de LEDs WS2812

### Estrutura MQTT

- **Publica em:** `Tempdata` → formato `"temp,hum,"` (ex: `25.6,42.0,`)
- **Assina:**
  - `lights` → `"ON"` ou `"OFF"` para LED simples
  - `servo` → ângulo (ex: `"90"`)
  - `lights/neopixel` → cor RGB (ex: `"255,0,0"` para vermelho)

### Repositório do Projeto

🔗 [GitHub - OBJETOS-INTELIGENTES-CONECTADOS](https://github.com/felippefreyre/OBJETOS-INTELIGENTES-CONECTADOS.git)

## ⚙️ Hardware Utilizado

| Componente         | Função                                                           |
|--------------------|------------------------------------------------------------------|
| ESP32              | Microcontrolador principal com Wi-Fi                            |
| Sensor DHT22       | Leitura de temperatura e umidade do ar                          |
| LED (GPIO 26)      | Indicador de status ON/OFF                                      |
| Servo motor (GPIO 2) | Movimentação via ângulos controlados por MQTT                |
| Tira WS2812 (GPIO 4)| Controle RGB remoto via MQTT                                   |
| Protoboard e jumpers| Montagem dos circuitos                                         |
| Fonte 5V / USB     | Alimentação do sistema                                          |

> *Nota: Este projeto não utiliza sensor de umidade do solo ou bomba de água, por limitações da plaforma WOKWI que ao exceder uma quantidade de componentes precisa assinar uma assinatura premium e por questão financeira não foi viável a versão fisica*


## 📡 Comunicação e Protocolos

- **Conectividade:** Wi-Fi (rede Wokwi-GUEST no protótipo)
- **Protocolo:** MQTT via `broker.hivemq.com` (sem autenticação)
- **Client ID:** definido estaticamente no código
- **Porta:** 1883 (TCP padrão MQTT)

## ✅ Conclusões

### 🎯 Objetivos Alcançados?

Sim. O projeto permitiu:

- Monitoramento ambiental com DHT22
- Publicação dos dados em tempo real
- Controle remoto completo de LED, servo e tira de LED via MQTT

### ⚠️ Principais Desafios e Soluções

- **Reconexão de Wi-Fi e MQTT:** resolvido com lógica de reconexão automática
- **Interpretação de comandos MQTT:** uso de `sscanf()` e `toInt()` para parsing de dados
- **Sincronismo:** uso de `millis()` ao invés de `delay()` para leitura e envio contínuos

### ✅ Vantagens

- Simples, acessível e modular
- Fácil de expandir para outros sensores/atuadores
- Ideal para aprendizado de IoT

### ❌ Desvantagens

- Sem autenticação segura no MQTT
- Depende da conectividade Wi-Fi estável
- Sem armazenamento histórico dos dados

### 💡 Melhorias Futuras

- Implementar TLS/SSL e autenticação no MQTT
- Criar app ou dashboard com visualização dos dados
- Expandir com sensores de luz, gás, presença, etc.
- Armazenamento em banco de dados (Firebase, InfluxDB, etc.)

---

🛠 Projeto desenvolvido por **Felipe Freire**  
📘 Universidade Presbiteriana Mackenzie – 2025  
📎 Contato: [felippefreyre@outlook.com](mailto:felippefreyre@outlook.com)
