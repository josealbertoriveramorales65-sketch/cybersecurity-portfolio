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
