# 🛡️ SOC Lab: Despliegue de Wazuh & Respuesta Activa ante Intrusiones

**Autor:** Franco Aravena | [@francojaq2](https://github.com/francojaq2)
**Especialidad:** Ingeniería en Ciberseguridad (SOC / Blue Team)
**Plataforma:** VMware Workstation — Entorno 100% Aislado
**Fecha:** Mayo 2026

---

## 📋 Resumen Ejecutivo
Este repositorio documenta el despliegue técnico de un laboratorio SOC funcional desde cero. El proyecto abarca el ciclo de vida completo de un incidente: desde el diseño de la infraestructura y la resolución de conflictos de compatibilidad, hasta la simulación de ataques de **Fuerza Bruta (T1110)** y la configuración de **Respuesta Activa (SOAR)** para la contención automática de amenazas.

El objetivo es demostrar competencias en administración de sistemas Linux, ingeniería de detección y automatización de seguridad.

---

## 🏗️ Fase 1: Arquitectura e Infraestructura

### 1.1 Diseño de Red
Se configuró una arquitectura de tres nodos en un segmento de red privado (`172.16.220.0/24`):

| Nodo | Rol | Sistema Operativo | Dirección IP |
| :--- | :--- | :--- | :--- |
| **Wazuh Manager** | SIEM / Analítica | Ubuntu Server 22.04 LTS | `172.16.220.136` |
| **Atacante** | Red Team (Kali) | Kali Linux 2026.1 | `172.16.220.133` |
| **Víctima** | Blue Team (Target) | Ubuntu Server 22.04 LTS | `172.16.220.137` |

### 1.2 Gestión de Desafíos Técnicos (Troubleshooting)

> [!IMPORTANT]
> **Decisión Técnica: Estabilidad vs. Versión**
> Durante el despliegue inicial en Ubuntu 24.04, se identificaron incompatibilidades críticas con las librerías del instalador de Wazuh 4.7.5. Se realizó un **downgrade controlado a Ubuntu 22.04 LTS**, priorizando la estabilidad del entorno SOC y el soporte oficial del fabricante.

**Resolución de Error de Credenciales:**
Tras la instalación, el Dashboard rechazaba el acceso del usuario `admin`.
1. **Diagnóstico:** Desincronización entre el Indexer y el Dashboard.
2. **Solución:** Uso de la herramienta `wazuh-passwords-tool.sh` para resetear usuarios `admin` y `kibanaserver`.
3. **Persistencia:** Actualización manual de secretos en `/etc/wazuh-dashboard/opensearch_dashboards.yml`.

---

## ⚔️ Fase 2: Simulación de Ataque (MITRE ATT&CK)

### 2.1 Reconocimiento (T1595)
Validación de conectividad y servicios expuestos desde la máquina Kali:
```bash
ping -c 4 172.16.220.137
nmap -p 22 172.16.220.137

Resultado: Puerto 22/TCP abierto. Superficie de ataque SSH confirmada.
2.2 Ejecución de Fuerza Bruta (T1110.001)
<img width="847" height="393" alt="Scan puerto 22 Nmap" src="https://github.com/user-attachments/assets/da5c2f88-10d2-4ec9-82ab-92114d75d0b0" />



Simulación de un ataque de diccionario utilizando Hydra y la wordlist rockyou.txt:
hydra -l user_test -P /usr/share/wordlists/rockyou.txt ssh://172.16.220.137 -t 4 -V
<img width="1219" height="628" alt="Eventos de ataque" src="https://github.com/user-attachments/assets/7ae5aa4d-b31e-43be-bc5f-5f63bafbee47" />
<img width="1220" height="629" alt="evento primer ataque" src="https://github.com/user-attachments/assets/3ab32411-cf37-4761-9c8f-b32508f1619c" />



# 🛡️ SOC Lab: Despliegue de Wazuh & Respuesta Activa ante Intrusiones

**Autor:** Franco Aravena | [@francojaq2](https://github.com/francojaq2)
**Especialidad:** Ingeniería en Ciberseguridad (SOC / Blue Team)
**Plataforma:** VMware Workstation — Entorno 100% Aislado
**Fecha:** Mayo 2026


---

## 📋 Resumen Ejecutivo
Este repositorio documenta el despliegue técnico de un laboratorio SOC funcional desde cero. El proyecto abarca el ciclo de vida completo de un incidente: desde el diseño de la infraestructura y la resolución de conflictos de compatibilidad, hasta la simulación de ataques de **Fuerza Bruta (T1110)** y la configuración de **Respuesta Activa (SOAR)** para la contención automática de amenazas.

El objetivo es demostrar competencias en administración de sistemas Linux, ingeniería de detección y automatización de seguridad.

---

## 🏗️ Fase 1: Arquitectura e Infraestructura

### 1.1 Diseño de Red
Se configuró una arquitectura de tres nodos en un segmento de red privado (`172.16.220.0/24`):

| Nodo | Rol | Sistema Operativo | Dirección IP |
| :--- | :--- | :--- | :--- |
| **Wazuh Manager** | SIEM / Analítica | Ubuntu Server 22.04 LTS | `172.16.220.136` |
| **Atacante** | Red Team (Kali) | Kali Linux 2026.1 | `172.16.220.133` |
| **Víctima** | Blue Team (Target) | Ubuntu Server 22.04 LTS | `172.16.220.137` |

### 1.2 Gestión de Desafíos Técnicos (Troubleshooting)

> [!IMPORTANT]
> **Decisión Técnica: Estabilidad vs. Versión**
> Durante el despliegue inicial en Ubuntu 24.04, se identificaron incompatibilidades críticas con las librerías del instalador de Wazuh 4.7.5. Se realizó un **downgrade controlado a Ubuntu 22.04 LTS**, priorizando la estabilidad del entorno SOC y el soporte oficial del fabricante.

**Resolución de Error de Credenciales:**
Tras la instalación, el Dashboard rechazaba el acceso del usuario `admin`.
1. **Diagnóstico:** Desincronización entre el Indexer y el Dashboard.
2. **Solución:** Uso de la herramienta `wazuh-passwords-tool.sh` para resetear usuarios `admin` y `kibanaserver`.
3. **Persistencia:** Actualización manual de secretos en `/etc/wazuh-dashboard/opensearch_dashboards.yml`.

---

## ⚔️ Fase 2: Simulación de Ataque (MITRE ATT&CK)

### 2.1 Reconocimiento (T1595)
Validación de conectividad y servicios expuestos desde la máquina Kali:
```bash
ping -c 4 172.16.220.137
nmap -p 22 172.16.220.137

Resultado: Puerto 22/TCP abierto. Superficie de ataque SSH confirmada.
2.2 Ejecución de Fuerza Bruta (T1110.001)

Simulación de un ataque de diccionario utilizando Hydra y la wordlist rockyou.txt:
Bash

hydra -l user_test -P /usr/share/wordlists/rockyou.txt ssh://172.16.220.137 -t 4 -V

🔍 Fase 3: Análisis de Detección (SIEM)

Wazuh detectó la anomalía mediante la correlación de eventos de los logs de autenticación:

    Alerta 5760 (Nivel 5): Detección individual de fallo de autenticación SSH.

    Alerta 40111 (Nivel 10): Detección crítica de patrón de fuerza bruta (múltiples fallos correlacionados).

    [!TIP]
    Correlación Normativa: El SIEM mapeó automáticamente el ataque con los controles de cumplimiento PCI DSS 10.2.4 y NIST 800-53, facilitando la labor de auditoría.

Se priorizó la monitorización de la regla 40111 sobre la 5760 para evitar fatiga de alertas, enfocando la respuesta activa solo en ataques confirmados por correlación.

🛡️ Fase 4: Respuesta Activa (Contención Automática)

Para minimizar el MTTR (Mean Time To Respond), se implementó un módulo de respuesta automática (Active Response) en el Manager.
4.1 Configuración del Script de Bloqueo

Se configuró el trigger para ejecutar un bloqueo de red ante la detección de la regla 40111:
<active-response>
  <command>firewall-drop</command>
  <location>local</location>
  <rules_id>40111</rules_id>
  <timeout>1800</timeout>
</active-response>
4.2 Resultado de la Mitigación

Al alcanzar el umbral de intentos fallidos, el Manager instruyó al agente de la víctima para ejecutar un firewall-drop.

    Acción: La IP del atacante (172.16.220.133) fue bloqueada en el firewall local de la víctima por 30 minutos.

    Eficacia: El ataque fue neutralizado automáticamente sin intervención humana.

📈 Competencias Demostradas

    Ingeniería de Sistemas: Resolución de dependencias y troubleshooting de servicios críticos.

    Ciberseguridad Ofensiva: Pentesting básico y validación de vulnerabilidades.

    Ciberseguridad Defensiva: Gestión de reglas SIEM y telemetría de agentes.

    Automatización (SOAR): Configuración de respuestas automáticas ante incidentes de seguridad.

Laboratorio realizado con fines educativos en entorno controlado.
---

