# Nmap - Escaneo de Redes

## ¿Qué es?
Herramienta de código abierto para escaneo de redes y auditoría de seguridad.

## Instalación
```bash
# En Kali Linux ya viene instalado
nmap --version

# En Debian/Ubuntu
sudo apt install nmap
```

## Casos de uso

| Comando | Para qué sirve |
|---|---|
| `nmap IP` | Escaneo básico |
| `nmap -sV IP` | Ver servicios y versiones |
| `nmap -A IP` | Escaneo agresivo completo |
| `nmap -p 80 IP` | Puerto específico |
| `nmap IP/24` | Toda la red |
| `nmap -oN file.txt IP` | Guardar resultados |

## Puertos importantes a conocer

| Puerto | Servicio |
|---|---|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 3389 | RDP (Windows) |

## ⚠️ Importante
Usar Nmap solo en redes propias o con permiso explícito.
Escanear redes ajenas sin permiso es ilegal.
```
