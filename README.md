# Sistemas_Embarcados

Visão Geral

O Projeto teve como objetivo desenvolver um sistema capaz de monitorar a ocorrência de chuva através do sensor de chuva FC-37 conectado a uma placa de ESP32. Além da detecção da chuva, o sistema deveria enviar alertas para um dispositivo móvel utilizando a plataforma Blynk IoT.

#
Código ESP32

#define BLYNK_TEMPLATE_ID "TMPL2KMQMXw_Q"
#define BLYNK_TEMPLATE_NAME "SensorChuva"
#define BLYNK_AUTH_TOKEN "W2V2cqQYsAf710yNjB6s0XAllAp29JlF"
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>

char ssid[] = "IFPE_PLM_MOBILE_ALUNOS";

char pass[] = "alunosifpe";

#define SENSOR_CHUVA 34

void setup() {

  Serial.begin(115200);

  Blynk.begin(BLYNK_AUTH_TOKEN, ssid, pass);

}

void loop() {

  Blynk.run();

  int valorChuva = analogRead(SENSOR_CHUVA);

  Blynk.virtualWrite(V1, valorChuva);

  if (valorChuva > 3200) {
  
    Serial.println("SEM CHUVA");
    
    Blynk.virtualWrite(V2, "Sem chuva");
  
  }
  
  else if (valorChuva > 2000) {
  
    Serial.println("CHUVA FRACA");
  
    Blynk.virtualWrite(V2, "Chuva Fraca 🌧️");
  
  }
  
  else if (valorChuva > 1000) {
  
    Serial.println("CHUVA MODERADA");
    
    Blynk.virtualWrite(V2, "Chuva Moderada 🌧️🌧️");
  
  }
  
  else {
  
    Serial.println("CHUVA FORTE!");
    
    Blynk.virtualWrite(V2, "CHUVA FORTE! ⚠️");
    
    Blynk.logEvent("chuva_forte", "ALERTA! Chuva forte detectada!");
    
    }
  
  }

# 
<img width="1080" height="1160" alt="WhatsApp Image 2026-06-22 at 21 26 44" src="https://github.com/user-attachments/assets/d6bea8a8-4567-4e0e-aeb4-c58bd3a4fe0a" />

Essa é a tela inicial do aplicativo do Blynk IoT, nela é possível ver o volume de chuva e se está forte, moderada ou sem chuva.

#
<img width="1080" height="989" alt="WhatsApp Image 2026-06-22 at 21 49 55" src="https://github.com/user-attachments/assets/ba1f9cf6-4c2c-451d-9422-a9a0e40f9749" />

Essa é a notificação enviada pelo Blynk para o celular, alertando que o nível de chuva está muito forte.
