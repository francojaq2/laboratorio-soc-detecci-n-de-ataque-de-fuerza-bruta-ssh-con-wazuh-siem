
# 🛡️ SOC Lab Portfolio — Wazuh SIEM
 
**Autor:** JAq  
**GitHub:** [@francojaq2](https://github.com/francojaq2)  
**Plataforma:** VMware Workstation — Entorno virtualizado local
 
---
 
## Descripción
 
Laboratorio de ciberseguridad defensiva construido desde cero para simular un entorno SOC (Security Operations Center) profesional. El objetivo es practicar detección, análisis y documentación de ataques reales usando Wazuh como SIEM principal.
 
Todos los ejercicios están realizados en un entorno aislado con fines educativos.
 
---
 
## Entorno del Laboratorio
 
| Rol | Sistema | IP |
|---|---|---|
| 🖥️ SIEM / Manager | Ubuntu Server 22.04 + Wazuh 4.7.5 | 172.16.220.136 |
| 💀 Atacante | Kali Linux 2026.1 | 172.16.220.133 |
| 🎯 Víctima | Ubuntu Server 22.04 | 172.16.220.137 |
 
---
 
## Ejercicios
 
| # | Ejercicio | Herramientas | Estado |
|---|---|---|---|
| 01 | [Ataque de Fuerza Bruta SSH](./ejercicio-01-fuerza-bruta-ssh/informe.md) | Hydra, Nmap, Wazuh | ✅ Completado |
| 02 | Escaneo de puertos con Nmap | Nmap, Wazuh | 🔜 Próximamente |
| 03 | Explotación con Metasploit | Metasploit, Wazuh | 🔜 Próximamente |
| 04 | Respuesta activa con Wazuh | Wazuh Active Response | 🔜 Próximamente |
| 05 | Detección de escalada de privilegios | Linux, Wazuh | 🔜 Próximamente |
 
---
 
## Tecnologías
<img width="1280" height="720" alt="Wazuh clean" src="https://github.com/user-attachments/assets/692d82ff-2523-4880-88da-c7ec93c4f9d3" />
<img width="847" height="393" alt="Scan puerto 22 Nmap" src="https://github.com/user-attachments/assets/6549c5fb-7613-4aa5-a273-4509c6dc8440" />
<img width="1219" height="628" alt="Eventos de ataque" src="https://github.com/user-attachments/assets/d0866376-b17e-4a07-a990-dc2cdd86cb0a" />
<img width="1220" height="629" alt="evento primer ataque" src="https://github.com/user-attachments/assets/22301acc-32d6-4795-97ee-23cc64fb8fb3" />
<img width="1064" height="592" alt="Ataque de fuerza bruta" src="https://github.com/user-attachments/assets/aed438c3-ebab-4065-97be-7b77ab4e31bf" />

 
---
 
## Estructura del Repositorio
 
```
soc-lab-portfolio/
├── README.md
├── ejercicio-01-fuerza-bruta-ssh/
│   ├── informe.md
│   └── evidencias/
│       ├── 01-nmap-puerto-22.png
│       ├── 02-hydra-ejecutando.png
│       ├── 03-wazuh-dashboard.png
│       └── 04-wazuh-alertas.png
```
 
---
 
*Todos los ejercicios se realizan en entorno controlado con fines educativos.*
