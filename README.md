# Sistema Monitorador e Controlador de Pressão (SMCP)

Este repositório contém o código-fonte do projeto **SMCP - Sistema Monitorador e Controlador de Pressão**, desenvolvido para simular o controle de pressão em uma máquina industrial utilizando MQTT e a placa Raspberry Pi Pico W (BitDogLab).

## Objetivo

Desenvolver um sistema capaz de monitorar e controlar o nível de pressão de um fluido, com comunicação entre dois clientes MQTT:

- **Cliente 1 (Pico W):** simula o controle de pressão via joystick, publica os dados de pressão e recebe comandos para alterar a cor de um LED RGB.
- **Cliente 2 (Celular com IOT MQTT Panel):** exibe os dados em tempo real (gráfico e manômetro), e envia comandos de cor para o LED RGB.

## Componentes Utilizados

- Raspberry Pi Pico W (BitDogLab)
- Módulo CYW43439 (Wi-Fi)
- Joystick (eixo Y)
- LED RGB
- Buzzer
- Broker Mosquitto (executado via Termux)
- Aplicativo IOT MQTT Panel

## Funcionamento

- O joystick simula a válvula de controle de pressão, com leitura via ADC.
- A pressão é convertida para uma escala de 0% a 100% e publicada no tópico `/pressure`.
- O aplicativo IOT MQTT Panel assina esse tópico para exibir o valor da pressão.
- O aplicativo também publica no tópico `/rgb_led` uma cor ("green", "yellow", "red" ou "off"), que é recebida pela Pico W.
- A placa acende o LED RGB com a cor recebida e emite um sinal sonoro com o buzzer a cada mudança.

## Tópicos MQTT

- **/pressure**: publica o valor da pressão em porcentagem.
- **/rgb_led**: recebe comandos de cor para o LED RGB.
- **/rgb_led/color**: publica a cor atual do LED como confirmação.
- **/ping**, **/print**, **/exit**: tópicos auxiliares de teste/debug.

## Como Compilar

1. Clone o repositório:
   ```bash
   git clone https://github.com/DanielPortoBraz/Sistema-Monitorador-Controlador-de-Pressao.git
   ```
2. Instale o [Pico SDK](https://github.com/raspberrypi/pico-sdk) e configure o ambiente.
3. Crie uma pasta `build` e entre nela:
   ```bash
   mkdir build && cd build
   cmake ..
   make
   ```
4. Grave o arquivo `.uf2` na placa Pico W.

## Vídeo de Demonstração

## Licença

Este projeto é de uso educacional e foi desenvolvido para fins de aprendizado. Direitos reservados a Daniel Porto Braz.
