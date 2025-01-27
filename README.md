# Universidad de las Américas  
**Avance del Proyecto - Redes I - Progreso 2**  

**Elaborado Por:**  
Alexander Cahueñas  
Alejandra Fogacho  
Hans Ortiz  
Kamila Revelo  

**Docente Guía:**  
Ing. Javier Alejandro Larrea Sarmiento  

**Fecha de Entrega:**  
13 de diciembre de 2024  

---

## I. Empresa  
**EcuaIntegration Corp S.A.**  

## II. Introducción  
EcuaIntegrationCorp S.A. es una empresa líder en el desarrollo de soluciones tecnológicas empresariales y servicios de consultoría en TI. Fundada en 2021, la empresa ha experimentado un rápido crecimiento y actualmente cuenta con más de 190 empleados distribuidos en sus diferentes departamentos. Su sede principal está ubicada en Quito, con planes de expansión a otras ciudades en Ecuador.  

## III. Descripción de la Empresa  
La empresa se especializa en:  
- Desarrollo de software empresarial personalizado  
- Consultoría en transformación digital  
- Implementación de soluciones cloud  
- Servicios de ciberseguridad  
- Análisis de datos y Business Intelligence  

## IV. Justificación de la LAN  
La implementación de esta red LAN es fundamental para:  
- Asegurar una comunicación eficiente entre departamentos  
- Garantizar el acceso seguro a recursos compartidos  
- Implementar políticas de seguridad por departamento  
- Optimizar el rendimiento de aplicaciones críticas  
- Facilitar la gestión y monitorización de la red  
- Permitir el crecimiento futuro de la infraestructura  

---

## V. Tabla de Subredes (Actualizada con VLSM y 4 Routers)  
| Departamento      | Host Requeridos | Subred             | Máscara | Gateway       | Rango de IPs Útiles      | Broadcast         |  
|--------------------|-----------------|--------------------|---------|---------------|--------------------------|-------------------|  
| **Ventas**         | 100             | 192.168.20.0/25    | /25     | 192.168.20.1  | 192.168.20.2 - 192.168.20.126 | 192.168.20.127    |  
| **Desarrollo**     | 50              | 192.168.20.128/26  | /26     | 192.168.20.129| 192.168.20.130 - 192.168.20.190 | 192.168.20.191    |  
| **Administración** | 25              | 192.168.20.192/27  | /27     | 192.168.20.193| 192.168.20.194 - 192.168.20.222 | 192.168.20.223    |  
| **Servidores**     | 5               | 192.168.20.224/28  | /28     | 192.168.20.225| 192.168.20.226 - 192.168.20.238 | 192.168.20.239    |  
| **Enlaces Seriales** | 2 por enlace  | 192.168.20.240/30  | /30     | -             | 192.168.20.241 - 192.168.20.242 | 192.168.20.243    |  
|                    |                 | 192.168.20.244/30  | /30     | -             | 192.168.20.245 - 192.168.20.246 | 192.168.20.247    |  
|                    |                 | 192.168.20.248/30  | /30     | -             | 192.168.20.249 - 192.168.20.250 | 192.168.20.251    |  

---

## VI. Asignación Detallada de Subredes  
| Departamento      | Subred             | Gateway       | Primera IP | Última IP | Broadcast         |  
|--------------------|--------------------|---------------|------------|-----------|-------------------|  
| Ventas            | 192.168.20.0/25    | 192.168.20.1  | 192.168.20.2 | 192.168.20.126 | 192.168.20.127 |  
| Desarrollo        | 192.168.20.128/26  | 192.168.20.129| 192.168.20.130 | 192.168.20.190 | 192.168.20.191 |  
| Administración    | 192.168.20.192/27  | 192.168.20.193| 192.168.20.194 | 192.168.20.222 | 192.168.20.223 |  
| Servidores        | 192.168.20.224/28  | 192.168.20.225| 192.168.20.226 | 192.168.20.238 | 192.168.20.239 |  

---

## VII. Segmentación de Red y Seguridad  
### 1. VLANs Asignadas  
- **VLAN 10**: Ventas  
- **VLAN 20**: Desarrollo  
- **VLAN 30**: Administración  
- **VLAN 99**: Servidores  

### 2. Políticas de Seguridad  
- Implementación de ACLs entre VLANs.  
- Acceso restringido a servidores mediante autenticación 802.1X.  
- Segmentación de tráfico administrativo.  
- Configuración de SSH en routers y switches (usuario: `admin`, contraseña: `cisco`).  

### 3. Consideraciones Adicionales  
- Firewall perimetral en el router principal (R0).  
- Sistema de detección de intrusiones (IDS).  
- Monitorización de red 24/7 con SNMP.  

---

## VIII. Plan de Implementación  
### Fase 1: Preparación  
- Documentación de la topología actual con 4 routers y enlaces seriales.  
- Inventario de equipos (4 routers ISR331, 4 switches, servidores).  

### Fase 2: Configuración Core  
- Configuración de interfaces seriales en routers:  
  - **R0**: S0/0/0 (`192.168.20.241/30`), S0/0/1 (`192.168.20.245/30`).  
  - **R1**: S0/0/0 (`192.168.20.242/30`), S0/0/1 (`192.168.20.249/30`).  
  - **R2**: S0/0/0 (`192.168.20.246/30`), S0/0/1 (`192.168.20.250/30`).  
  - **R3**: S0/0/0 (`192.168.20.251/30`).  

### Fase 3: Despliegue por Departamentos  
- Configuración de VLANs en switches.  
- Asignación de IPs estáticas a servidores (`192.168.20.226-230`).  

### Fase 4: Optimización  
- Configuración de OSPF para enrutamiento dinámico.  
- Pruebas de conectividad entre departamentos y servidores.  

---

## IX. Diagramación Actualizada  
![Topología](imagen.png)  
- **4 Routers ISR331** con enlaces seriales.  
- **4 Switches** (uno por departamento y servidores).  
- **3 Servidores** (DHCP, DNS/Web, Base de Datos).  

---

## X. Recomendaciones  
- **Monitorización:** Implementar herramientas como PRTG para seguimiento en tiempo real.  
- **Mantenimiento:** Actualizar firmware de routers y switches trimestralmente.  
- **Escalabilidad:** Reservar subredes adicionales (`192.168.20.252/30`) para futuras expansiones.  

---  
**Documentación Adjunta:**  
- Archivo de Packet Tracer con la simulación completa.  
- Cálculos VLSM detallados en formato IEEE.  
