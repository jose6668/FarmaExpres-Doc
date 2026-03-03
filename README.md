# FarmaExpres-Doc

## Problematica de la Farmacéutica

Actualmente no contamos con un sistema confiable para controlar el inventario de medicamentos. Esto provoca que no tengamos claridad en el stock real, que puedan generarse errores cuando varias personas trabajan al mismo tiempo y que exista el riesgo de vender productos vencidos.

Además, no tenemos un registro seguro y detallado de quién realiza cada movimiento, lo que dificulta detectar y corregir errores. Tampoco hay un control sólido de accesos, lo que pone en riesgo la información.


## Presentacion de Solucion por RF
Proyecto: FarmaExpres  
Sistema de Gestión de Inventario Farmacéutico

Este documento define los requerimientos funcionales y no funcionales de la **Versión 1.0 (MVP)** del sistema FarmaExpres.<br>
La priorización se realiza con base en las necesidades del negocio, requerimientos funcionales (RF) y no funcionales (RNF).

El objetivo es establecer una base operativa mínima que garantice:

- Control de inventario
- Seguridad
- Trazabilidad
- Operación multiusuario estable

---

## 1 Alcance 

La versión 1.0 incluye: 

- Aplicación web
- Gestión de usuarios y control de acceso
- Registro y control de medicamentos
- Gestión de entradas y salidas
- Historial inmutable de movimientos
- Alertas de vencimiento
- Soporte multiusuario con control de concurrencia
- Reportes básicos operativos

No se incluyen:

- Integraciones externas
- Arquitectura distribuida avanzada
- Aplicación móvil
- Inteligencia predictiva

---

# 2. Descripción General del Sistema

FarmaExpres es un sistema web orientado a la gestión de inventario farmacéutico que permite:

- Controlar medicamentos y fecha de vencimiento
- Gestionar movimientos de entrada y salida
- Evitar inconsistencias por concurrencia
- Mantener trazabilidad completa de operaciones
- Garantizar seguridad de la información

---

# 3. Requerimientos Funcionales (RF)

---

## 3.1 Seguridad y Gestión de Usuarios

- **RF-01** Registro de usuarios con asignación de roles.
- **RF-02** Autenticación mediante credenciales únicas.
- **RF-03** Recuperación de contraseña.
- **RF-05** Registro en bitácora de accesos y acciones críticas.

---

## 3.2 Gestión de Inventario

- **RF-06** Registro de medicamentos con los siguientes campos obligatorios:
  - Código único
  - Nombre
  - Precio unitario
  - Fecha de vencimiento
  - Stock
  - Estado

- **RF-07** Actualización de información de medicamentos.
- **RF-08** Eliminación lógica de medicamentos.
- **RF-09** Generación de alertas configurables de vencimiento y bloqueo automático de productos vencidos.
- **RF-10** Consulta de inventario en tiempo real.

---

## 3.3 Movimientos de Inventario

- **RF-11** Registro de entradas de inventario.
- **RF-12** Registro de salidas con descuento automático de stock.
- **RF-13** Historial completo e inmutable de movimientos.

---

## 3.4 Concurrencia

- **RF-16** Soporte de acceso concurrente multiusuario.
- **RF-17** Actualización de cambios en otros clientes en tiempo real (≤ 15 segundos).

---

## 3.5 Reportes Básicos

- **RF-14** Reporte de inventario actual.
- **RF-15** Reporte de productos próximos a vencer.
- **RF-18** Reporte de productos agotados.
- **RF-19** Reporte de historial de movimientos.

---

# 4. Requerimientos No Funcionales (RNF)

---

## 4.1 Seguridad

- **RNF-15** Comunicación segura mediante HTTPS.
- **RNF-16** Control de acceso basado en roles.
- **RNF-31** Almacenamiento cifrado de contraseñas.
- **RNF-32** Validación obligatoria de campos.

---

## 4.2 Integridad y Consistencia

- **RNF-06** Prevención de stock negativo.
- **RNF-12** Prevención de duplicidad de código.
- **RNF-11** Atomicidad en transacciones (todo o nada).
- **RNF-13** Rollback automático ante error.
- **RNF-29** Sincronización automática con fecha y hora del servidor.

---

## 4.3 Concurrencia

- **RNF-05** Prevención de inconsistencias por acceso simultáneo.
- **RNF-07** Manejo de conflictos de edición.
- **RNF-30** Límite configurable de sesiones activas.

---

# 5. Criterios de Aceptación

---

## 5.1 RF-02 – Autenticación

- Permite acceso únicamente con credenciales válidas.

---

## 5.2 RF-06 – Registro de Medicamentos

- No permite campos obligatorios vacíos.
- No permite códigos duplicados.
- Persiste correctamente en base de datos.

---

## 5.3 RF-09 – Alertas de Vencimiento

- Genera alerta configurable (15 días antes).
- Bloquea automáticamente productos vencidos.
- Impide su uso en movimientos posteriores.

---

## 5.4 RF-12 – Salidas de Inventario

- Reduce automáticamente el stock al confirmar la salida.
- No permite stock negativo.
- Registra usuario, fecha y tipo de movimiento.

---

## 5.5 RF-13 – Historial

- Registra usuario, fecha/hora y tipo.
- No permite modificación posterior.

---

## 5.6 Concurrencia (RF-16 / RF-17)

- No permite inconsistencias simultáneas.
- Refleja cambios en otros clientes ≤ 15 segundos.
- Aplica transacciones completas o rollback ante error.

---

# 6. Matriz de Trazabilidad

| Necesidad del Negocio | RF | RNF |
|------------------------|----|-----|
| Control de inventario | RF-06, RF-10, RF-14 | RNF-06, RNF-12 |
| Gestión operativa | RF-11, RF-12 | RNF-11, RNF-13 |
| Control por lote y vencimiento | RF-06, RF-09 | RNF-06 |
| Concurrencia segura | RF-16, RF-17 | RNF-05, RNF-07 |
| Seguridad y acceso | RF-01, RF-02 | RNF-15, RNF-16, RNF-31 |
| Trazabilidad | RF-05, RF-13 | RNF-29 |

---

# 7. Definición Formal de la MVP

La Versión 1.0 garantiza:

- Control total del inventario farmacéutico.
- Prevención de errores críticos (duplicados y stock negativo).
- Seguridad en autenticación y control de acceso.
- Registro inmutable de movimientos.
- Alertas automáticas de vencimiento.

---

## MoSCoW
[📄 Ver Requerimientos MoSCoW (PDF)](./FarmaExpres_Requerimientos_MoSCoW_v1.0_actualizado.pdf)


### Diagramas 

[Git Diagraams)(https://github.com/jose6668/FarmaExpres-Diagramas.git)

###  Estructura Monorepo

```text
farmaexpres/
├── README.md
├── docker-compose.yml
|
│
├── gateway/                      # API Gateway
│   ├── src/
│   ├── pom.xml
│   └── Dockerfile
│
├── auth-service/                 # Microservicio - Autenticación
│   ├── src/
│   │   └── main/
│   │       ├── java/
│   │       └── resources/
│   │           └── application.yml
│   ├── pom.xml
│   └── Dockerfile
│
├── inventory-service/
│   ├── src/
│   │   └── main/
│   │       ├── java/
│   │       └── resources/
│   │           └── application.yml
│   ├── pom.xml
│   └── Dockerfile
│
└── database/
    └── init.sql

```

### 📌 Historias de Usuario (RF)

Las siguientes Historias de Usuario han sido creadas y gestionadas como Issues dentro del repositorio:

- HU-RF-01 – Gestión de Usuarios  
- HU-RF-02 – Autenticación 
- HU-RF-03 – Cambio de Contraseña  
- HU-RF-04 – Registro de Medicamentos  
- HU-RF-05 – Actualización de Medicamento 
- HU-RF-06 – Eliminación Lógica de Medicamento  
- HU-RF-07 – Registro de Salida de Inventario
- HU-RF-08 – Alertas de Vencimiento
- HU-RF-09 – Reporte de Inventario Actual
- HU-RF-09 – Reporte de Inventario Actual
- HU-RF-10 - Reporte de Productos Agotados
- HU-RF-11 - Reporte de Historial de Movimientos 

[Ver HU](https://github.com/JerssonF/Week-4.git)


### HU-RF-01 – Gestión de Usuarios

[Ver HU-RF-01 – Gestión de Usuarios](./HU-RF-01–Gestión_de_Usuarios.docx)

### HU-RF-02 – Autenticación
[Ver HU-RF-02 – Autenticación](./HU-RF-02–Autenticación.docx)

### HU-RF-03 – Cambio de Contraseña

[ver HU-RF-03 – Cambio de Contraseña](./HU-RF-03–Cambio_de_Contraseña%20.docx)

