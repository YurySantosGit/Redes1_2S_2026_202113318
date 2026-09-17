# Proyecto 1 — SmartCity Tech Park

**Curso:** Redes de Computadoras 1  
**Carné:** 202113318  
**Archivo Packet Tracer:** `Proyecto1_202113318.pkt`  
**Estado del documento:** Avance del proyecto  

---

## 1. Objetivo

Diseñar e implementar en Cisco Packet Tracer una red LAN corporativa para **SmartCity Tech Park**, aplicando conceptos de Capa 1 y Capa 2, principalmente:

- VLANs.
- VTP.
- enlaces Trunk y Access.
- PVST.
- EtherChannel mediante LACP.
- redundancia.
- selección de medios físicos.
- documentación y pruebas de conectividad.

> Este documento se irá actualizando conforme avance la implementación de las demás áreas.

---

## 2. Parámetros asignados por carné

Para el carné `202113318`:

| Parámetro | Valor |
|---|---|
| Último dígito `X` | `8` |
| Penúltimo dígito | `1` |
| Dominio VTP | `Smart_1` |
| Contraseña VTP | `proyecto12S2026` |
| VLAN Gerencia | `18` — `GERENCIA` |
| VLAN Investigación | `28` — `INVESTIGACION` |
| VLAN Producción | `38` — `PRODUCCION` |
| VLAN Servidores | `48` — `SERVIDORES` |
| VLAN Visitantes | `58` — `VISITANTES` |
| VLAN nativa | `98` — `NATIVA` |
| EtherChannel | `LACP` |
| STP | `PVST` |
| Banner MOTD | `Acceso Restringido - TechPark_202113318` |

---

# 3. Avance actual — Centro de Datos

El Centro de Datos se inició utilizando dos dispositivos `Switch-PT`:

- `CORE-SW`: switch principal del campus.
- `SERVER-SW`: switch destinado a la granja de servidores.

![Switches iniciales del Centro de Datos](./evidencias/01_switches_centro_datos.png)

Posteriormente se agregaron cuatro servidores:

- `SRV1`
- `SRV2`
- `SRV3`
- `SRV4`

![Dispositivos iniciales del Centro de Datos](./evidencias/02_dispositivos_centro_datos.png)

---

## 3.1 Preparación física de SERVER-SW

`SERVER-SW` utiliza interfaces de cobre para los cuatro servidores y dos interfaces de fibra para la interconexión redundante con `CORE-SW`.

Se instalaron:

- 4 interfaces FastEthernet de cobre.
- 2 interfaces FastEthernet de fibra `100Base-FX`.

![Módulos instalados en SERVER-SW](./evidencias/03_modulos_server_sw.png)

### Justificación

Los servidores se conectan localmente mediante cobre debido a la corta distancia dentro del Centro de Datos. Para el enlace entre switches se utiliza fibra, permitiendo representar un backbone de mayor capacidad y proporcionando interfaces compatibles para EtherChannel.

---

## 3.2 Preparación física de CORE-SW

En `CORE-SW` se instalaron interfaces adicionales de fibra FastEthernet `100Base-FX`, dejando disponibles interfaces para el backbone del campus.

![Módulos de fibra instalados en CORE-SW](./evidencias/04_modulos_core_sw.png)

---

## 3.3 Conexión de servidores

Los cuatro servidores se conectaron a `SERVER-SW` mediante enlaces de cobre.

![Servidores conectados a SERVER-SW](./evidencias/05_servidores_conectados.png)

Los puertos utilizados en `SERVER-SW` son:

| Dispositivo | Puerto de SERVER-SW | Tipo |
|---|---|---|
| SRV1 | `Fa0/1` | Access |
| SRV2 | `Fa1/1` | Access |
| SRV3 | `Fa2/1` | Access |
| SRV4 | `Fa3/1` | Access |

Todos estos puertos se asignaron posteriormente a la VLAN 48 `SERVIDORES`.

---

# 4. EtherChannel entre SERVER-SW y CORE-SW

Se utilizaron dos enlaces de fibra entre los switches:

```text
SERVER-SW Fa4/1  <-------- fibra -------->  CORE-SW Fa4/1
SERVER-SW Fa5/1  <-------- fibra -------->  CORE-SW Fa5/1
```

![Enlaces de fibra SERVER-SW hacia CORE-SW](./evidencias/06_enlaces_fibra_server_core.png)

En `CORE-SW` se verificó que las interfaces utilizadas estuvieran activas.

![Puertos activos en CORE-SW](./evidencias/07_puertos_core_sw.png)

---

## 4.1 Configuración LACP en SERVER-SW

```cisco
enable
configure terminal

hostname SERVER-SW

interface range fastEthernet 4/1 , fastEthernet 5/1
 channel-protocol lacp
 channel-group 1 mode active
exit

end
copy running-config startup-config
```

---

## 4.2 Configuración LACP en CORE-SW

```cisco
enable
configure terminal

hostname CORE-SW

interface range fastEthernet 4/1 , fastEthernet 5/1
 channel-protocol lacp
 channel-group 1 mode active
exit

end
copy running-config startup-config
```

---

## 4.3 Verificación de EtherChannel

Comando utilizado:

```cisco
show etherchannel summary
```

Resultado esperado:

```text
Po1(SU)   LACP   Fa4/1(P) Fa5/1(P)
```

Donde:

- `S`: EtherChannel de Capa 2.
- `U`: Port-Channel en uso.
- `P`: interfaz agregada correctamente al Port-Channel.

### Evidencia CORE-SW

![EtherChannel LACP en CORE-SW](./evidencias/08_lacp_core_sw.png)

### Evidencia SERVER-SW

![EtherChannel LACP en SERVER-SW](./evidencias/09_lacp_server_sw.png)

**Resultado:** el Port-Channel 1 quedó operativo en ambos extremos.

---

# 5. Configuración VTP y VLANs

`CORE-SW` se configuró como servidor VTP.

## 5.1 CORE-SW — VTP Server y creación de VLANs

```cisco
enable
configure terminal

vtp domain Smart_1
vtp mode server
vtp password proyecto12S2026
vtp version 2

spanning-tree mode pvst

vlan 18
 name GERENCIA
exit

vlan 28
 name INVESTIGACION
exit

vlan 38
 name PRODUCCION
exit

vlan 48
 name SERVIDORES
exit

vlan 58
 name VISITANTES
exit

vlan 98
 name NATIVA
exit

end
copy running-config startup-config
```

### Verificación de VLANs

```cisco
show vlan brief
```

![VLANs creadas en CORE-SW](./evidencias/10_vlans_core_sw.png)

---

## 5.2 Verificación VTP en CORE-SW

Comando:

```cisco
show vtp status
```

Parámetros comprobados:

```text
VTP Version        : 2
VTP Operating Mode : Server
VTP Domain Name    : Smart_1
VTP V2 Mode        : Enabled
```

![Estado VTP de CORE-SW](./evidencias/11_vtp_core_sw.png)

---

## 5.3 SERVER-SW — VTP Client

```cisco
enable
configure terminal

vtp domain Smart_1
vtp mode client
vtp password proyecto12S2026
vtp version 2

spanning-tree mode pvst

end
copy running-config startup-config
```

La propagación se comprobó con:

```cisco
show vlan brief
```

Las VLANs recibidas automáticamente fueron:

```text
18  GERENCIA
28  INVESTIGACION
38  PRODUCCION
48  SERVIDORES
58  VISITANTES
98  NATIVA
```

---

# 6. Configuración del trunk sobre Port-Channel 1

El EtherChannel entre `CORE-SW` y `SERVER-SW` se configuró como enlace troncal.

## 6.1 SERVER-SW

```cisco
enable
configure terminal

interface port-channel 1
 switchport mode trunk
 switchport trunk native vlan 98
 switchport trunk allowed vlan 18,28,38,48,58,98
exit

end
copy running-config startup-config
```

## 6.2 CORE-SW

```cisco
enable
configure terminal

interface port-channel 1
 switchport mode trunk
 switchport trunk native vlan 98
 switchport trunk allowed vlan 18,28,38,48,58,98
exit

end
copy running-config startup-config
```

### Verificación

```cisco
show interfaces trunk
```

Se verificó que:

- `Po1` esté en estado `trunking`.
- la encapsulación sea `802.1Q`.
- la VLAN nativa sea `98`.
- las VLANs `18,28,38,48,58,98` estén permitidas y activas.

![Verificación del trunk en CORE-SW](./evidencias/12_trunk_core_sw.png)

---

# 7. VLAN 48 — SERVIDORES

Los puertos de los cuatro servidores fueron configurados como Access dentro de la VLAN 48.

```cisco
enable
configure terminal

interface range fastEthernet 0/1 , fastEthernet 1/1 , fastEthernet 2/1 , fastEthernet 3/1
 switchport mode access
 switchport access vlan 48
exit

end
copy running-config startup-config
```

Verificación:

```cisco
show vlan brief
```

Resultado:

```text
48   SERVIDORES   active   Fa0/1, Fa1/1, Fa2/1, Fa3/1
```

---

# 8. Configuración de PVST y Root Bridge

Por tratarse de un carné par se utiliza `PVST`.

`CORE-SW` se seleccionó como Root Bridge porque funciona como núcleo del campus y concentra los enlaces principales del backbone.

Configuración:

```cisco
enable
configure terminal

spanning-tree vlan 18,28,38,48,58,98 priority 4096

end
copy running-config startup-config
```

Verificación utilizada:

```cisco
show spanning-tree vlan 48
```

Salida obtenida:

```text
VLAN0048
  Spanning tree enabled protocol ieee
  Root ID    Priority    4144
             Address     0030.A36E.B520
             This bridge is the root

  Bridge ID  Priority    4144
             Address     0030.A36E.B520

Interface        Role Sts
---------------- ---- ---
Po1              Desg FWD
Fa4/1            Desg FWD
Fa5/1            Desg FWD
```

La frase:

```text
This bridge is the root
```

confirma que `CORE-SW` es el Root Bridge para la VLAN 48.

> **Captura pendiente:** agregar posteriormente una captura limpia de `show spanning-tree vlan 48`.

---

# 9. Banner MOTD

En `CORE-SW` se configuró:

```cisco
enable
configure terminal

banner motd #Acceso Restringido - TechPark_202113318#

end
copy running-config startup-config
```

Mensaje configurado:

```text
Acceso Restringido - TechPark_202113318
```

> El banner deberá agregarse también a los switches de distribución correspondientes conforme avance el proyecto.

---

# 10. Comandos de verificación utilizados

```cisco
show vlan brief
show vtp status
show etherchannel summary
show interfaces trunk
show spanning-tree vlan 48
```

Posteriormente también se utilizarán:

```cisco
show spanning-tree
show running-config
```

