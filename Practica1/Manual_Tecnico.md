# Manual Técnico

## Práctica 1 - QuetzalDev S.A.

| Información | Detalle |
|---|---|
| **Curso** | Redes de Computadoras 1 |
| **Universidad** | Universidad de San Carlos de Guatemala |
| **Facultad** | Facultad de Ingeniería |
| **Carrera** | Ingeniería en Ciencias y Sistemas |
| **Carnet** | 202113318 |
| **Semestre** | Segundo Semestre 2026 |

---

## Índice

1. [Introducción](#1-introducción)
2. [Descripción General de la Red](#2-descripción-general-de-la-red)
3. [Diseño de la Topología Física](#3-diseño-de-la-topología-física)
4. [Cuarto de Telecomunicaciones - MDF](#4-cuarto-de-telecomunicaciones---mdf)
5. [Puntos y Tomas de Red](#5-puntos-y-tomas-de-red)
6. [Cableado Estructurado](#6-cableado-estructurado)
7. [Medios de Transmisión](#7-medios-de-transmisión)
8. [Estimación de Distancias de Cableado](#8-estimación-de-distancias-de-cableado)
9. [Inventario de Equipos](#9-inventario-de-equipos)
10. [Verificación de Capacidad de Patch Panels y Switches](#10-verificación-de-capacidad-de-patch-panels-y-switches)
11. [Canalización del Cableado](#11-canalización-del-cableado)
12. [Rack del MDF](#12-rack-del-mdf)
13. [Respaldo de Energía - UPS](#13-respaldo-de-energía---ups)
14. [Estándares T568A y T568B](#14-estándares-t568a-y-t568b)
15. [Tipo de Cable por Enlace](#15-tipo-de-cable-por-enlace)
16. [Etiquetado del Cableado](#16-etiquetado-del-cableado)
17. [Comparación con el Estándar TIA/EIA-606](#17-comparación-con-el-estándar-tiaeia-606)
18. [Flujo de Conexión End-to-End](#18-flujo-de-conexión-end-to-end)
19. [Consideraciones de Escalabilidad Futura](#19-consideraciones-de-escalabilidad-futura)
20. [Presupuesto Estimado](#20-presupuesto-estimado)
21. [Conclusiones](#21-conclusiones)
22. [Referencias](#22-referencias)

---

## 1. Introducción

El presente Manual Técnico documenta el diseño físico de la infraestructura de red propuesta para QuetzalDev S.A., considerando la distribución de los departamentos, dispositivos finales, switches, puntos de red, cableado estructurado, canalización y elementos de telecomunicaciones requeridos para su implementación.

La propuesta se desarrolla desde el enfoque de la Capa 1 del modelo OSI, por lo que se concentra principalmente en los componentes físicos de la red, incluyendo el cableado horizontal, el cableado troncal, las tomas de red, patch panels, fibra óptica, ODF, rack, sistema de respaldo eléctrico y medios de transmisión.

El diseño contempla un total de **48 dispositivos finales**, distribuidos entre computadoras de escritorio, laptops y servidores ubicados en ocho áreas de la empresa. Cada departamento dispone de un switch local conectado mediante cableado troncal hacia un switch principal ubicado en el cuarto de telecomunicaciones principal o MDF.

Para el cableado horizontal se propone utilizar **UTP categoría 6**, mientras que para los ocho enlaces troncales se utilizará **fibra óptica multimodo**. Además, se definen criterios de etiquetado, estimaciones de distancia, capacidad de crecimiento, estándares de terminación T568A y T568B, organización del cableado y un presupuesto estimado de los componentes requeridos.

El objetivo del manual es proporcionar una referencia técnica clara y organizada que permita comprender la estructura física de la red propuesta y sirva como base para una posible implementación, mantenimiento o ampliación futura de la infraestructura de QuetzalDev S.A.

---

## 2. Descripción General de la Red

QuetzalDev S.A. cuenta con un edificio corporativo de un solo nivel en el cual se encuentran distribuidos los departamentos de Recepción, Recursos Humanos, Legal, Sala de Capacitación, Diseño e Innovación, Dirección General, Backend y Data Center.

La infraestructura propuesta corresponde a una red de área local (LAN) diseñada desde el punto de vista físico, considerando la distribución de los dispositivos, switches departamentales, puntos de red, cableado horizontal, cableado troncal y un cuarto de telecomunicaciones principal (MDF).

La empresa dispone de un total de **48 dispositivos finales**, distribuidos en **30 computadoras de escritorio, 12 laptops y 6 servidores**. Cada área contará con un switch encargado de conectar sus dispositivos finales, mientras que un switch principal ubicado en el MDF permitirá la interconexión con los ocho switches de área.

### 2.1 Distribución de Dispositivos

La distribución de las computadoras de escritorio y laptops se realizó considerando la cantidad total de dispositivos especificada para cada departamento y manteniendo los totales establecidos para la empresa.

| Área / Departamento  | PCs de escritorio | Laptops | Servidores | Total de dispositivos |
| -------------------- | ----------------: | ------: | ---------: | --------------------: |
| Recepción            |                 2 |       1 |          1 |                     4 |
| Recursos Humanos     |                 7 |       1 |          0 |                     8 |
| Legal                |                 2 |       2 |          0 |                     4 |
| Sala de Capacitación |                 8 |       2 |          0 |                    10 |
| Diseño e Innovación  |                 5 |       2 |          1 |                     8 |
| Dirección General    |                 2 |       2 |          0 |                     4 |
| Backend              |                 4 |       2 |          1 |                     7 |
| Data Center          |                 0 |       0 |          3 |                     3 |
| **Total**            |            **30** |  **12** |      **6** |                **48** |

Cada uno de los 48 dispositivos representa inicialmente un enlace de cableado horizontal hacia el switch correspondiente a su área.

En total se consideran:

* **48 enlaces horizontales** entre los switches departamentales y los dispositivos finales.
* **8 enlaces troncales**, uno desde el MDF hacia cada switch de área.
* **8 switches de área**.
* **1 switch principal** ubicado en el MDF.

---

## 3. Diseño de la Topología Física

### 3.1 Topología General del Edificio

Para la infraestructura general de QuetzalDev S.A. se propone una **topología física jerárquica tipo árbol o estrella extendida**.

El nivel principal de la topología estará formado por el switch central ubicado en el cuarto de telecomunicaciones (MDF). Desde este equipo partirá un enlace troncal independiente hacia el switch correspondiente a cada una de las ocho áreas de la empresa.

Cada switch departamental funcionará posteriormente como nodo central de una topología en estrella para conectar los dispositivos finales de su respectivo departamento.

La estructura general puede representarse de la siguiente manera:

```text
                              MDF
                               │
                      ┌────────┴────────┐
                      │ Switch Principal│
                      └────────┬────────┘
                               │
        ┌───────────┬───────────┬───────────┬───────────┬───────────┬───────────┬───────────┬
        │           │           │           │           │           │           │           │
        ▼           ▼           ▼           ▼           ▼           ▼           ▼           ▼
   ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐
   │ Switch  │ │ Switch  │ │ Switch  │ │ Switch  │ │ Switch  │ │ Switch  │ │ Switch  │ │ Switch  │
   │Recepción│ │  RRHH   │ │  Legal  │ │Capacit. │ │ Diseño  │ │Dirección│ │ Backend │ │Data Ctr.│
   └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘
        │           │           │           │           │           │           │           │
        ▼           ▼           ▼           ▼           ▼           ▼           ▼           ▼
     4 Hosts     8 Hosts     4 Hosts     10 Hosts     8 Hosts     4 Hosts     7 Hosts     3 Servidores
```

En esta estructura, el **switch principal ubicado en el MDF** constituye el punto central de distribución. Desde él parten los ocho enlaces troncales hacia los switches correspondientes a Recepción, Recursos Humanos, Legal, Sala de Capacitación, Diseño e Innovación, Dirección General, Backend y Data Center.

A partir de cada switch departamental se distribuyen los enlaces horizontales hacia las computadoras de escritorio, laptops y servidores asignados a cada área.


El uso de una estructura jerárquica facilita la organización del cableado, permite identificar claramente los enlaces de cada departamento y ofrece capacidad de crecimiento sin necesidad de modificar completamente la infraestructura existente.

### 3.2 Topología por Departamento

Para cada departamento se seleccionó una **topología física en estrella**. En esta topología, cada PC, laptop o servidor se conecta mediante un enlace independiente hacia el switch de su área.

La elección se realizó debido a que la infraestructura especificada para QuetzalDev ya establece la existencia de un switch en cada departamento. La topología estrella permite centralizar las conexiones, simplificar la administración del cableado y aislar fallas de enlaces individuales.

| Departamento         | Hosts | Topología | Justificación                                                                                                                      |
| -------------------- | ----: | --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Recepción            |     4 | Estrella  | La pequeña cantidad de dispositivos puede conectarse directamente al switch del área de forma sencilla y organizada.               |
| Recursos Humanos     |     8 | Estrella  | Permite administrar los ocho dispositivos mediante conexiones independientes y facilita futuras ampliaciones.                      |
| Legal                |     4 | Estrella  | No requiere una topología más compleja debido a la cantidad reducida de dispositivos.                                              |
| Sala de Capacitación |    10 | Estrella  | Al ser el área con mayor cantidad de estaciones, la conexión centralizada simplifica la distribución y mantenimiento del cableado. |
| Diseño e Innovación  |     8 | Estrella  | Permite conectar de forma independiente las estaciones de trabajo y el servidor asignado al departamento.                          |
| Dirección General    |     4 | Estrella  | Proporciona una infraestructura sencilla, ordenada y suficiente para la cantidad actual de equipos.                                |
| Backend              |     7 | Estrella  | Centraliza las computadoras, laptops y servidor del departamento mediante el switch local.                                         |
| Data Center          |     3 | Estrella  | Los tres servidores principales se conectarán directamente al switch asignado al Data Center.                                      |

Una ventaja importante de esta topología es que una falla en el cable de un dispositivo afecta únicamente a dicho equipo y no al resto de los hosts del departamento. Asimismo, la disponibilidad de puertos libres en los switches permitirá agregar dispositivos en el futuro.

### 3.3 Diagrama de Diseño Físico

El siguiente diagrama representa la distribución física propuesta para la red de QuetzalDev S.A.

En el plano se muestran:

- La ubicación de los ocho departamentos.
- El cuarto de telecomunicaciones principal (MDF).
- El switch principal ubicado en el MDF.
- Los ocho switches departamentales.
- Las computadoras de escritorio, laptops y servidores.
- Los puntos y tomas de red.
- El cableado horizontal UTP Cat 6.
- El cableado troncal mediante fibra óptica multimodo.
- Las rutas principales de distribución del cableado.

Para facilitar la interpretación del diseño se utilizó la siguiente representación:

- **Verde:** cableado horizontal UTP Cat 6.
- **Azul:** cableado troncal de fibra óptica multimodo.
- **PC:** computadora de escritorio.
- **LAP:** laptop.
- **SRV:** servidor.
- **SW:** switch.
- **PR:** punto de red.
- **MDF:** cuarto de telecomunicaciones principal.

![Diagrama físico de la red de QuetzalDev S.A.](./img/Diagrama_Fisico_QuetzalDev.png)

**Figura 1. Diagrama de diseño físico propuesto para QuetzalDev S.A.**

---

## 4. Cuarto de Telecomunicaciones - MDF

### 4.1 Ubicación Propuesta

Se propone ubicar el **cuarto de telecomunicaciones principal (MDF)** en una zona central del edificio, próxima al **Hall Central y al Vestíbulo de Ingreso**.

El MDF no se colocará directamente en el área abierta de circulación. Se propone destinar un **espacio cerrado y de acceso restringido cercano a esta zona central**, destinado exclusivamente al equipo de telecomunicaciones y sus sistemas de soporte.

La ubicación exacta será identificada gráficamente en el diagrama de diseño físico.

### 4.2 Justificación de la Ubicación

La ubicación propuesta fue seleccionada principalmente por su **centralidad con respecto a los departamentos del edificio**.

Inicialmente se consideró utilizar el Data Center como ubicación del switch principal; sin embargo, el Data Center se encuentra desplazado hacia el extremo superior derecho del plano. Esto incrementaría las distancias hacia departamentos como Recursos Humanos, Sala de Capacitación y Dirección General.

También se analizaron áreas como Recepción y Sala de Capacitación. Aunque presentan posiciones relativamente favorables, son espacios destinados a la atención o permanencia de personas y no resultan apropiados para alojar de forma permanente infraestructura central de telecomunicaciones.

La zona próxima al Hall Central y Vestíbulo ofrece un mejor equilibrio debido a los siguientes factores:

* **Centralidad:** se encuentra aproximadamente en el centro geométrico del edificio principal.
* **Reducción de distancias:** permite distribuir los enlaces hacia los departamentos de ambos extremos sin concentrar recorridos excesivamente largos en un solo lado.
* **Seguridad:** al utilizar un espacio cerrado y dedicado se limita el acceso de personas no autorizadas.
* **Mantenimiento:** permite que el personal técnico acceda al equipo sin intervenir directamente en las áreas de trabajo.
* **Distribución del cableado:** su posición facilita la salida de rutas de canalización hacia los sectores izquierdo, derecho y superior del edificio.
* **Conexión con el Data Center:** aunque el Data Center no se encuentra inmediatamente junto al MDF, la distancia estimada de su recorrido se encuentra aproximadamente **22 metros**, por lo que continúa siendo viable la interconexión mediante el cableado troncal propuesto.

Dentro del MDF se contempla la instalación del switch principal, elementos de terminación del cableado, organización de fibra, rack y el sistema de respaldo eléctrico correspondiente.

---

## 5. Puntos y Tomas de Red

La infraestructura física propuesta para QuetzalDev S.A. contempla un total de **48 puntos de red**, correspondientes a las 30 computadoras de escritorio, 12 laptops y 6 servidores definidos para la empresa.

Cada dispositivo final dispondrá de un puerto de red independiente. Sin embargo, cuando varios dispositivos se encuentren físicamente próximos, sus puertos podrán agruparse dentro de una misma toma doble, triple o de varios puertos.

Para evitar confusiones se utilizarán dos tipos de identificación:

* **Identificador de la toma física:** permite identificar la caja o salida instalada físicamente, por ejemplo `REC-T01`.
* **Identificador del punto de red:** corresponde al formato de etiquetado solicitado para la práctica, por ejemplo `Recepcion-PR01`.

Por lo tanto, una toma física puede contener uno o varios puntos de red independientes.

Ejemplo:

```text
REC-T01
├── Recepcion-PR01
├── Recepcion-PR02
└── Recepcion-PR03
```

En este caso, `REC-T01` representa una toma triple y cada uno de sus tres puertos posee una etiqueta independiente.

### 5.1 Distribución General de Puntos de Red

| Área / Departamento  | Dispositivos finales | Puntos de red requeridos |
| -------------------- | -------------------: | -----------------------: |
| Recepción            |                    4 |                        4 |
| Recursos Humanos     |                    8 |                        8 |
| Legal                |                    4 |                        4 |
| Sala de Capacitación |                   10 |                       10 |
| Diseño e Innovación  |                    8 |                        8 |
| Dirección General    |                    4 |                        4 |
| Backend              |                    7 |                        7 |
| Data Center          |                    3 |                        3 |
| **Total**            |               **48** |                   **48** |

Cada punto representa un enlace independiente de cableado horizontal entre el dispositivo final y el switch correspondiente al área.

---

### 5.2 Departamento de Recepción

Recepción dispone de cuatro dispositivos finales: dos computadoras de escritorio, una laptop y un servidor.

Se propone utilizar una toma triple para los tres dispositivos de usuario y una toma unitaria independiente para el servidor.

| Toma física | Tipo     | Cantidad de puertos | Etiquetas de puntos de red                           |
| ----------- | -------- | ------------------: | ---------------------------------------------------- |
| REC-T01     | Triple   |                   3 | `Recepcion-PR01`, `Recepcion-PR02`, `Recepcion-PR03` |
| REC-T02     | Unitaria |                   1 | `Recepcion-PR04`                                     |

**Total de puntos:** 4.

---

### 5.3 Departamento de Recursos Humanos

Recursos Humanos dispone de ocho dispositivos finales: siete computadoras de escritorio y una laptop.

Debido a la distribución de las estaciones de trabajo, se proponen cuatro tomas dobles.

| Toma física | Tipo  | Cantidad de puertos | Etiquetas de puntos de red                     |
| ----------- | ----- | ------------------: | ---------------------------------------------- |
| RRHH-T01    | Doble |                   2 | `RecursosHumanos-PR01`, `RecursosHumanos-PR02` |
| RRHH-T02    | Doble |                   2 | `RecursosHumanos-PR03`, `RecursosHumanos-PR04` |
| RRHH-T03    | Doble |                   2 | `RecursosHumanos-PR05`, `RecursosHumanos-PR06` |
| RRHH-T04    | Doble |                   2 | `RecursosHumanos-PR07`, `RecursosHumanos-PR08` |

**Total de puntos:** 8.

---

### 5.4 Departamento Legal

El Departamento Legal dispone de cuatro dispositivos finales: dos computadoras de escritorio y dos laptops.

Se proponen dos tomas dobles.

| Toma física | Tipo  | Cantidad de puertos | Etiquetas de puntos de red |
| ----------- | ----- | ------------------: | -------------------------- |
| LEG-T01     | Doble |                   2 | `Legal-PR01`, `Legal-PR02` |
| LEG-T02     | Doble |                   2 | `Legal-PR03`, `Legal-PR04` |

**Total de puntos:** 4.

---

### 5.5 Sala de Capacitación

La Sala de Capacitación dispone de diez dispositivos finales: ocho computadoras de escritorio y dos laptops.

Debido a que las estaciones se encuentran agrupadas dentro del área de capacitación, se proponen cinco tomas dobles.

| Toma física | Tipo  | Cantidad de puertos | Etiquetas de puntos de red               |
| ----------- | ----- | ------------------: | ---------------------------------------- |
| CAP-T01     | Doble |                   2 | `Capacitacion-PR01`, `Capacitacion-PR02` |
| CAP-T02     | Doble |                   2 | `Capacitacion-PR03`, `Capacitacion-PR04` |
| CAP-T03     | Doble |                   2 | `Capacitacion-PR05`, `Capacitacion-PR06` |
| CAP-T04     | Doble |                   2 | `Capacitacion-PR07`, `Capacitacion-PR08` |
| CAP-T05     | Doble |                   2 | `Capacitacion-PR09`, `Capacitacion-PR10` |

**Total de puntos:** 10.

---

### 5.6 Departamento de Diseño e Innovación

Diseño e Innovación dispone de ocho dispositivos finales: cinco computadoras de escritorio, dos laptops y un servidor.

Para las estaciones de trabajo se proponen tres tomas dobles y una toma unitaria. El servidor utilizará una toma unitaria independiente.

| Toma física | Tipo     | Cantidad de puertos | Etiquetas de puntos de red                       |
| ----------- | -------- | ------------------: | ------------------------------------------------ |
| DIS-T01     | Doble    |                   2 | `DisenoInnovacion-PR01`, `DisenoInnovacion-PR02` |
| DIS-T02     | Doble    |                   2 | `DisenoInnovacion-PR03`, `DisenoInnovacion-PR04` |
| DIS-T03     | Doble    |                   2 | `DisenoInnovacion-PR05`, `DisenoInnovacion-PR06` |
| DIS-T04     | Unitaria |                   1 | `DisenoInnovacion-PR07`                          |
| DIS-T05     | Unitaria |                   1 | `DisenoInnovacion-PR08`                          |

**Total de puntos:** 8.

---

### 5.7 Dirección General

Dirección General dispone de cuatro dispositivos finales: dos computadoras de escritorio y dos laptops.

Se proponen dos tomas dobles.

| Toma física | Tipo  | Cantidad de puertos | Etiquetas de puntos de red                       |
| ----------- | ----- | ------------------: | ------------------------------------------------ |
| DIR-T01     | Doble |                   2 | `DireccionGeneral-PR01`, `DireccionGeneral-PR02` |
| DIR-T02     | Doble |                   2 | `DireccionGeneral-PR03`, `DireccionGeneral-PR04` |

**Total de puntos:** 4.

---

### 5.8 Departamento de Backend

Backend dispone de siete dispositivos finales: cuatro computadoras de escritorio, dos laptops y un servidor.

Los seis equipos de usuario se agruparán mediante tres tomas dobles. El servidor contará con una toma unitaria independiente.

| Toma física | Tipo     | Cantidad de puertos | Etiquetas de puntos de red     |
| ----------- | -------- | ------------------: | ------------------------------ |
| BACK-T01    | Doble    |                   2 | `Backend-PR01`, `Backend-PR02` |
| BACK-T02    | Doble    |                   2 | `Backend-PR03`, `Backend-PR04` |
| BACK-T03    | Doble    |                   2 | `Backend-PR05`, `Backend-PR06` |
| BACK-T04    | Unitaria |                   1 | `Backend-PR07`                 |

**Total de puntos:** 7.

---

### 5.9 Data Center

El Data Center dispone de tres servidores principales.

Debido a que los tres servidores se encontrarán concentrados dentro del mismo espacio técnico, se propone una terminación de tres puertos dedicada al área de servidores.

| Toma física / terminación | Tipo               | Cantidad de puertos | Etiquetas de puntos de red                              |
| ------------------------- | ------------------ | ------------------: | ------------------------------------------------------- |
| DC-T01                    | Triple / 3 puertos |                   3 | `DataCenter-PR01`, `DataCenter-PR02`, `DataCenter-PR03` |

**Total de puntos:** 3.

---

### 5.10 Resumen de Tomas de Red

| Área / Departamento  | Tomas unitarias | Tomas dobles | Tomas triples | Cantidad de tomas físicas | Puertos de red |
| -------------------- | --------------: | -----------: | ------------: | ------------------------: | -------------: |
| Recepción            |               1 |            0 |             1 |                         2 |              4 |
| Recursos Humanos     |               0 |            4 |             0 |                         4 |              8 |
| Legal                |               0 |            2 |             0 |                         2 |              4 |
| Sala de Capacitación |               0 |            5 |             0 |                         5 |             10 |
| Diseño e Innovación  |               2 |            3 |             0 |                         5 |              8 |
| Dirección General    |               0 |            2 |             0 |                         2 |              4 |
| Backend              |               1 |            3 |             0 |                         4 |              7 |
| Data Center          |               0 |            0 |             1 |                         1 |              3 |
| **Total**            |           **4** |       **19** |         **2** |                    **25** |         **48** |

En total se proponen **25 ubicaciones físicas de tomas**, las cuales proporcionan los **48 puertos de red** requeridos por los dispositivos de QuetzalDev S.A.

---

### 5.11 Criterio de Etiquetado de los Puntos

Para los puntos correspondientes al cableado horizontal se utilizará el formato establecido para la práctica:

```text
[Área/Departamento]-[Número de Punto de Red]
```

Ejemplos:

```text
Recepcion-PR01
RecursosHumanos-PR04
Legal-PR03
Capacitacion-PR08
DisenoInnovacion-PR05
DireccionGeneral-PR02
Backend-PR07
DataCenter-PR03
```

El identificador será asociado al puerto de la toma, al cable correspondiente y a su terminación dentro del sistema de distribución, permitiendo reconocer de forma clara el origen y destino de cada enlace.

El etiquetado de los **enlaces troncales** utiliza el siguiente formato:

```text
MDF-[Área/Departamento]
```

Por ejemplo:

```text
MDF-Recepcion
MDF-RecursosHumanos
MDF-Legal
MDF-Capacitacion
MDF-DisenoInnovacion
MDF-DireccionGeneral
MDF-Backend
MDF-DataCenter
```

La comparación entre este esquema simplificado y el estándar **TIA/EIA-606** se presenta en la sección 17 del presente Manual Técnico.


---
## 6. Cableado Estructurado

El diseño físico de la red de QuetzalDev S.A. se basa en un sistema de cableado estructurado que permite organizar las conexiones entre el cuarto de telecomunicaciones, los switches de cada departamento y los dispositivos finales.

Para facilitar la administración de la infraestructura se diferencian dos segmentos principales:

* **Cableado troncal o backbone:** encargado de interconectar el MDF con los switches de cada área.
* **Cableado horizontal:** encargado de conectar los switches departamentales con las computadoras, laptops y servidores correspondientes.

Esta separación permite mantener una infraestructura organizada, facilitar las tareas de mantenimiento y permitir futuras ampliaciones de la red.

---

### 6.1 Cableado Horizontal

El cableado horizontal corresponde a los enlaces existentes entre el **switch de cada departamento y sus dispositivos finales**.

Dentro de QuetzalDev S.A. se consideran como dispositivos finales:

* Computadoras de escritorio.
* Laptops.
* Servidores.

Cada dispositivo tendrá un enlace independiente hacia el switch correspondiente a su departamento.

La estructura básica será:

```text
Dispositivo final
       │
       │ Cableado horizontal
       │
Switch del departamento
```

Por ejemplo:

```text
PC Recursos Humanos
        │
        │ UTP Cat 6
        │
Switch Recursos Humanos
```

La red contempla un total de **48 enlaces horizontales**, distribuidos de la siguiente forma:

| Área / Departamento  | Enlaces horizontales |
| -------------------- | -------------------: |
| Recepción            |                    4 |
| Recursos Humanos     |                    8 |
| Legal                |                    4 |
| Sala de Capacitación |                   10 |
| Diseño e Innovación  |                    8 |
| Dirección General    |                    4 |
| Backend              |                    7 |
| Data Center          |                    3 |
| **Total**            |               **48** |

Para estos enlaces se utilizará **cable UTP categoría 6**, debido a que las distancias internas del edificio se encuentran dentro del rango adecuado para este medio y permite disponer de una solución de cobre apropiada para conexiones Ethernet dentro de las áreas de trabajo.

El cableado horizontal deberá terminar bajo el mismo estándar en ambos extremos, tanto en la toma de red como en el sistema de terminación correspondiente.

---

### 6.2 Cableado Troncal o Backbone

El cableado troncal corresponde a los enlaces que conectan el **switch principal ubicado en el MDF con cada uno de los ocho switches de área**.

La estructura será:

```text
                        MDF
                         │
                  Switch principal
                         │
                   Cable troncal
                         │
                Switch departamental
```

Se contemplan los siguientes ocho enlaces:

1. MDF - Recepción.
2. MDF - Recursos Humanos.
3. MDF - Legal.
4. MDF - Sala de Capacitación.
5. MDF - Diseño e Innovación.
6. MDF - Dirección General.
7. MDF - Backend.
8. MDF - Data Center.

Por lo tanto, la infraestructura dispone de **8 enlaces troncales**.

Para estos enlaces se propone utilizar **fibra óptica multimodo**, debido a su capacidad de transmisión, escalabilidad y conveniencia para interconectar equipos de telecomunicaciones dentro de un mismo edificio.

---

### 6.3 Diferenciación entre Cableado Horizontal y Troncal

La diferencia principal entre ambos segmentos se encuentra en los dispositivos que interconectan y en la función que cumplen dentro de la infraestructura.

| Característica          | Cableado Horizontal                                | Cableado Troncal                              |
| ----------------------- | -------------------------------------------------- | --------------------------------------------- |
| Origen                  | Switch departamental                               | MDF / switch principal                        |
| Destino                 | Dispositivo final                                  | Switch departamental                          |
| Dispositivos conectados | PC, laptop o servidor                              | Switch principal y switch de área             |
| Medio propuesto         | UTP Cat 6                                          | Fibra óptica multimodo                        |
| Cantidad de enlaces     | 48                                                 | 8                                             |
| Función                 | Conectar usuarios y servidores dentro de cada área | Interconectar las diferentes áreas con el MDF |

Ejemplo del flujo:

```text
MDF
 │
 │ Fibra óptica multimodo
 │ Cableado troncal
 ▼
Switch Recursos Humanos
 │
 │ UTP Cat 6
 │ Cableado horizontal
 ▼
PC Recursos Humanos
```

Esta diferenciación se mantendrá también en el diagrama físico utilizando diferentes estilos de línea para facilitar su identificación.

---

## 7. Medios de Transmisión

La selección de los medios de transmisión se realizó considerando la función de cada segmento, las distancias existentes dentro del edificio, la capacidad requerida, el costo y la posibilidad de crecimiento futuro.

Se utilizarán dos medios principales:

* **UTP categoría 6** para el cableado horizontal.
* **Fibra óptica multimodo** para el cableado troncal.

---

### 7.1 Medio Utilizado en el Cableado Horizontal

Para el cableado horizontal se propone utilizar **cable de par trenzado UTP categoría 6**.

Este medio será utilizado para conectar:

```text
Switch departamental → PC
Switch departamental → Laptop
Switch departamental → Servidor
```

La elección de UTP Cat 6 se fundamenta principalmente en:

* Las distancias relativamente cortas existentes dentro de cada departamento.
* Su utilización común para conexiones Ethernet dentro de áreas de trabajo.
* Un costo de implementación menor respecto a una instalación de fibra hacia cada dispositivo final.
* Facilidad de instalación, terminación y mantenimiento.
* Capacidad suficiente para las necesidades de conectividad planteadas en el diseño.

Cada uno de los 48 dispositivos finales dispondrá de su propio enlace UTP hacia el switch correspondiente.

---

### 7.2 Medio Utilizado en el Cableado Troncal

Para los enlaces troncales se propone utilizar **fibra óptica multimodo**.

La fibra conectará el switch principal ubicado en el MDF con cada uno de los switches de área.

La elección se fundamenta en los siguientes criterios:

#### Capacidad

La fibra óptica proporciona una capacidad de transmisión elevada, característica conveniente para enlaces que concentran el tráfico proveniente de varios dispositivos.

#### Escalabilidad

Su utilización proporciona margen para futuras necesidades de mayor ancho de banda sin tener que reemplazar inmediatamente el medio físico troncal.

#### Interferencias electromagnéticas

Al transmitir la información mediante señales ópticas y no mediante señales eléctricas sobre conductores de cobre, la fibra presenta una alta inmunidad frente a interferencias electromagnéticas.

#### Distancia

Las dimensiones del edificio no representan una limitación para la utilización de fibra multimodo. Incluso el recorrido estimado hacia el Data Center, considerado uno de los enlaces troncales más largos, es de aproximadamente **22 metros**, por lo que se mantiene dentro de un rango adecuado para la solución de fibra óptica multimodo propuesta.

#### Costo

La instalación de fibra puede representar un costo superior respecto al cableado de cobre. Sin embargo, para QuetzalDev S.A. se limita su utilización a únicamente **ocho enlaces troncales**, mientras que los 48 enlaces hacia los dispositivos finales continuarán utilizando UTP Cat 6.

De esta manera se busca obtener un equilibrio entre costo, capacidad y escalabilidad.

---

### 7.3 Tabla de Medios por Segmento

| Segmento   | Origen                     | Destino                             | Medio seleccionado | Tipo / Categoría | Justificación principal                                         |
| ---------- | -------------------------- | ----------------------------------- | ------------------ | ---------------- | --------------------------------------------------------------- |
| Horizontal | Switch Recepción           | Dispositivos de Recepción           | Cobre              | UTP Cat 6        | Distancia corta, facilidad de instalación y costo               |
| Horizontal | Switch Recursos Humanos    | Dispositivos de RRHH                | Cobre              | UTP Cat 6        | Distancia corta, facilidad de instalación y costo               |
| Horizontal | Switch Legal               | Dispositivos de Legal               | Cobre              | UTP Cat 6        | Distancia corta, facilidad de instalación y costo               |
| Horizontal | Switch Capacitación        | Dispositivos de Capacitación        | Cobre              | UTP Cat 6        | Distancia corta, facilidad de instalación y costo               |
| Horizontal | Switch Diseño e Innovación | Dispositivos de Diseño e Innovación | Cobre              | UTP Cat 6        | Distancia corta, facilidad de instalación y costo               |
| Horizontal | Switch Dirección General   | Dispositivos de Dirección General   | Cobre              | UTP Cat 6        | Distancia corta, facilidad de instalación y costo               |
| Horizontal | Switch Backend             | Dispositivos de Backend             | Cobre              | UTP Cat 6        | Distancia corta, facilidad de instalación y costo               |
| Horizontal | Switch Data Center         | Servidores principales              | Cobre              | UTP Cat 6        | Distancias internas reducidas                                   |
| Troncal    | MDF                        | Switch Recepción                    | Fibra óptica       | Multimodo        | Capacidad y escalabilidad                                       |
| Troncal    | MDF                        | Switch Recursos Humanos             | Fibra óptica       | Multimodo        | Capacidad y escalabilidad                                       |
| Troncal    | MDF                        | Switch Legal                        | Fibra óptica       | Multimodo        | Capacidad y escalabilidad                                       |
| Troncal    | MDF                        | Switch Capacitación                 | Fibra óptica       | Multimodo        | Capacidad y escalabilidad                                       |
| Troncal    | MDF                        | Switch Diseño e Innovación          | Fibra óptica       | Multimodo        | Capacidad y escalabilidad                                       |
| Troncal    | MDF                        | Switch Dirección General            | Fibra óptica       | Multimodo        | Capacidad y escalabilidad                                       |
| Troncal    | MDF                        | Switch Backend                      | Fibra óptica       | Multimodo        | Capacidad y escalabilidad                                       |
| Troncal    | MDF                        | Switch Data Center                  | Fibra óptica       | Multimodo        | Capacidad, escalabilidad y conexión hacia el área de servidores |

### 7.4 Resumen de Medios de Transmisión

La solución propuesta combina cobre y fibra óptica de acuerdo con la función de cada segmento:

```text
                    MDF
                     │
            Fibra óptica multimodo
                     │
             Switch departamental
                     │
                  UTP Cat 6
                     │
             Dispositivo final
```

Esta combinación permite utilizar un medio de mayor capacidad para la infraestructura troncal y un medio de cobre más económico para las conexiones hacia los dispositivos finales.

---

## 8. Estimación de Distancias de Cableado

Las distancias fueron estimadas utilizando como referencia las dimensiones proporcionadas en el plano arquitectónico de QuetzalDev S.A.

Para realizar las estimaciones se consideró que los cables seguirán recorridos mediante paredes, pasillos y canalizaciones, evitando utilizar distancias diagonales directas entre los dispositivos.

El diseño diferencia las siguientes distancias:

* **Distancia horizontal:** recorrido desde el punto de red hasta el switch del departamento.
* **Distancia troncal:** recorrido desde el switch departamental hasta el MDF.
* **Distancia de referencia hacia el MDF:** suma del recorrido horizontal y troncal correspondiente al área.

La última distancia se utiliza únicamente como referencia del recorrido completo del dispositivo hacia la infraestructura central; físicamente el cableado horizontal y troncal corresponden a segmentos independientes.

---

### 8.1 Distancias del Cableado Troncal

El cableado troncal conecta el switch principal ubicado en el MDF con cada uno de los ocho switches de área.

| Enlace troncal             | Distancia aproximada |
| -------------------------- | -------------------: |
| MDF - Recepción            |                  4 m |
| MDF - Recursos Humanos     |                 12 m |
| MDF - Legal                |                 11 m |
| MDF - Sala de Capacitación |                  7 m |
| MDF - Diseño e Innovación  |                  6 m |
| MDF - Dirección General    |                 11 m |
| MDF - Backend              |                 12 m |
| MDF - Data Center          |                 22 m |
| **Total estimado**         |             **85 m** |

Para contemplar curvas, terminaciones y holgura de instalación se agrega aproximadamente un **15 % de reserva**:

```text
85 m × 1.15 = 97.75 m
```

Por lo tanto, se considera aproximadamente:

**100 metros de fibra óptica multimodo para el cableado troncal.**

---

### 8.2 Distancias del Cableado Horizontal

El cableado horizontal corresponde a los enlaces UTP Cat 6 entre los switches departamentales y cada uno de los 48 puntos de red.

#### Departamento de Recepción

| Punto                | Distancia horizontal | Troncal hacia MDF | Recorrido de referencia hacia MDF |
| -------------------- | -------------------: | ----------------: | --------------------------------: |
| Recepcion-PR01       |                  7 m |               4 m |                              11 m |
| Recepcion-PR02       |                  8 m |               4 m |                              12 m |
| Recepcion-PR03       |                 10 m |               4 m |                              14 m |
| Recepcion-PR04       |                 11 m |               4 m |                              15 m |
| **Total horizontal** |             **36 m** |                   |                                   |

---

#### Departamento de Recursos Humanos

| Punto                | Distancia horizontal | Troncal hacia MDF | Recorrido de referencia hacia MDF |
| -------------------- | -------------------: | ----------------: | --------------------------------: |
| RecursosHumanos-PR01 |                  5 m |              12 m |                              17 m |
| RecursosHumanos-PR02 |                  6 m |              12 m |                              18 m |
| RecursosHumanos-PR03 |                  6 m |              12 m |                              18 m |
| RecursosHumanos-PR04 |                  7 m |              12 m |                              19 m |
| RecursosHumanos-PR05 |                  7 m |              12 m |                              19 m |
| RecursosHumanos-PR06 |                  7 m |              12 m |                              19 m |
| RecursosHumanos-PR07 |                  8 m |              12 m |                              20 m |
| RecursosHumanos-PR08 |                  8 m |              12 m |                              20 m |
| **Total horizontal** |             **54 m** |                   |                                   |

---

#### Departamento Legal

| Punto                | Distancia horizontal | Troncal hacia MDF | Recorrido de referencia hacia MDF |
| -------------------- | -------------------: | ----------------: | --------------------------------: |
| Legal-PR01           |                  4 m |              11 m |                              15 m |
| Legal-PR02           |                  5 m |              11 m |                              16 m |
| Legal-PR03           |                  6 m |              11 m |                              17 m |
| Legal-PR04           |                  7 m |              11 m |                              18 m |
| **Total horizontal** |             **22 m** |                   |                                   |

---

#### Sala de Capacitación

| Punto                | Distancia horizontal | Troncal hacia MDF | Recorrido de referencia hacia MDF |
| -------------------- | -------------------: | ----------------: | --------------------------------: |
| Capacitacion-PR01    |                  5 m |               7 m |                              12 m |
| Capacitacion-PR02    |                  5 m |               7 m |                              12 m |
| Capacitacion-PR03    |                  6 m |               7 m |                              13 m |
| Capacitacion-PR04    |                  6 m |               7 m |                              13 m |
| Capacitacion-PR05    |                  7 m |               7 m |                              14 m |
| Capacitacion-PR06    |                  7 m |               7 m |                              14 m |
| Capacitacion-PR07    |                  8 m |               7 m |                              15 m |
| Capacitacion-PR08    |                  8 m |               7 m |                              15 m |
| Capacitacion-PR09    |                  9 m |               7 m |                              16 m |
| Capacitacion-PR10    |                  9 m |               7 m |                              16 m |
| **Total horizontal** |             **70 m** |                   |                                   |

---

#### Departamento de Diseño e Innovación

| Punto                 | Distancia horizontal | Troncal hacia MDF | Recorrido de referencia hacia MDF |
| --------------------- | -------------------: | ----------------: | --------------------------------: |
| DisenoInnovacion-PR01 |                  5 m |               6 m |                              11 m |
| DisenoInnovacion-PR02 |                  5 m |               6 m |                              11 m |
| DisenoInnovacion-PR03 |                  6 m |               6 m |                              12 m |
| DisenoInnovacion-PR04 |                  6 m |               6 m |                              12 m |
| DisenoInnovacion-PR05 |                  7 m |               6 m |                              13 m |
| DisenoInnovacion-PR06 |                  7 m |               6 m |                              13 m |
| DisenoInnovacion-PR07 |                  7 m |               6 m |                              13 m |
| DisenoInnovacion-PR08 |                  8 m |               6 m |                              14 m |
| **Total horizontal**  |             **51 m** |                   |                                   |

---

#### Dirección General

| Punto                 | Distancia horizontal | Troncal hacia MDF | Recorrido de referencia hacia MDF |
| --------------------- | -------------------: | ----------------: | --------------------------------: |
| DireccionGeneral-PR01 |                  4 m |              11 m |                              15 m |
| DireccionGeneral-PR02 |                  5 m |              11 m |                              16 m |
| DireccionGeneral-PR03 |                  6 m |              11 m |                              17 m |
| DireccionGeneral-PR04 |                  7 m |              11 m |                              18 m |
| **Total horizontal**  |             **22 m** |                   |                                   |

---

#### Departamento de Backend

| Punto                | Distancia horizontal | Troncal hacia MDF | Recorrido de referencia hacia MDF |
| -------------------- | -------------------: | ----------------: | --------------------------------: |
| Backend-PR01         |                  5 m |              12 m |                              17 m |
| Backend-PR02         |                  6 m |              12 m |                              18 m |
| Backend-PR03         |                  6 m |              12 m |                              18 m |
| Backend-PR04         |                  7 m |              12 m |                              19 m |
| Backend-PR05         |                  7 m |              12 m |                              19 m |
| Backend-PR06         |                  7 m |              12 m |                              19 m |
| Backend-PR07         |                  8 m |              12 m |                              20 m |
| **Total horizontal** |             **46 m** |                   |                                   |

---

#### Data Center

| Punto                | Distancia horizontal | Troncal hacia MDF | Recorrido de referencia hacia MDF |
| -------------------- | -------------------: | ----------------: | --------------------------------: |
| DataCenter-PR01      |                  4 m |              22 m |                              26 m |
| DataCenter-PR02      |                  4 m |              22 m |                              26 m |
| DataCenter-PR03      |                  4 m |              22 m |                              26 m |
| **Total horizontal** |             **12 m** |                   |                                   |

---

### 8.3 Resumen del Cableado Horizontal

| Departamento         | Cantidad de enlaces | Cable horizontal estimado |
| -------------------- | ------------------: | ------------------------: |
| Recepción            |                   4 |                      36 m |
| Recursos Humanos     |                   8 |                      54 m |
| Legal                |                   4 |                      22 m |
| Sala de Capacitación |                  10 |                      70 m |
| Diseño e Innovación  |                   8 |                      51 m |
| Dirección General    |                   4 |                      22 m |
| Backend              |                   7 |                      46 m |
| Data Center          |                   3 |                      12 m |
| **Total**            |              **48** |                 **313 m** |

El diseño requiere aproximadamente:

```text
313 m de UTP Cat 6
```

A este valor se agrega un **10 % de reserva** para considerar terminaciones, curvas, rutas de canalización y posibles ajustes durante la instalación.

```text
313 m × 0.10 = 31.3 m

313 m + 31.3 m = 344.3 m
```

Por lo tanto:

**Cable UTP Cat 6 requerido ≈ 345 m**

---

### 8.4 Cálculo de Bobinas de Cable UTP

Las bobinas estándar consideradas para la práctica son de:

```text
305 m
```

Se calcula:

```text
344.3 m ÷ 305 m = 1.13 bobinas
```

Debido a que no es posible adquirir una fracción de bobina, el resultado se redondea hacia arriba.

```text
Cantidad requerida = 2 bobinas
```

Por lo tanto, se propone adquirir:

**2 bobinas de cable UTP Cat 6 de 305 metros cada una.**

La cantidad total disponible sería:

```text
2 × 305 m = 610 m
```

Después de utilizar aproximadamente 344.3 m, quedaría un margen de cable disponible para mantenimiento, reposición o futuras ampliaciones.

---

### 8.5 Resumen General de Cable Requerido

| Medio                  | Cantidad estimada | Reserva incluida | Adquisición propuesta |
| ---------------------- | ----------------: | ---------------: | --------------------- |
| UTP Cat 6              |             313 m |        ≈ 344.3 m | 2 bobinas de 305 m    |
| Fibra óptica multimodo |              85 m |        ≈ 97.75 m | Aproximadamente 100 m |

Las cantidades calculadas corresponden a estimaciones basadas en las dimensiones arquitectónicas proporcionadas y deberán verificarse mediante mediciones físicas antes de una implementación real.

Las rutas representadas en el diagrama físico final corresponden a los recorridos considerados para estas estimaciones. Debido a que el diseño se realiza a partir de un plano arquitectónico y una representación en Cisco Packet Tracer, las distancias indicadas son aproximadas y deberán validarse mediante mediciones físicas antes de realizar una instalación real.

---

## 9. Inventario de Equipos

La infraestructura de QuetzalDev S.A. contará con equipos de distribución y elementos de terminación destinados a organizar tanto el cableado horizontal como el cableado troncal.

En esta sección se dimensionan los switches, patch panels y demás elementos de distribución requeridos para la infraestructura. Los requerimientos técnicos definidos sirven como base para los modelos y referencias comerciales considerados en el presupuesto.

---

### 9.1 Switches

La red contará con:

* **8 switches departamentales**, uno para cada área.
* **1 switch principal**, ubicado en el MDF.

Los switches departamentales conectarán las computadoras, laptops y servidores mediante cableado UTP Cat 6.

Debido a que el backbone será implementado con fibra óptica multimodo, cada switch departamental deberá disponer además de al menos **una interfaz SFP o SFP+** para establecer el enlace troncal hacia el MDF.

#### Dimensionamiento de Switches Departamentales

| Área / Departamento  | Dispositivos actuales | Switch propuesto | Puertos RJ45 libres | Uplink óptico |
| -------------------- | --------------------: | ---------------: | ------------------: | ------------- |
| Recepción            |                     4 |        8 puertos |                   4 | 1 SFP/SFP+    |
| Recursos Humanos     |                     8 |       16 puertos |                   8 | 1 SFP/SFP+    |
| Legal                |                     4 |        8 puertos |                   4 | 1 SFP/SFP+    |
| Sala de Capacitación |                    10 |       16 puertos |                   6 | 1 SFP/SFP+    |
| Diseño e Innovación  |                     8 |       16 puertos |                   8 | 1 SFP/SFP+    |
| Dirección General    |                     4 |        8 puertos |                   4 | 1 SFP/SFP+    |
| Backend              |                     7 |       16 puertos |                   9 | 1 SFP/SFP+    |
| Data Center          |                     3 |        8 puertos |                   5 | 1 SFP/SFP+    |

La selección deja puertos disponibles en todas las áreas para permitir la incorporación de nuevos dispositivos sin reemplazar inmediatamente el switch.

En total se requieren inicialmente:

* **4 switches de 8 puertos RJ45**

  * Recepción.
  * Legal.
  * Dirección General.
  * Data Center.

Las rutas representadas en el diagrama físico final corresponden a los recorridos considerados para estas estimaciones. Debido a que el diseño se realiza a partir de un plano arquitectónico y una representación en Cisco Packet Tracer, las distancias indicadas son aproximadas y deberán validarse mediante mediciones físicas antes de realizar una instalación real.

* **4 switches de 16 puertos RJ45**

  * Recursos Humanos.
  * Sala de Capacitación.
  * Diseño e Innovación.
  * Backend.

Se recomienda que los equipos cuenten con **dos interfaces SFP/SFP+ cuando sea posible**, utilizando una para el enlace troncal actual y dejando la segunda disponible para crecimiento o futuras necesidades de redundancia.

#### Switch Principal del MDF

El switch principal será el punto central de distribución del backbone y recibirá los enlaces provenientes de los ocho switches departamentales.

| Característica             | Requerimiento                              |
| -------------------------- | ------------------------------------------ |
| Ubicación                  | MDF                                        |
| Función                    | Agregación de los switches departamentales |
| Enlaces troncales actuales | 8                                          |
| Interfaces ópticas mínimas | 8 SFP/SFP+                                 |
| Capacidad recomendada      | Superior a 8 interfaces ópticas            |
| Tipo                       | Administrable                              |
| Instalación                | Montaje en rack                            |
| Medio utilizado            | Fibra óptica multimodo                     |

El requerimiento mínimo es de ocho interfaces ópticas, una por cada área. Sin embargo, se recomienda seleccionar un equipo con capacidad superior para permitir futuras ampliaciones.

La cantidad exacta de interfaces será definida cuando se seleccione el modelo comercial correspondiente.

#### Características Generales Recomendadas

Los switches deberán considerar como mínimo:

* Puertos Gigabit Ethernet RJ45.
* Interfaces SFP o SFP+ compatibles con fibra multimodo.
* Capacidad administrable.
* Indicadores de estado de puertos y enlaces.
* Capacidad suficiente para la cantidad de dispositivos conectados.
* Puertos disponibles para crecimiento futuro.
* Compatibilidad con la infraestructura de rack o gabinete correspondiente.

Aunque la práctica se concentra en el diseño físico de Capa 1 y no contempla la configuración de los dispositivos, utilizar switches administrables permitirá aprovechar posteriormente funciones de red sin reemplazar el hardware.

---

### 9.2 Patch Panels

Los patch panels se utilizarán para **terminar y organizar el cableado horizontal UTP Cat 6** proveniente de las tomas de red.

El recorrido físico de una conexión será:

**Dispositivo → toma de red → cableado horizontal → patch panel → patch cord → switch departamental**

De esta forma, el cableado permanente no se conecta directamente al switch, facilitando la identificación de puertos, el mantenimiento y futuras modificaciones.

#### Dimensionamiento de Patch Panels

Cada patch panel tendrá una capacidad igual o superior a la cantidad de puntos de red existentes en el departamento.

| Área / Departamento  | Puntos de red | Patch panel propuesto | Puertos libres | Capacidad del switch |
| -------------------- | ------------: | --------------------: | -------------: | -------------------: |
| Recepción            |             4 |             8 puertos |              4 |            8 puertos |
| Recursos Humanos     |             8 |            12 puertos |              4 |           16 puertos |
| Legal                |             4 |             8 puertos |              4 |            8 puertos |
| Sala de Capacitación |            10 |            12 puertos |              2 |           16 puertos |
| Diseño e Innovación  |             8 |            12 puertos |              4 |           16 puertos |
| Dirección General    |             4 |             8 puertos |              4 |            8 puertos |
| Backend              |             7 |            12 puertos |              5 |           16 puertos |
| Data Center          |             3 |             8 puertos |              5 |            8 puertos |

En todos los casos se cumple que la capacidad del switch es **igual o superior a la capacidad del patch panel correspondiente**.

#### Resumen de Capacidad

| Concepto                             |   Cantidad |
| ------------------------------------ | ---------: |
| Puntos de red utilizados actualmente |         48 |
| Capacidad total de patch panels      | 80 puertos |
| Puertos disponibles para crecimiento |         32 |

La capacidad instalada permite cubrir los 48 puntos actuales y mantener espacio adicional para futuras conexiones.

#### Cantidad de Patch Panels

La propuesta requiere:

* **4 patch panels de 8 puertos**

  * Recepción.
  * Legal.
  * Dirección General.
  * Data Center.

* **4 patch panels de 12 puertos**

  * Recursos Humanos.
  * Sala de Capacitación.
  * Diseño e Innovación.
  * Backend.

En total se utilizarán **8 patch panels**, uno por cada área.

Los patch panels deberán ser compatibles con **UTP Cat 6** y conservar el esquema de identificación establecido para cada punto de red.

Por ejemplo, el punto de red:

`Recepcion-PR01`

se encuentra asociado físicamente a la toma:

`REC-T01`

y deberá poder relacionarse durante todo su recorrido mediante:

**Toma `REC-T01` / Punto `Recepcion-PR01` → cableado horizontal → puerto correspondiente del patch panel → switch de Recepción**

Esto facilitará la localización y administración de cada enlace durante las tareas de mantenimiento.

### 9.3 ODF - Optical Distribution Frame

Debido a que el cableado troncal de QuetzalDev S.A. se realizará mediante **fibra óptica multimodo**, se propone instalar un **ODF (Optical Distribution Frame)** dentro del MDF.

El ODF tendrá como función principal organizar, proteger e identificar las terminaciones de fibra correspondientes a los enlaces entre el MDF y los switches departamentales.

#### Enlaces Ópticos

La infraestructura contempla ocho enlaces troncales:

| No. | Enlace |
|---:|---|
| 1 | MDF - Recepción |
| 2 | MDF - Recursos Humanos |
| 3 | MDF - Legal |
| 4 | MDF - Sala de Capacitación |
| 5 | MDF - Diseño e Innovación |
| 6 | MDF - Dirección General |
| 7 | MDF - Backend |
| 8 | MDF - Data Center |

En la propuesta se utilizarán enlaces de fibra **dúplex**, utilizando una fibra para transmisión y otra para recepción.

Por lo tanto:

- **8 enlaces troncales**
- **2 fibras por enlace**
- **16 fibras utilizadas**

#### Dimensionamiento del ODF

Para los 16 hilos de fibra requeridos se propone utilizar un **ODF con capacidad de 24 fibras**, dejando capacidad adicional para futuras ampliaciones.

| Característica | Propuesta |
|---|---|
| Ubicación | MDF |
| Medio | Fibra óptica multimodo |
| Enlaces actuales | 8 |
| Fibras utilizadas | 16 |
| Capacidad propuesta | 24 fibras |
| Capacidad libre | 8 fibras |
| Instalación | Montaje en rack |
| Función | Organización, terminación y protección del backbone |

La capacidad adicional permite incorporar nuevos enlaces ópticos sin necesidad de sustituir inmediatamente el ODF.

#### Terminación de Fibra en los Departamentos

En el extremo correspondiente a cada departamento se utilizará una terminación óptica protegida antes de conectar la fibra al switch departamental.

El flujo físico del backbone será:

**Switch principal → ODF → fibra multimodo → terminación óptica del departamento → switch departamental**

Esto permite mantener protegidas y organizadas las terminaciones de fibra tanto en el MDF como en cada área.

#### Identificación de los Enlaces

Cada enlace óptico conservará el esquema de etiquetado definido para el cableado troncal:

| Enlace | Etiqueta |
|---|---|
| MDF - Recepción | `MDF-Recepcion` |
| MDF - Recursos Humanos | `MDF-RecursosHumanos` |
| MDF - Legal | `MDF-Legal` |
| MDF - Sala de Capacitación | `MDF-Capacitacion` |
| MDF - Diseño e Innovación | `MDF-DisenoInnovacion` |
| MDF - Dirección General | `MDF-DireccionGeneral` |
| MDF - Backend | `MDF-Backend` |
| MDF - Data Center | `MDF-DataCenter` |

La selección definitiva del ODF, los conectores y los accesorios ópticos deberá verificar su compatibilidad con la fibra multimodo, los módulos ópticos y los equipos de red utilizados en la implementación.

### 9.4 Tomas, Conectores y Accesorios

Además de los switches, patch panels y elementos de distribución óptica, la instalación requiere componentes para la terminación y conexión de los 48 puntos de red.

Las cantidades se determinaron a partir de la distribución de tomas definida anteriormente.

#### Tomas de Red

La infraestructura contempla **25 ubicaciones físicas de tomas**, las cuales proporcionan un total de **48 puertos de red**.

| Tipo de toma | Cantidad | Puertos proporcionados |
|---|---:|---:|
| Unitaria | 4 | 4 |
| Doble | 19 | 38 |
| Triple | 2 | 6 |
| **Total** | **25 tomas** | **48 puertos** |

Cada puerto será identificado individualmente mediante el esquema de etiquetado correspondiente al área y número de punto de red.

---

#### Keystone Jacks

Cada punto de red UTP requiere un conector hembra RJ45 para realizar la terminación en la toma correspondiente.

Por lo tanto, se requieren:

| Elemento | Cantidad |
|---|---:|
| Keystone Jack RJ45 Cat 6 | 48 |

Los keystone jacks deberán ser compatibles con cable UTP Cat 6 y con el estándar de terminación seleccionado para la instalación.

---

#### Placas y Cajas para Tomas

Se instalarán placas o cajas compatibles con la cantidad de puertos de cada punto físico.

| Tipo de placa / caja | Cantidad |
|---|---:|
| 1 puerto | 4 |
| 2 puertos | 19 |
| 3 puertos | 2 |
| **Total** | **25** |

Estas placas deberán permitir la instalación de los keystone jacks y mantener protegidas las terminaciones del cableado horizontal.

---

#### Patch Cords UTP Cat 6

Cada dispositivo requiere un patch cord para conectarse desde el equipo final hasta la toma de red.

Adicionalmente, en el extremo del switch se utilizará otro patch cord para conectar el puerto correspondiente del patch panel con el switch departamental.

Por lo tanto:

| Uso | Cantidad |
|---|---:|
| Dispositivo final → toma de red | 48 |
| Patch panel → switch | 48 |
| **Total de patch cords UTP Cat 6** | **96** |

Se recomienda utilizar patch cords prefabricados y certificados para Cat 6.

---

#### Accesorios para Fibra Óptica

Los ocho enlaces troncales requerirán elementos adicionales para la correcta terminación y protección de la fibra multimodo.

| Elemento | Cantidad inicial |
|---|---:|
| Terminaciones o cajas ópticas departamentales | 8 |
| Enlaces ópticos dúplex | 8 |
| ODF central | 1 |
| Patch cords ópticos para MDF | 8 |
| Patch cords ópticos para switches departamentales | 8 |

En total se contemplan **16 patch cords ópticos**, correspondientes a dos por cada enlace troncal:

- uno en el extremo del MDF;
- uno en el extremo del switch departamental.

El tipo definitivo de conector óptico deberá ser compatible con los módulos SFP/SFP+, los patch cords ópticos, las terminaciones departamentales y el ODF utilizados.

---

#### Resumen de Elementos de Terminación

| Elemento | Cantidad |
|---|---:|
| Tomas físicas | 25 |
| Puertos de red | 48 |
| Keystone Jack RJ45 Cat 6 | 48 |
| Patch cords UTP Cat 6 | 96 |
| Patch cords ópticos | 16 |
| Cajas de terminación óptica departamentales | 8 |
| ODF | 1 |

Las cantidades anteriores corresponden a la infraestructura actual. En una implementación real se recomienda considerar unidades adicionales de reserva para mantenimiento, sustitución de componentes y futuras ampliaciones.

### 9.5 Compatibilidad del Backbone Óptico

La implementación del backbone requiere que los switches, módulos ópticos, fibra y elementos de terminación sean compatibles entre sí.

La infraestructura contempla:

- 8 switches departamentales con al menos una interfaz óptica.
- 1 switch principal con al menos 8 interfaces ópticas.
- 16 módulos ópticos en total, uno por cada extremo de los 8 enlaces troncales.
- 8 enlaces de fibra óptica multimodo dúplex.
- 1 ODF con capacidad para 24 fibras.
- 8 terminaciones ópticas departamentales.
- 16 patch cords ópticos.

Antes de adquirir los equipos deberán verificarse como mínimo los siguientes aspectos:

- Compatibilidad entre los puertos SFP/SFP+ de los switches y los módulos ópticos.
- Velocidad soportada por los módulos y los switches.
- Tipo de fibra multimodo utilizado.
- Longitud de onda de los transceptores.
- Tipo de conector utilizado por los módulos, ODF y terminaciones ópticas.
- Distancia máxima soportada por la combinación de fibra y transceptores.

Todos los enlaces del backbone deberán utilizar componentes compatibles y mantener el mismo criterio tecnológico en ambos extremos.

La selección definitiva entre SFP o SFP+ dependerá de los modelos comerciales adquiridos. Por esta razón, el presente diseño define el requerimiento de interfaces ópticas sin limitar la solución a un modelo específico.

El ODF de 24 fibras dispone de capacidad suficiente para los 16 hilos actualmente requeridos y mantiene 8 fibras disponibles, equivalentes a capacidad para hasta 4 enlaces dúplex adicionales.

> **Nota:** Los modelos de switches representados en Cisco Packet Tracer se utilizan como referencia gráfica del diseño físico. La implementación real deberá utilizar equipos que cumplan con la cantidad de puertos RJ45 e interfaces ópticas establecidas en este Manual Técnico.


---

## 10. Verificación de Capacidad de Patch Panels y Switches

El dimensionamiento de los elementos de distribución se realizó considerando los **48 puntos de red actuales** de QuetzalDev S.A. y dejando capacidad adicional para futuras ampliaciones.

Para cada departamento se verificó que:

- El patch panel disponga de una cantidad de puertos igual o superior a los puntos de red actuales.
- El switch departamental disponga de una cantidad de puertos RJ45 igual o superior a la capacidad del patch panel.
- El switch disponga adicionalmente de una interfaz SFP/SFP+ para el enlace troncal de fibra óptica.

### 10.1 Verificación por Departamento

| Área / Departamento | Puntos actuales | Patch Panel | Switch RJ45 | Puertos libres en Patch Panel | Puertos libres en Switch |
|---|---:|---:|---:|---:|---:|
| Recepción | 4 | 8 | 8 | 4 | 4 |
| Recursos Humanos | 8 | 12 | 16 | 4 | 8 |
| Legal | 4 | 8 | 8 | 4 | 4 |
| Sala de Capacitación | 10 | 12 | 16 | 2 | 6 |
| Diseño e Innovación | 8 | 12 | 16 | 4 | 8 |
| Dirección General | 4 | 8 | 8 | 4 | 4 |
| Backend | 7 | 12 | 16 | 5 | 9 |
| Data Center | 3 | 8 | 8 | 5 | 5 |
| **Total** | **48** | **80** | **96** | **32** | **48** |

La infraestructura cumple con el criterio de que la capacidad del switch sea igual o superior a la capacidad del patch panel correspondiente.

### 10.2 Capacidad Instalada

Actualmente se requieren:

- **48 puntos de red activos**.
- **80 puertos de patch panel instalados**.
- **96 puertos RJ45 disponibles en los switches departamentales**.

Por lo tanto, se dispone inicialmente de:

- **32 puertos libres en patch panels**.
- **48 puertos RJ45 libres en switches**.

Esta capacidad adicional permite incorporar nuevos dispositivos sin realizar inmediatamente un reemplazo de los elementos principales de distribución.

### 10.3 Verificación del Switch Principal

El switch principal del MDF deberá concentrar los ocho enlaces troncales provenientes de los switches departamentales.

| Concepto | Cantidad |
|---|---:|
| Switches departamentales | 8 |
| Enlaces troncales actuales | 8 |
| Interfaces ópticas mínimas requeridas | 8 |
| Capacidad recomendada | Superior a 8 interfaces ópticas |

El equipo seleccionado deberá disponer como mínimo de **8 interfaces SFP/SFP+**.

Para permitir crecimiento futuro, el equipo comercial considerado deberá disponer de una cantidad superior a las ocho interfaces ópticas actualmente requeridas.

### 10.4 Resultado del Dimensionamiento

La capacidad propuesta satisface las necesidades actuales de QuetzalDev S.A. y mantiene un margen disponible para futuras ampliaciones.

La relación general queda definida de la siguiente manera:

| Elemento | Necesidad actual | Capacidad instalada/propuesta |
|---|---:|---:|
| Puntos de red | 48 | 48 activos |
| Patch Panels | 48 puertos necesarios | 80 puertos |
| Switches departamentales | 48 puertos utilizados | 96 puertos RJ45 |
| Backbone | 8 enlaces | 8 interfaces ópticas mínimas + crecimiento |

De esta forma, el diseño evita utilizar equipos sin capacidad de expansión y permite aumentar posteriormente el número de estaciones de trabajo, servidores o dispositivos de red.

---

## 11. Canalización del Cableado

La canalización tiene como objetivo proteger, ordenar y guiar el recorrido del cableado estructurado dentro del edificio.

Debido a que QuetzalDev S.A. utilizará dos medios de transmisión diferentes, se propone una canalización distinta para el cableado horizontal y para el cableado troncal.

La selección se realiza considerando:

- Tipo de cable.
- Cantidad de enlaces.
- Protección física.
- Facilidad de mantenimiento.
- Orden de la instalación.
- Posibilidad de futuras ampliaciones.

---

### 11.1 Canalización del Cableado Horizontal

Para el cableado horizontal UTP Cat 6 se propone utilizar **canaleta cerrada de PVC** instalada principalmente sobre paredes y zonas perimetrales de cada departamento.

La canaleta permitirá transportar los cables desde el patch panel y switch departamental hasta las diferentes tomas de red.

#### Justificación

La canaleta cerrada de PVC se selecciona debido a que:

- Protege físicamente los cables UTP.
- Mantiene una apariencia ordenada dentro de las oficinas.
- Permite realizar derivaciones hacia las diferentes tomas de red.
- Facilita el acceso al cableado durante tareas de mantenimiento.
- Su instalación resulta adecuada para recorridos cortos dentro de cada departamento.
- Permite agregar nuevos cables si existe capacidad disponible.

La ruta del cableado horizontal deberá seguir principalmente paredes y perímetros, evitando atravesar espacios abiertos o zonas de circulación sin protección.

La estructura general será:

**Switch departamental → Patch panel → Canaleta PVC → Toma de red → Dispositivo final**

---

### 11.2 Canalización del Cableado Troncal

Para los ocho enlaces de fibra óptica multimodo se propone utilizar una **bandeja metálica cerrada** como ruta principal de distribución.

Esta canalización partirá desde el MDF y recorrerá principalmente la zona del Hall Central y los corredores del edificio, desde donde se realizarán derivaciones hacia cada departamento.

#### Justificación

La bandeja metálica cerrada proporciona:

- Protección mecánica para la fibra óptica.
- Organización de los enlaces troncales.
- Mayor capacidad para incorporar nuevos enlaces.
- Facilidad de inspección y mantenimiento.
- Una ruta centralizada entre el MDF y los diferentes departamentos.
- Protección adicional en áreas de circulación.

El backbone deberá mantenerse organizado y separado de otros tipos de instalaciones cuando sea posible.

La ruta general será:

**MDF → ruta principal de bandeja cerrada → derivación hacia el departamento → terminación óptica → switch departamental**

---

### 11.3 Ruta General de Canalización

La canalización troncal partirá desde el MDF ubicado cerca del Hall Central y Vestíbulo de Ingreso.

Desde este punto se establecerán dos rutas principales de distribución:

#### Ruta hacia el sector izquierdo

Esta ruta atenderá principalmente:

- Sala de Capacitación.
- Recursos Humanos.
- Dirección General.

#### Ruta hacia el sector derecho

Esta ruta atenderá principalmente:

- Diseño e Innovación.
- Backend.
- Legal.
- Data Center.

Recepción podrá conectarse mediante una derivación cercana desde la zona central del MDF.

La ruta hacia el Data Center continuará mediante el corredor secundario ubicado en el extremo derecho del edificio.

---

### 11.4 Separación entre Canalización Horizontal y Troncal

Aunque ambos sistemas forman parte de la misma infraestructura física, se mantendrán claramente diferenciados.

| Segmento | Medio | Canalización propuesta |
|---|---|---|
| Horizontal | UTP Cat 6 | Canaleta cerrada de PVC |
| Troncal | Fibra óptica multimodo | Bandeja metálica cerrada |

Esta diferenciación facilita la identificación de las rutas y reduce la posibilidad de confundir el cableado de usuario con los enlaces principales del backbone.

---

### 11.5 Consideraciones de Instalación

Durante la instalación se deberán considerar los siguientes criterios:

- Evitar curvas excesivamente cerradas.
- Mantener protegidos los cables en zonas de tránsito.
- Evitar recorridos innecesariamente largos.
- Mantener espacio disponible para futuras ampliaciones.
- Identificar correctamente cada derivación hacia los departamentos.
- Facilitar el acceso para inspección y mantenimiento.
- Mantener una separación adecuada respecto a instalaciones eléctricas cuando sea posible.

La ruta definitiva será representada sobre el plano arquitectónico mediante líneas diferenciadas para el cableado troncal y el cableado horizontal.

En el diagrama físico final, las rutas de canalización se representan de forma simplificada mediante líneas de diferente color:

- **Verde:** recorrido correspondiente al cableado horizontal UTP Cat 6.
- **Azul:** recorrido correspondiente al cableado troncal de fibra óptica multimodo.

Las líneas representan las rutas generales propuestas y no la posición exacta de cada canaleta o bandeja. Durante una implementación real, el recorrido definitivo deberá ajustarse a las condiciones físicas del edificio, manteniendo las distancias, protección y criterios de instalación establecidos en este manual.

---

## 12. Rack del MDF

Para alojar y organizar los equipos principales de telecomunicaciones se propone instalar un **rack de piso** dentro del MDF.

La elección de un rack de piso en lugar de un gabinete de pared se debe a que el MDF concentrará varios elementos de infraestructura, entre ellos:

- Switch principal.
- ODF para la terminación de fibra óptica.
- Organizadores de cableado.
- UPS.
- Unidad de distribución eléctrica.
- Espacio disponible para futuras ampliaciones.

### 12.1 Tipo de Rack Seleccionado

Se propone utilizar un **rack de piso de 19 pulgadas**, con una capacidad inicial recomendada de **12U o superior**.

La capacidad definitiva podrá ajustarse durante la selección de los modelos comerciales, pero deberá permitir instalar los equipos actuales y mantener espacio libre para crecimiento.

### 12.2 Distribución Estimada del Rack

La siguiente distribución representa una propuesta inicial de utilización del espacio:

| Elemento | Espacio estimado |
|---|---:|
| ODF de fibra óptica | 1U |
| Organizador horizontal de cableado | 1U |
| Switch principal | 1U |
| Organizador horizontal adicional | 1U |
| Bandeja o espacio para equipo auxiliar | 1U |
| Espacio reservado para crecimiento | 4U o más |

El UPS podrá instalarse en la parte inferior del rack si el modelo seleccionado permite montaje en rack, o ubicarse sobre una base adecuada dentro del MDF en caso de utilizar un modelo tipo torre.

La distribución exacta dependerá de las dimensiones y características de los equipos seleccionados durante la adquisición.

### 12.3 Justificación del Rack de Piso

La utilización de un rack de piso ofrece las siguientes ventajas:

- **Mayor capacidad:** permite alojar varios equipos dentro de una misma estructura.
- **Soporte para el UPS:** el respaldo eléctrico puede representar uno de los equipos más pesados del MDF, por lo que un rack apoyado sobre el piso ofrece una mejor solución física.
- **Organización:** permite ordenar equipos, cableado óptico y alimentación eléctrica.
- **Mantenimiento:** facilita el acceso frontal y posterior a los dispositivos.
- **Escalabilidad:** permite reservar unidades de rack para futuros equipos.
- **Seguridad:** puede mantenerse dentro del MDF con acceso restringido.
- **Protección:** reduce la exposición directa de los equipos de telecomunicaciones.

### 12.4 Organización General del MDF

La organización física propuesta será aproximadamente la siguiente:

| Elemento | Función |
|---|---|
| ODF | Terminación y organización del backbone de fibra |
| Switch principal | Concentración de los 8 enlaces troncales |
| Organizadores | Gestión ordenada del cableado y patch cords |
| PDU | Distribución de energía dentro del rack |
| UPS | Respaldo eléctrico de los equipos principales |
| Espacio libre | Crecimiento futuro |

El MDF deberá mantener condiciones adecuadas de ventilación, seguridad y acceso para mantenimiento.

### 12.5 Esquema Conceptual

El rack puede representarse conceptualmente de la siguiente manera:

| Posición | Equipo |
|---|---|
| Parte superior | ODF |
|  | Organizador |
|  | Switch principal |
|  | Organizador |
|  | Espacio disponible |
|  | Espacio disponible |
| Parte inferior / área cercana | UPS |

Se recomienda mantener los elementos de interconexión y distribución en posiciones superiores para facilitar la organización del cableado. El UPS deberá ubicarse en la zona inferior del rack cuando sea compatible con montaje en rack o, en caso de utilizar un modelo tipo torre, sobre una superficie estable dentro del MDF.

---

## 13. Respaldo de Energía - UPS

La infraestructura principal ubicada en el MDF requiere un sistema de respaldo eléctrico que permita mantener operativos los equipos activos ante interrupciones breves del suministro de energía.

Para esta propuesta se contempla la instalación de **un UPS principal dentro del MDF**, destinado principalmente a respaldar:

- El switch principal.
- Equipos auxiliares activos instalados dentro del rack.
- Posibles equipos adicionales incorporados posteriormente en el MDF.

Los patch panels y el ODF son elementos pasivos, por lo que no requieren alimentación eléctrica.

Los switches departamentales se encuentran distribuidos físicamente en las diferentes áreas del edificio y, por lo tanto, no serán alimentados directamente por el UPS ubicado en el MDF.

---

### 13.1 Estimación del Consumo Eléctrico del Equipo Activo

Para dimensionar el respaldo eléctrico de la infraestructura se considera el consumo estimado de todo el equipo activo de red del edificio:

- 1 switch principal ubicado en el MDF.
- 4 switches departamentales de 8 puertos.
- 4 switches departamentales de 16 puertos.

Los valores utilizados son estimaciones de referencia. Antes de una implementación real deberán verificarse utilizando las fichas técnicas de los modelos comerciales adquiridos.

| Equipo | Cantidad | Consumo estimado por unidad | Consumo total |
|---|---:|---:|---:|
| Switch principal de agregación | 1 | 60 W | 60 W |
| Switch departamental de 8 puertos | 4 | 12 W | 48 W |
| Switch departamental de 16 puertos | 4 | 20 W | 80 W |
| **Total estimado** | **9** |  | **188 W** |

Por lo tanto, el consumo aproximado del equipo activo de red es de:

**188 W**

Para evitar dimensionar el sistema de respaldo exactamente al límite y mantener capacidad para pequeñas variaciones de consumo y crecimiento, se agrega un margen del **25 %**.

```text
188 W × 0.25 = 47 W

188 W + 47 W = 235 W
```

---

### 13.2 Capacidad Recomendada del UPS

Tomando como referencia una carga de diseño aproximada de **235 W**, se propone utilizar un UPS con capacidad de:

**1000 VA / 600 W o superior**

Esta capacidad supera ampliamente la potencia estimada y proporciona margen para futuras ampliaciones y equipos auxiliares.

| Característica | Recomendación |
|---|---|
| Capacidad aparente | 1000 VA o superior |
| Potencia real soportada | 600 W o superior |
| Consumo estimado de los 9 switches | 188 W |
| Potencia de diseño con margen | 235 W |
| Tipo recomendado | UPS line-interactive |
| Protección | Regulación de voltaje y respaldo por batería |
| Ubicación principal | MDF |

La autonomía exacta dependerá del modelo seleccionado, de la capacidad de sus baterías y de la carga conectada.

El cálculo de **235 W** representa la referencia de consumo del conjunto del equipo activo del edificio. Sin embargo, debido a que los ocho switches departamentales se encuentran distribuidos físicamente en diferentes áreas, un único UPS instalado en el MDF no puede alimentarlos directamente sin disponer de una infraestructura eléctrica respaldada que llegue hasta dichos departamentos.

---

### 13.3 Respaldo de los Switches Departamentales

Los ocho switches departamentales se encuentran distribuidos físicamente en diferentes áreas del edificio, por lo que no pueden conectarse directamente al UPS instalado dentro del MDF.

Si se desea proporcionar respaldo eléctrico también a estos equipos, será necesario implementar alguna de las siguientes alternativas:

1. Instalar un UPS local en cada departamento.
2. Utilizar circuitos eléctricos respaldados desde un sistema central.
3. Implementar posteriormente una solución de respaldo eléctrico distribuido.

Estas alternativas no se incluyen dentro del presupuesto actual de la práctica.

El UPS considerado en el presupuesto corresponde específicamente al **MDF y a los equipos activos instalados dentro de dicho cuarto de telecomunicaciones**.

### 13.4 Equipos Respaldados en el MDF

El UPS principal del MDF deberá respaldar como mínimo los siguientes elementos:

- Switch principal.
- Equipos auxiliares de telecomunicaciones que requieran alimentación.
- Elementos adicionales instalados posteriormente dentro del rack.

El ODF y los patch panels son elementos pasivos y, por lo tanto, no requieren alimentación eléctrica.

### 13.5 Justificación

La utilización de un UPS permite:

- Mantener temporalmente la conectividad durante interrupciones breves de energía.
- Proteger los equipos frente a variaciones de voltaje.
- Reducir el riesgo de apagados inesperados.
- Facilitar un apagado controlado en caso de una interrupción prolongada.
- Mantener capacidad disponible para futuras ampliaciones.

La capacidad definitiva del UPS deberá verificarse mediante las fichas técnicas de los equipos que se adquieran y su consumo eléctrico real antes de realizar la implementación.

---

## 14. Estándares T568A y T568B

Para las terminaciones de cableado de cobre se consideran los estándares **T568A y T568B**, los cuales definen el orden de los ocho conductores de un cable de par trenzado en una terminación RJ45.

En la infraestructura horizontal de QuetzalDev S.A. se utilizará **T568B como estándar principal**, manteniendo la misma disposición en ambos extremos de los enlaces UTP Cat 6.

Esto permite mantener uniformidad en toda la instalación y facilita las tareas de identificación, mantenimiento y reparación.

### 14.1 Disposición de Pines T568A

| Pin | Color del conductor |
|---:|---|
| 1 | Blanco / Verde |
| 2 | Verde |
| 3 | Blanco / Naranja |
| 4 | Azul |
| 5 | Blanco / Azul |
| 6 | Naranja |
| 7 | Blanco / Café |
| 8 | Café |

### 14.2 Disposición de Pines T568B

| Pin | Color del conductor |
|---:|---|
| 1 | Blanco / Naranja |
| 2 | Naranja |
| 3 | Blanco / Verde |
| 4 | Azul |
| 5 | Blanco / Azul |
| 6 | Verde |
| 7 | Blanco / Café |
| 8 | Café |

La principal diferencia entre T568A y T568B se encuentra en la posición de los pares verde y naranja.

---

### 14.3 Cable Straight-Through

Un cable **straight-through o directo** conserva la misma disposición de pines en ambos extremos.

Para QuetzalDev S.A. se utilizará la configuración:

**T568B → T568B**

Este esquema de terminación se utilizará en el canal de cableado horizontal de cobre, manteniendo T568B de forma uniforme en las terminaciones correspondientes.

Dentro de la infraestructura se aplica principalmente en:

- Patch cord del dispositivo final hacia la toma de red.
- Cableado permanente entre la toma de red y el patch panel.
- Patch cord entre el patch panel y el switch departamental.

#### Ejemplo de disposición Straight-Through T568B - T568B

| Pin | Extremo A - T568B | Extremo B - T568B |
|---:|---|---|
| 1 | Blanco / Naranja | Blanco / Naranja |
| 2 | Naranja | Naranja |
| 3 | Blanco / Verde | Blanco / Verde |
| 4 | Azul | Azul |
| 5 | Blanco / Azul | Blanco / Azul |
| 6 | Verde | Verde |
| 7 | Blanco / Café | Blanco / Café |
| 8 | Café | Café |

En este caso:

- Pin 1 → Pin 1
- Pin 2 → Pin 2
- Pin 3 → Pin 3
- Pin 4 → Pin 4
- Pin 5 → Pin 5
- Pin 6 → Pin 6
- Pin 7 → Pin 7
- Pin 8 → Pin 8

La secuencia se mantiene igual en ambos extremos.

---

### 14.4 Cable Crossover

Un cable **crossover o cruzado** utiliza diferentes estándares en cada extremo.

La configuración documentada será:

**T568A → T568B**

Este tipo de cable se utiliza tradicionalmente para conectar dispositivos del mismo tipo, por ejemplo:

- Switch → switch.
- PC → PC.

#### Ejemplo de disposición Crossover T568A - T568B

| Pin | Extremo A - T568A | Extremo B - T568B |
|---:|---|---|
| 1 | Blanco / Verde | Blanco / Naranja |
| 2 | Verde | Naranja |
| 3 | Blanco / Naranja | Blanco / Verde |
| 4 | Azul | Azul |
| 5 | Blanco / Azul | Blanco / Azul |
| 6 | Naranja | Verde |
| 7 | Blanco / Café | Blanco / Café |
| 8 | Café | Café |

En esta configuración se intercambian principalmente los pares verde y naranja.

Por ejemplo:

- Pin 1 se relaciona con el pin 3.
- Pin 2 se relaciona con el pin 6.
- Pin 3 se relaciona con el pin 1.
- Pin 6 se relaciona con el pin 2.

> **Nota:** El cable crossover se documenta como parte de los conocimientos de cableado de Capa 1. En el diseño físico propuesto para QuetzalDev S.A. no será utilizado, debido a que las conexiones entre switches se realizarán mediante fibra óptica multimodo.

---


### 14.5 Aplicación en QuetzalDev S.A.

Para la instalación propuesta se utilizará **T568B en ambos extremos del cableado horizontal**, generando conexiones straight-through.

| Segmento | Medio | Estándar / Terminación |
|---|---|---|
| Dispositivo final → toma | UTP Cat 6 | T568B |
| Toma → patch panel | UTP Cat 6 | T568B |
| Patch panel → switch | UTP Cat 6 | T568B |
| MDF → switch departamental | Fibra multimodo | No aplica T568A/T568B |

Los enlaces troncales no utilizan T568A ni T568B debido a que se implementarán mediante **fibra óptica multimodo**.

Por esta razón, aunque se documenta el cable crossover como evidencia del conocimiento de la Capa 1, no será necesario utilizarlo en los ocho enlaces troncales del diseño propuesto.

---

## 15. Tipo de Cable por Enlace

Para cada segmento de la topología se identifica el medio físico utilizado y, cuando corresponde cableado de cobre, el tipo de terminación aplicado.

En el diseño de QuetzalDev S.A. se utilizarán:

- **Straight-through T568B - T568B** para los enlaces horizontales UTP Cat 6.
- **Fibra óptica multimodo dúplex** para los enlaces troncales entre el MDF y los switches departamentales.
- **Crossover T568A - T568B** únicamente como referencia técnica, ya que no existe en la topología propuesta un enlace switch a switch implementado mediante cobre.

---

### 15.1 Enlaces Horizontales

Los enlaces horizontales conectan dispositivos finales con switches departamentales utilizando UTP Cat 6.

Debido a que se conectan dispositivos de diferente tipo, se utiliza cableado **straight-through**, manteniendo T568B en ambos extremos.

| Área / Departamento | Puntos incluidos | Cantidad | Dispositivos conectados | Medio | Tipo |
|---|---|---:|---|---|---|
| Recepción | `Recepcion-PR01` a `Recepcion-PR04` | 4 | Hosts ↔ Switch Recepción | UTP Cat 6 | Straight-through |
| Recursos Humanos | `RecursosHumanos-PR01` a `RecursosHumanos-PR08` | 8 | Hosts ↔ Switch RRHH | UTP Cat 6 | Straight-through |
| Legal | `Legal-PR01` a `Legal-PR04` | 4 | Hosts ↔ Switch Legal | UTP Cat 6 | Straight-through |
| Sala de Capacitación | `Capacitacion-PR01` a `Capacitacion-PR10` | 10 | Hosts ↔ Switch Capacitación | UTP Cat 6 | Straight-through |
| Diseño e Innovación | `DisenoInnovacion-PR01` a `DisenoInnovacion-PR08` | 8 | Hosts ↔ Switch Diseño | UTP Cat 6 | Straight-through |
| Dirección General | `DireccionGeneral-PR01` a `DireccionGeneral-PR04` | 4 | Hosts ↔ Switch Dirección | UTP Cat 6 | Straight-through |
| Backend | `Backend-PR01` a `Backend-PR07` | 7 | Hosts ↔ Switch Backend | UTP Cat 6 | Straight-through |
| Data Center | `DataCenter-PR01` a `DataCenter-PR03` | 3 | Servidores ↔ Switch Data Center | UTP Cat 6 | Straight-through |
| **Total** |  | **48** |  |  |  |

Todos estos enlaces utilizarán la siguiente terminación:

**T568B → T568B**

El recorrido físico completo de cada enlace horizontal será:

**Dispositivo → patch cord → toma de red → UTP Cat 6 → patch panel → patch cord → switch departamental**

---

### 15.2 Enlaces Troncales

Los enlaces troncales conectan el switch principal ubicado en el MDF con los switches de cada área.

Debido a que estos enlaces se implementarán mediante fibra óptica multimodo, los estándares T568A y T568B no son aplicables.

| Etiqueta | Origen | Destino | Medio | Tipo de enlace |
|---|---|---|---|---|
| `MDF-Recepcion` | Switch principal | Switch Recepción | Fibra multimodo | Óptico dúplex |
| `MDF-RecursosHumanos` | Switch principal | Switch RRHH | Fibra multimodo | Óptico dúplex |
| `MDF-Legal` | Switch principal | Switch Legal | Fibra multimodo | Óptico dúplex |
| `MDF-Capacitacion` | Switch principal | Switch Capacitación | Fibra multimodo | Óptico dúplex |
| `MDF-DisenoInnovacion` | Switch principal | Switch Diseño | Fibra multimodo | Óptico dúplex |
| `MDF-DireccionGeneral` | Switch principal | Switch Dirección | Fibra multimodo | Óptico dúplex |
| `MDF-Backend` | Switch principal | Switch Backend | Fibra multimodo | Óptico dúplex |
| `MDF-DataCenter` | Switch principal | Switch Data Center | Fibra multimodo | Óptico dúplex |

En total existen **8 enlaces troncales de fibra óptica multimodo**.

---

### 15.3 Uso de Cable Crossover

El cable crossover se utiliza tradicionalmente para conectar directamente dispositivos del mismo tipo mediante cobre, por ejemplo:

- Switch ↔ Switch.
- PC ↔ PC.

Su configuración corresponde a:

**T568A → T568B**

Sin embargo, **no se utilizará cable crossover en la infraestructura propuesta de QuetzalDev S.A.**, debido a que las conexiones entre el switch principal y los switches departamentales se realizarán mediante fibra óptica multimodo.

El crossover fue documentado en la sección anterior como evidencia de comprensión de los estándares de Capa 1.

---

### 15.4 Resumen

| Segmento | Cantidad de enlaces | Medio | Terminación / Tipo |
|---|---:|---|---|
| Horizontal | 48 | UTP Cat 6 | Straight-through T568B - T568B |
| Troncal | 8 | Fibra óptica multimodo | Óptico dúplex |
| Crossover utilizado físicamente | 0 | — | No aplica |

Por lo tanto, la topología física contempla un total de **56 enlaces de red**:

- **48 enlaces horizontales de cobre.**
- **8 enlaces troncales de fibra óptica.**

---

## 16. Etiquetado del Cableado

Para facilitar la identificación, mantenimiento y documentación de la infraestructura física, todos los puntos de red y enlaces troncales serán etiquetados mediante un esquema uniforme.

Se utilizarán identificadores diferentes para:

- Cableado horizontal.
- Cableado troncal.
- Tomas físicas.

---

### 16.1 Etiquetado del Cableado Horizontal

Para los puntos correspondientes al cableado horizontal se utilizará el siguiente formato:

`[Área/Departamento]-[Número de Punto de Red]`

El número de punto será representado mediante el prefijo `PR` seguido de dos dígitos.

Ejemplos:

- `Recepcion-PR01`
- `RecursosHumanos-PR04`
- `Legal-PR03`
- `Capacitacion-PR08`
- `DisenoInnovacion-PR05`
- `DireccionGeneral-PR02`
- `Backend-PR07`
- `DataCenter-PR03`

Cada identificador se asociará al mismo enlace durante todo su recorrido, permitiendo relacionar:

**Toma de red → cable horizontal → patch panel → switch departamental**

---

### 16.2 Etiquetas por Departamento

| Área / Departamento | Rango de etiquetas |
|---|---|
| Recepción | `Recepcion-PR01` a `Recepcion-PR04` |
| Recursos Humanos | `RecursosHumanos-PR01` a `RecursosHumanos-PR08` |
| Legal | `Legal-PR01` a `Legal-PR04` |
| Sala de Capacitación | `Capacitacion-PR01` a `Capacitacion-PR10` |
| Diseño e Innovación | `DisenoInnovacion-PR01` a `DisenoInnovacion-PR08` |
| Dirección General | `DireccionGeneral-PR01` a `DireccionGeneral-PR04` |
| Backend | `Backend-PR01` a `Backend-PR07` |
| Data Center | `DataCenter-PR01` a `DataCenter-PR03` |

En total se dispondrá de **48 identificadores correspondientes a los 48 puntos de red**.

---

### 16.3 Etiquetado de Tomas Físicas

Además de la identificación individual de cada puerto, las cajas o tomas físicas tendrán un identificador propio.

El formato utilizado será:

`[Abreviatura del Área]-T[Número de Toma]`

Ejemplos:

- `REC-T01`
- `RRHH-T02`
- `LEG-T01`
- `CAP-T04`
- `DIS-T03`
- `DIR-T02`
- `BACK-T04`
- `DC-T01`

El identificador de la toma no sustituye la etiqueta del punto de red.

Por ejemplo:

`REC-T01`

puede contener:

- `Recepcion-PR01`
- `Recepcion-PR02`
- `Recepcion-PR03`

De esta forma se diferencia claramente la **caja física** de los **puertos de red individuales** contenidos en ella.

---

### 16.4 Etiquetado del Cableado Troncal

Para los enlaces troncales se utilizará el siguiente formato:

`MDF-[Área/Departamento]`

Cada etiqueta identifica el enlace de fibra óptica entre el MDF y el switch correspondiente.

| Enlace | Etiqueta |
|---|---|
| MDF → Recepción | `MDF-Recepcion` |
| MDF → Recursos Humanos | `MDF-RecursosHumanos` |
| MDF → Legal | `MDF-Legal` |
| MDF → Sala de Capacitación | `MDF-Capacitacion` |
| MDF → Diseño e Innovación | `MDF-DisenoInnovacion` |
| MDF → Dirección General | `MDF-DireccionGeneral` |
| MDF → Backend | `MDF-Backend` |
| MDF → Data Center | `MDF-DataCenter` |

En total se dispondrá de **8 etiquetas correspondientes a los 8 enlaces troncales**.

---

### 16.5 Aplicación de las Etiquetas

Las etiquetas deberán colocarse en puntos que permitan identificar fácilmente cada conexión.

Para el cableado horizontal se recomienda identificar:

- Puerto de la toma de red.
- Ambos extremos del cable horizontal.
- Puerto correspondiente del patch panel.

Para el cableado troncal se deberá identificar:

- Terminación en el MDF.
- Puerto correspondiente del ODF.
- Extremo de fibra ubicado en el departamento.
- Terminación asociada al switch departamental.

Esto permitirá realizar tareas de mantenimiento y localización de enlaces sin necesidad de seguir físicamente todo el recorrido del cable.

En el diagrama físico final se utiliza una representación resumida del etiquetado para evitar saturar visualmente el plano. El detalle completo de la relación entre tomas físicas, puntos de red y enlaces troncales se documenta en las tablas del presente Manual Técnico.

---

### 16.6 Resumen del Sistema de Etiquetado

| Elemento | Formato | Ejemplo |
|---|---|---|
| Punto de red horizontal | `[Área]-PR##` | `Backend-PR03` |
| Toma física | `[Abreviatura]-T##` | `BACK-T02` |
| Enlace troncal | `MDF-[Área]` | `MDF-Backend` |

El esquema utilizado en esta práctica es intencionalmente sencillo y permite identificar rápidamente el área y el punto asociado a cada conexión.

En la siguiente sección se comparará este sistema con el estándar **TIA/EIA-606**, identificando sus principales diferencias y la conveniencia de utilizar un esquema de administración más completo en una infraestructura real.

---

## 17. Comparación con el Estándar TIA/EIA-606

El sistema de etiquetado utilizado para QuetzalDev S.A. fue diseñado de forma simplificada para facilitar la identificación de los puntos de red y enlaces troncales dentro de la práctica.

El esquema empleado permite identificar principalmente:

- El área o departamento.
- El número del punto de red.
- El enlace troncal correspondiente al MDF.
- La toma física asociada.

Ejemplos:

- `Recepcion-PR01`
- `Backend-PR05`
- `MDF-DataCenter`
- `RRHH-T02`

Aunque este sistema permite identificar rápidamente las conexiones principales, un entorno empresarial real requiere un esquema de administración más completo.

### 17.1 Esquema Utilizado en la Práctica

El etiquetado horizontal utiliza el formato:

`[Área/Departamento]-[Número de Punto de Red]`

Por ejemplo:

`Backend-PR03`

Para los enlaces troncales se utiliza:

`MDF-[Área/Departamento]`

Por ejemplo:

`MDF-Backend`

Este esquema tiene como principal ventaja su sencillez y facilidad de interpretación.

---

### 17.2 Estándar TIA/EIA-606

TIA/EIA-606 establece principios para la administración e identificación de la infraestructura de telecomunicaciones.

Su objetivo no consiste únicamente en colocar una etiqueta sobre un cable, sino en mantener una relación organizada entre los diferentes componentes de la infraestructura, tales como:

- Cables.
- Puertos.
- Espacios de telecomunicaciones.
- Equipos de terminación.
- Rutas y canalizaciones.
- Elementos de conexión.
- Registros asociados a la infraestructura.

De esta forma, la identificación física se complementa con documentación que permita conocer la función, ubicación y relación de cada elemento.

---

### 17.3 Comparación

| Característica | Esquema de QuetzalDev | TIA/EIA-606 |
|---|---|---|
| Identificación del área | Incluida directamente en la etiqueta | Utiliza identificadores estructurados asociados a la infraestructura |
| Identificación del punto | Número simple `PR##` | Permite administrar identificadores únicos de los elementos |
| Cableado troncal | `MDF-[Área]` | Puede relacionarse con espacios, terminaciones y registros de administración |
| Tomas físicas | Identificación simplificada `T##` | Se integran dentro de un sistema completo de administración |
| Canalizaciones | Se representan principalmente en el plano | Pueden formar parte de los registros de infraestructura |
| Documentación | Manual y plano de la práctica | Administración estructurada y registros asociados |
| Complejidad | Baja | Mayor |
| Aplicación | Proyecto académico | Infraestructuras profesionales de telecomunicaciones |

---

### 17.4 Diferencias Principales

#### 1. Nivel de información del identificador

El esquema utilizado en esta práctica se concentra principalmente en identificar el departamento y el número del punto.

Por ejemplo:

`Legal-PR03`

Este formato permite reconocer rápidamente que el punto pertenece al Departamento Legal y que corresponde al punto número 03.

Sin embargo, un sistema basado completamente en TIA/EIA-606 puede relacionar el identificador con información adicional de administración, como la ubicación física, espacio de telecomunicaciones, terminaciones y registros correspondientes.

Por lo tanto, el sistema utilizado en QuetzalDev es más sencillo pero contiene menos información administrativa.

#### 2. Administración de la infraestructura

En la práctica, las etiquetas se utilizan principalmente para reconocer cables, tomas y enlaces.

TIA/EIA-606 contempla una administración más amplia de la infraestructura de telecomunicaciones, relacionando los identificadores con documentación y registros.

Esto permite que un técnico pueda determinar no solamente a qué departamento pertenece un enlace, sino también cómo se relaciona con otros componentes de la infraestructura.

---

### 17.5 Ventajas del Esquema Simplificado

El esquema utilizado para QuetzalDev presenta algunas ventajas dentro del alcance de la práctica:

- Es fácil de comprender.
- Permite reconocer rápidamente el departamento.
- Facilita la identificación de los 48 puntos de red.
- Permite diferenciar los enlaces horizontales de los troncales.
- Reduce la complejidad de documentación para una infraestructura relativamente pequeña.

Por ejemplo:

`RecursosHumanos-PR05`

puede interpretarse inmediatamente como el punto de red número 05 del Departamento de Recursos Humanos.

---

### 17.6 Uso del Estándar Completo en un Entorno Real

En una implementación empresarial real sería recomendable utilizar un sistema de administración basado completamente en TIA/EIA-606.

Esto sería especialmente importante si QuetzalDev creciera y llegara a disponer de:

- Más pisos.
- Más cuartos de telecomunicaciones.
- Varios racks.
- Mayor cantidad de usuarios.
- Nuevos Data Centers.
- Más rutas de canalización.
- Varios edificios.
- Mayor cantidad de enlaces troncales.

En estas condiciones, utilizar únicamente etiquetas como `Backend-PR01` podría resultar insuficiente para administrar toda la infraestructura.

Un esquema completo permitiría mantener una relación más precisa entre:

**Ubicación → espacio de telecomunicaciones → terminación → cable → toma → dispositivo**

Esto facilita las tareas de mantenimiento, solución de problemas, auditoría y ampliación de la red.

### 17.7 Conclusión de la Comparación

Para el alcance de esta práctica, el esquema de etiquetado simplificado proporciona suficiente información para identificar los puntos de red y enlaces troncales de QuetzalDev S.A.

Sin embargo, en una infraestructura empresarial de mayor tamaño sería recomendable utilizar completamente los principios de TIA/EIA-606, debido a que permiten una administración más estructurada y escalable de los componentes de telecomunicaciones.

---

## 18. Flujo de Conexión End-to-End

El flujo de conexión end-to-end permite visualizar el recorrido físico que sigue una conexión desde un dispositivo final hasta el switch principal ubicado en el MDF.

En la infraestructura propuesta para QuetzalDev S.A., el recorrido general será:

**Dispositivo final → Patch cord UTP Cat 6 → Toma de red → Cableado horizontal UTP Cat 6 → Patch panel → Patch cord UTP Cat 6 → Switch departamental → Patch cord óptico → Terminación óptica departamental → Fibra óptica multimodo → ODF del MDF → Patch cord óptico → Switch principal del MDF**

### 18.1 Recorrido General

El flujo físico puede representarse de la siguiente manera:

```text
Dispositivo final
      │
      │ Patch cord UTP Cat 6
      ▼
Toma de red
      │
      │ Cableado horizontal UTP Cat 6
      ▼
Patch panel
      │
      │ Patch cord UTP Cat 6
      ▼
Switch departamental
      │
      │ Patch cord óptico
      ▼
Terminación óptica departamental
      │
      │ Fibra óptica multimodo
      │ Cableado troncal
      ▼
ODF ubicado en el MDF
      │
      │ Patch cord óptico
      ▼
Switch principal del MDF
```

Este recorrido se mantiene para todos los departamentos, variando únicamente la identificación del punto de red, el switch departamental y el enlace troncal correspondiente.

### 18.2 Ejemplo: Recursos Humanos

Para un equipo ubicado en Recursos Humanos, por ejemplo `RecursosHumanos-PR03`, el flujo sería:

**PC de Recursos Humanos → toma asociada a `RecursosHumanos-PR03` → cableado horizontal UTP Cat 6 → patch panel de Recursos Humanos → switch de Recursos Humanos → patch cord óptico → terminación óptica departamental → enlace `MDF-RecursosHumanos` mediante fibra óptica multimodo → ODF del MDF → patch cord óptico → switch principal del MDF**

En este recorrido:

* El segmento desde la toma hasta el switch departamental corresponde al **cableado horizontal**.
* El segmento desde el switch departamental hasta el MDF corresponde al **cableado troncal**.
* El cableado horizontal utiliza **UTP Cat 6**.
* El backbone utiliza **fibra óptica multimodo**.

### 18.3 Ejemplo: Data Center

Para uno de los servidores principales, por ejemplo `DataCenter-PR01`, el flujo será:

**Servidor → toma asociada a `DataCenter-PR01` → cableado horizontal UTP Cat 6 → patch panel del Data Center → switch del Data Center → patch cord óptico → terminación óptica del Data Center → enlace `MDF-DataCenter` mediante fibra óptica multimodo → ODF del MDF → patch cord óptico → switch principal del MDF**

El Data Center mantiene la misma estructura de conexión que las demás áreas, aunque sus dispositivos finales corresponden exclusivamente a servidores.

| Segmento | Origen | Destino | Medio |
|---|---|---|---|
| Área de trabajo | Dispositivo final | Toma de red | Patch cord UTP Cat 6 |
| Cableado horizontal | Toma de red | Patch panel | UTP Cat 6 |
| Interconexión local | Patch panel | Switch departamental | Patch cord UTP Cat 6 |
| Interconexión óptica local | Switch departamental | Terminación óptica | Patch cord óptico |
| Cableado troncal | Terminación óptica departamental | ODF del MDF | Fibra óptica multimodo |
| Distribución central | ODF | Switch principal | Patch cord óptico |


### 18.5 Importancia del Flujo End-to-End

Documentar el recorrido completo permite:

* Identificar rápidamente los componentes involucrados en una conexión.
* Facilitar las tareas de mantenimiento.
* Localizar posibles fallas físicas.
* Relacionar las etiquetas con los dispositivos y puertos correspondientes.
* Diferenciar claramente el cableado horizontal del cableado troncal.
* Mantener organizada la infraestructura física.
* Facilitar futuras ampliaciones o modificaciones de la red.

Este flujo también servirá como referencia para representar las conexiones principales dentro del diagrama físico final.


---

## 19. Consideraciones de Escalabilidad Futura

El diseño físico de la red de QuetzalDev S.A. fue planteado no solamente para cubrir los requerimientos actuales, sino también para permitir futuras ampliaciones sin necesidad de reemplazar inmediatamente los principales elementos de infraestructura.

Actualmente la empresa dispone de **48 dispositivos finales**, distribuidos entre sus ocho áreas. Para facilitar un crecimiento posterior se ha dejado capacidad disponible en switches, patch panels, infraestructura óptica y rack.

### 19.1 Crecimiento de Dispositivos

Los switches departamentales fueron seleccionados con una cantidad de puertos superior al número de dispositivos actualmente conectados.

| Área / Departamento  | Dispositivos actuales | Puertos RJ45 disponibles | Puertos libres |
| -------------------- | --------------------: | -----------------------: | -------------: |
| Recepción            |                     4 |                        8 |              4 |
| Recursos Humanos     |                     8 |                       16 |              8 |
| Legal                |                     4 |                        8 |              4 |
| Sala de Capacitación |                    10 |                       16 |              6 |
| Diseño e Innovación  |                     8 |                       16 |              8 |
| Dirección General    |                     4 |                        8 |              4 |
| Backend              |                     7 |                       16 |              9 |
| Data Center          |                     3 |                        8 |              5 |
| **Total**            |                **48** |                   **96** |         **48** |

Los switches departamentales disponen en conjunto de **48 puertos RJ45 libres**, lo que proporciona capacidad suficiente para futuras ampliaciones.

Sin embargo, la cantidad de nuevos puntos de red que puede incorporarse sin ampliar otros elementos de distribución está limitada actualmente por la capacidad disponible de los patch panels, los cuales disponen de **32 puertos libres**.

Por lo tanto, la infraestructura actual permite incorporar hasta **32 nuevos puntos de red cableados** utilizando la capacidad existente de switches y patch panels. Una ampliación superior requeriría aumentar también la capacidad de los patch panels y demás elementos asociados.

#### Capacidad de Crecimiento por Departamento

| Área / Departamento | Puertos libres en switch | Puertos libres en patch panel | Nuevos puntos posibles sin ampliación |
|---|---:|---:|---:|
| Recepción | 4 | 4 | 4 |
| Recursos Humanos | 8 | 4 | 4 |
| Legal | 4 | 4 | 4 |
| Sala de Capacitación | 6 | 2 | 2 |
| Diseño e Innovación | 8 | 4 | 4 |
| Dirección General | 4 | 4 | 4 |
| Backend | 9 | 5 | 5 |
| Data Center | 5 | 5 | 5 |
| **Total** | **48** | **32** | **32** |

La cantidad de nuevos puntos posibles se determina por el elemento con menor capacidad disponible en cada departamento. Por esta razón, aunque los switches disponen de 48 puertos RJ45 libres en conjunto, la capacidad inmediata de crecimiento queda limitada a **32 nuevos puntos de red**, debido a la disponibilidad de los patch panels.



### 19.2 Capacidad de los Patch Panels

Los patch panels también fueron dimensionados con capacidad adicional.

| Concepto                           | Cantidad |
| ---------------------------------- | -------: |
| Puntos de red actuales             |       48 |
| Puertos instalados en patch panels |       80 |
| Puertos disponibles                |       32 |

Los **32 puertos libres** de los patch panels representan actualmente el límite de crecimiento inmediato del cableado horizontal. Estos puertos permiten incorporar hasta 32 nuevos puntos de red utilizando los switches existentes, siempre que también se instalen las tomas, cableado UTP Cat 6, keystone jacks y demás componentes necesarios para cada nueva conexión.

### 19.3 Escalabilidad del Backbone

El backbone utiliza **fibra óptica multimodo**, proporcionando una infraestructura adecuada para futuras necesidades de mayor capacidad de transmisión.

Actualmente existen:

* 8 enlaces troncales.
* 1 enlace por cada área.
* 16 fibras utilizadas considerando enlaces dúplex.

El ODF propuesto cuenta con capacidad para **24 fibras**, dejando:

**8 fibras disponibles para futuras ampliaciones.**

También se recomienda que los switches departamentales dispongan de interfaces SFP/SFP+ adicionales cuando sea posible.

Considerando que cada enlace óptico dúplex utiliza dos fibras, esta capacidad disponible permitiría implementar hasta **4 enlaces dúplex adicionales**, siempre que también exista capacidad suficiente en el switch principal y en los demás elementos ópticos.

### 19.4 Capacidad del Switch Principal

El switch principal requiere actualmente ocho interfaces ópticas, una por cada switch departamental.

Durante la selección del equipo comercial se buscará una capacidad superior a ocho interfaces para permitir:

* Incorporación de nuevos departamentos.
* Nuevos enlaces hacia equipos de infraestructura.
* Ampliaciones del Data Center.
* Posibles enlaces redundantes.

De esta manera, el crecimiento de la red no estará limitado exclusivamente a la cantidad de enlaces utilizados actualmente.

### 19.5 Espacio Disponible en el Rack

Para el presupuesto se tomó como referencia comercial un rack de piso de **42U**, el cual supera la capacidad mínima establecida para el diseño y proporciona espacio adicional para futuras ampliaciones. La capacidad de 12U corresponde al requerimiento mínimo estimado, mientras que el modelo comercial seleccionado como referencia dispone de una capacidad mayor.

Este espacio permitirá incorporar posteriormente elementos como:

* Nuevos switches.
* Equipos de seguridad.
* Nuevos elementos de distribución óptica.
* Organizadores adicionales.
* Equipos de telecomunicaciones.
* Sistemas de administración de red.

### 19.6 Canalización

Las rutas de canalización deberán instalarse evitando utilizar el 100 % de su capacidad.

Esto permitirá introducir nuevos cables UTP o enlaces ópticos sin sustituir completamente la canalización existente.

La utilización de canaletas para el cableado horizontal y bandeja metálica para el backbone facilita futuras modificaciones y ampliaciones.

### 19.7 Reserva de Cableado

El cálculo realizado para el cable UTP Cat 6 determina la adquisición de **dos bobinas de 305 metros**.

Aunque la cantidad disponible supera el consumo estimado inicial, el cable restante podrá utilizarse para:

* Nuevos puntos de red.
* Sustitución de enlaces dañados.
* Reubicación de estaciones de trabajo.
* Mantenimiento.
* Ampliaciones futuras.

De igual manera, se contempla una reserva en el cálculo del cableado troncal para compensar ajustes de instalación.

### 19.8 Resumen de Escalabilidad

| Elemento | Situación actual | Capacidad para crecimiento |
|---|---|---|
| Switches departamentales | 48 puertos utilizados de 96 | 48 puertos RJ45 libres |
| Patch panels | 48 puertos utilizados de 80 | 32 puertos libres |
| Crecimiento inmediato de puntos cableados | 48 puntos actuales | Hasta 32 nuevos puntos utilizando la infraestructura de distribución existente |
| ODF | 16 fibras utilizadas de 24 | 8 fibras libres, equivalentes a hasta 4 enlaces dúplex |
| Switch principal | 8 enlaces necesarios | Se seleccionará capacidad superior a 8 |
| Rack | Equipos actuales | Espacio reservado |
| Canalización | Rutas actuales | Capacidad prevista para nuevos cables |
| Cable UTP | Aproximadamente 345 m requeridos | Reserva disponible de las bobinas adquiridas |


---

## 20. Presupuesto Estimado

El siguiente presupuesto presenta una estimación de los materiales y equipos necesarios para implementar la infraestructura física propuesta para QuetzalDev S.A.

Los precios corresponden a valores de referencia consultados en comercios de Guatemala durante agosto de 2026. Los elementos marcados como **estimados** deberán ser confirmados mediante una cotización formal antes de realizar una implementación real.

| Equipo / Material | Cantidad | Precio unitario aproximado | Subtotal |
|---|---:|---:|---:|
| Switch principal MikroTik con capacidad superior a 8 interfaces SFP | 1 | Q4,166.00 | Q4,166.00 |
| Switch Grandstream administrable de 8 puertos con interfaces SFP | 4 | Q1,177.00 | Q4,708.00 |
| Switch Grandstream administrable de 16 puertos con interfaces SFP | 4 | Q1,727.00 | Q6,908.00 |
| Kit MikroTik de 2 módulos SFP 1.25G (16 módulos en total) | 8 kits | Q698.00 | Q5,584.00 |
| Bobina Xtech XTC-226 UTP Cat 6 de 305 m | 2 | Q519.00 | Q1,038.00 |
| Patch panel Cat 6 de 8 puertos | 4 | Q150.00 | Q600.00 |
| Patch panel Cat 6 de 12 puertos | 4 | Q200.00 | Q800.00 |
| Keystone Jack RJ45 Cat 6 | 48 | Q20.00 | Q960.00 |
| Placas y cajas para las 25 tomas de red | 1 lote | Q181.00 | Q181.00 |
| Patch cord UTP Cat 6 | 96 | Q18.00 | Q1,728.00 |
| ODF de 24 fibras para montaje en rack | 1 | Q600.00 | Q600.00 |
| Fibra óptica multimodo para backbone, aproximadamente 100 m | 1 | Q1,500.00 | Q1,500.00 |
| Caja de terminación óptica departamental | 8 | Q150.00 | Q1,200.00 |
| Patch cord óptico dúplex | 16 | Q75.00 | Q1,200.00 |
| Pigtails, adaptadores y accesorios para fibra óptica | 1 lote | Q800.00 | Q800.00 |
| Rack NextLink de piso de 4 postes, 19 pulgadas, 42U | 1 | Q1,812.00 | Q1,812.00 |
| Organizador horizontal NextLink de cableado 1U | 2 | Q104.00 | Q208.00 |
| PDU para rack | 1 | Q350.00 | Q350.00 |
| APC Easy UPS BV1000, 1000 VA / 600 W | 1 | Q714.00 | Q714.00 |
| Canaleta cerrada de PVC para cableado horizontal | 100 m aprox. | Q15.00/m | Q1,500.00 |
| Bandeja metálica cerrada para backbone | 30 m aprox. | Q75.00/m | Q2,250.00 |
| Material para etiquetado y consumibles | 1 lote | Q150.00 | Q150.00 |
| **TOTAL ESTIMADO** |  |  | **Q38,957.00** |

### 20.1 Consideraciones del Presupuesto

El presupuesto total estimado para la infraestructura física propuesta es de:

**Q38,957.00**

Este valor debe considerarse referencial, debido a que los precios, marcas y disponibilidad de los productos pueden variar al momento de realizar la compra.

El presupuesto contempla principalmente:

- Switch principal.
- Switches departamentales.
- Módulos SFP.
- Cableado UTP Cat 6.
- Fibra óptica multimodo.
- Patch panels.
- ODF.
- Tomas y conectores.
- Patch cords.
- Rack.
- UPS.
- Canalización.
- Elementos de organización y etiquetado.

No se incluyen dentro del presupuesto:

- Mano de obra.
- Obra civil.
- Instalación eléctrica.
- Herramientas especializadas.
- Certificación del cableado.
- Configuración de los dispositivos.
- Gastos de envío o transporte.

### 20.2 Compatibilidad de los Componentes

Antes de realizar la adquisición definitiva se deberá verificar la compatibilidad entre:

- Switches y módulos SFP/SFP+.
- Módulos ópticos y fibra multimodo.
- Conectores y ODF.
- Patch panels y cable UTP Cat 6.
- Keystone jacks y placas de las tomas de red.

La selección definitiva de marcas y modelos deberá realizarse mediante fichas técnicas y cotizaciones actualizadas.

### 20.3 Observación sobre el Costo del Backbone

El uso de fibra óptica multimodo en los ocho enlaces troncales representa una inversión inicial mayor respecto a una solución basada completamente en cobre.

Sin embargo, esta decisión proporciona beneficios como:

- Mayor capacidad de transmisión.
- Mayor posibilidad de crecimiento.
- Inmunidad frente a interferencias electromagnéticas.
- Infraestructura adecuada para futuras ampliaciones del backbone.

Por esta razón, se considera que la inversión adicional se encuentra justificada dentro del diseño propuesto para QuetzalDev S.A.

### 20.4 Referencias Comerciales del Presupuesto

Para la elaboración del presupuesto se consultaron catálogos comerciales disponibles en Guatemala, principalmente para obtener valores de referencia de switches, módulos ópticos, cableado UTP, componentes de terminación, rack y sistema UPS.

Entre las marcas utilizadas como referencia se encuentran:

- Grandstream para switches departamentales.
- MikroTik para el switch principal y módulos SFP.
- Xtech para la bobina UTP Cat 6.
- Linet-Lan para keystone jacks y patch cords Cat 6.
- NextLink para rack y organizadores de cableado.
- APC para el sistema UPS.

Los precios corresponden a valores consultados durante agosto de 2026 y pueden variar de acuerdo con disponibilidad, promociones, proveedor y fecha de adquisición.

Los elementos para los cuales no se seleccionó un modelo comercial específico mantienen un precio aproximado dentro del presupuesto y deberán ser confirmados mediante una cotización antes de realizar una implementación real.

### 20.5 Compra de Materiales y Uso de Proveedor Especializado

Para una posible implementación de la infraestructura se pueden considerar dos alternativas principales: realizar la compra individual de los materiales o contratar a un proveedor especializado que suministre e instale la solución completa.

La compra individual permite comparar precios entre diferentes distribuidores y seleccionar de forma independiente los switches, cableado, rack, UPS y accesorios. Esta alternativa puede permitir un mayor control sobre el presupuesto, pero requiere verificar cuidadosamente la compatibilidad entre los diferentes componentes adquiridos.

Por otro lado, trabajar con un proveedor especializado puede facilitar la instalación, terminación y certificación del cableado estructurado. Esta opción resulta especialmente conveniente para el backbone de fibra óptica, debido a que su instalación y terminación puede requerir herramientas, conocimientos y equipos especializados.

Para QuetzalDev S.A. se propone una estrategia combinada. Los equipos y materiales estandarizados pueden adquirirse directamente utilizando el presupuesto presentado, mientras que para la instalación, terminación y certificación de la fibra óptica se recomienda considerar el apoyo de un proveedor especializado.

El costo de mano de obra, instalación y certificación no se encuentra incluido dentro del presupuesto actual y deberá cotizarse por separado antes de realizar una implementación real.

---

## 21. Conclusiones

El diseño físico desarrollado para QuetzalDev S.A. permite organizar de forma estructurada la infraestructura de red requerida para los ocho departamentos de la empresa, considerando un total de **48 dispositivos finales**, distribuidos entre computadoras de escritorio, laptops y servidores.

La utilización de una **topología jerárquica tipo árbol o estrella extendida** permite centralizar los enlaces troncales en el MDF y mantener una topología en estrella dentro de cada departamento. Esta estructura facilita la administración, identificación y mantenimiento de las conexiones físicas.

Para el cableado horizontal se seleccionó **UTP categoría 6**, debido a que las distancias internas son adecuadas para este medio y representa una solución práctica y económica para conectar los dispositivos finales. Para el cableado troncal se propuso **fibra óptica multimodo**, proporcionando mayor capacidad de transmisión, inmunidad frente a interferencias electromagnéticas y mejores posibilidades de crecimiento futuro.

La ubicación del MDF en una zona central cercana al Hall Central y al Vestíbulo permite reducir los recorridos hacia los diferentes departamentos y facilita la distribución de las rutas de canalización. Dentro del MDF se concentran los principales elementos de infraestructura, como el switch principal, ODF, rack, organizadores y sistema de respaldo eléctrico.

El dimensionamiento de switches, patch panels, ODF y canalización se realizó dejando capacidad disponible para futuras ampliaciones. Actualmente se requieren 48 puntos de red, mientras que la propuesta mantiene puertos adicionales en los switches, patch panels y fibras disponibles en el ODF.

También se estableció un sistema de etiquetado para identificar puntos de red, tomas físicas y enlaces troncales, permitiendo relacionar cada conexión con su ubicación y recorrido. Aunque el esquema utilizado es simplificado, se comparó con los principios establecidos por TIA/EIA-606 para reconocer la importancia de una administración estructurada de la infraestructura de telecomunicaciones.

Finalmente, el presupuesto estimado permite identificar los principales materiales y equipos necesarios para una posible implementación del diseño. Debido a que las cantidades, distancias y precios fueron obtenidos a partir del plano y de valores de referencia, estos deberán verificarse mediante mediciones físicas y cotizaciones actualizadas antes de realizar una instalación real.

---

## 22. Referencias

1. Universidad de San Carlos de Guatemala, Facultad de Ingeniería, Escuela de Ingeniería en Ciencias y Sistemas. (2026). **Práctica 1 - QuetzalDev S.A.** Laboratorio de Redes de Computadoras 1, Segundo Semestre 2026.

2. Universidad de San Carlos de Guatemala, Facultad de Ingeniería, Escuela de Ingeniería en Ciencias y Sistemas. (2026). **Lectura Semana 2 - Conceptos Generales de Redes de Computadoras.** Laboratorio de Redes de Computadoras 1.

3. Universidad de San Carlos de Guatemala, Facultad de Ingeniería, Escuela de Ingeniería en Ciencias y Sistemas. (2026). **Semana 2 - Conceptos Generales.** Unidad 1: Fundamentos e Infraestructura de las Redes.

4. Universidad de San Carlos de Guatemala, Facultad de Ingeniería, Escuela de Ingeniería en Ciencias y Sistemas. (2026). **Semana 3 - Cableado Estructurado.** Unidad 1: Fundamentos e Infraestructura de las Redes.

5. Odom, W. (2019). **CCNA 200-301 Official Cert Guide, Volume 1.** Cisco Press.

6. Cisco Networking Academy. (2024). **Introduction to Networks.** Material de formación en fundamentos de redes.

7. Telecommunications Industry Association (TIA). **ANSI/TIA-606 - Administration Standard for Telecommunications Infrastructure.** Estándar utilizado como referencia para la administración e identificación de infraestructura de telecomunicaciones.

8. Siemon. (2022). **Catálogo de soluciones de cableado estructurado.** Material de referencia para componentes de infraestructura de telecomunicaciones.

9. Panduit. (2025). **Catálogo de infraestructura de redes.** Material de referencia para cableado, racks, canalización y elementos de terminación.

10. Kemik Guatemala. (2026). **Catálogo comercial de equipos y materiales de red.** Consultado como referencia para la estimación de precios de switches, cableado, UPS y accesorios.

---

**Nota:** Los precios incluidos en el presupuesto corresponden a valores de referencia y pueden variar según disponibilidad, marca, proveedor y fecha de adquisición.