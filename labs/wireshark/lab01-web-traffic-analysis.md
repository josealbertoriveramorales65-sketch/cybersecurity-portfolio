# Laboratorio 1: Análisis de Tráfico Web (DNS, TCP y TLS)

## Objetivo
Capturar y analizar la secuencia de tráfico web generada al navegar a un sitio HTTPS, identificando la resolución de nombres DNS, el establecimiento de conexión TCP y la negociación del protocolo TLS.

## Herramientas Utilizadas
* Wireshark (Captura e inspección de paquetes)
* Terminal de comandos / PowerShell (`ipconfig /flushdns`)
* Navegador Web

## Secuencia del Flujo de Red

1. **Resolución DNS:**
   * **IP Origen (Cliente):** `192.168.100.10`
   * **Servidor DNS (Gateway):** `192.168.100.1`
   * **Consulta:** Registro tipo A para `example.com`.
   * **Respuesta:** IP devuelta `104.20.23.154`.
   * **Análisis de Seguridad:** Identificación de Transaction IDs para prevención de DNS Spoofing / Cache Poisoning.

2. **TCP Three-Way Handshake:**
   * **Conexión:** `192.168.100.10:58802` -> `104.20.23.154:443`
   * **Trama 1 [SYN]:** Petición de inicio de sesión TCP.
   * **Trama 2 [SYN, ACK]:** Respuesta y sincronización del servidor.
   * **Trama 3 [ACK]:** Confirmación del cliente y sesión establecida.

3. **Negociación TLS y Carga Útil:**
   * Inspección del paquete `Client Hello` (`tls.handshake.type == 1`).
   * Extracción del metadato **SNI (Server Name Indication)** en texto plano (`ogads-pa.clients6.google.com` / `example.com`).
   * Tráfico de datos cifrado identificado en bloques de `Application Data`.

## Conclusiones y Lecciones Aprendidas
* Comprensión de la extracción de metadatos de red (SNI, IPs destino, volumen de tráfico) para investigar incidentes con tráfico cifrado por HTTPS.
* Mapeo completo de la secuencia operativa: Navegador $\rightarrow$ DNS $\rightarrow$ TCP Handshake $\rightarrow$ TLS Handshake $\rightarrow$ Tráfico Cifrado.
### 1. Resolución DNS y Transaction ID
![Consulta DNS](../../images/nombre-exacto-de-tu-archivo.png)

### 2. TCP Three-Way Handshake
![TCP Handshake](../../images/nombre-exacto-de-tu-archivo.png)

### 3. Negociación TLS y Extracción de SNI
![Extracción de SNI](../../images/nombre-exacto-de-tu-archivo.png)<img width="1916" height="767" alt="02_tcp_handshake png" src="https://github.com/user-attachments/assets/eb2a9602-d8e3-4051-9f94-745ed28ee69f" />
<img width="1919" height="972" alt="03_tls_sni_extraction png" src="https://github.com/user-attachments/assets/6fd7f688-c254-4258-b3d9-46e90637ff23" />
<img width="1121" height="874" alt="01_dns_query_analysis png" src="https://github.com/user-attachments/assets/9430034b-35ef-4818-ad82-90ec7a66ee49" />

