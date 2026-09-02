# 🏍️ MotoVerso — Sistema de Gestión para Taller de Motos

**Sistema web completo** para la gestión integral de un taller de motos: clientes, vehículos, órdenes de servicio, inventario de repuestos, mano de obra y cierres diarios con respaldo automatizado.

---

## 🎯 Propósito del Proyecto

Transformar la operación de un taller mecánico que funcionaba con **Excel y Google Sheets manuales** en un sistema digital robusto, multiusuario y en tiempo real. El objetivo fue eliminar errores de duplicación de datos, agilizar el registro de servicios y generar reportes de cierre diario de forma automática.

---

## 🏗️ Arquitectura del Sistema

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│   Cliente   │────▶│   Backend    │────▶│  MySQL (Cloud)  │
│  (Vanilla)  │     │  (Node.js)   │     │  Producción     │
└─────────────┘     └──────────────┘     └─────────────────┘
                            │
                            ▼
                   ┌──────────────────┐
                   │  Google Sheets   │  (respaldo + reportes)
                   └──────────────────┘
```

**Frontend:** HTML5 + CSS3 + JavaScript vanilla (SPA sin frameworks)  
**Backend:** Node.js + Express + MySQL (mysql2/promise)  
**Autenticación:** JWT con control de roles  
**Validación:** Joi en formularios  
**Integraciones:** Google Sheets API v4 (respaldo async)  
**Infraestructura:** Hosting cloud con timezone handling (Colombia vs UTC+2)

---

## ⚙️ Funcionalidades Clave

| Módulo | Qué hace |
|---|---|
| **Órdenes de Servicio** | Creación, edición y cierre de órdenes con placa, técnico asignado, diagnóstico, repuestos y mano de obra |
| **Gestión de Clientes** | CRUD de clientes con cédula, nombre, teléfono y correo; vinculación automática con vehículos |
| **Vehículos** | Registro por placa, modelo, kilometraje; historial de servicios vinculado |
| **Repuestos y MO** | Detalle de ítems por servicio con cantidad, precio unitario, subtotal y gran total auto-calculado |
| **Cierres Diarios** | Generación de cierre por técnico y fecha con PIN de seguridad; suma automática de mano de obra |
| **Panel de Errores** | Dashboard en vivo con logs de errores del frontend y backend filtrables por severidad |
| **Sync Google Sheets** | Respaldo automático de servicios y cierres en Sheets como backup operativo |
| **Roles y Permisos** | `admin`, `developer`, `mecanico`, `operador` — cada rol ve y puede hacer cosas distintas |

---

## 🧠 Decisiones Técnicas Destacadas

### Migración de datos masiva
- Migré **1,949 clientes, 1,880 vehículos, 3,277 servicios, 10,997 detalles y 600 cierres** desde Excel a MySQL en producción sin downtime.
- Generé IDs únicos (`SRV-<timestamp>`) y resolví duplicados de placas (ej: `QRH72E → QHR72E`).

### Manejo de timezone
- El servidor está en **UTC+2 (Alemania)** y los usuarios en **Colombia (UTC-5)**.
- Implementé lógica explícita de conversión a `America/Bogota` en todas las fechas para evitar que los cierres diarios queden en el día equivocado.

### Google Sheets como capa de backup
- Diseñé una cola de sincronización (`sheets-queue.js`) que envía cambios a Sheets de forma asíncrona, sin bloquear la respuesta al usuario.
- El sistema sigue funcionando aunque la API de Google falle temporalmente.

### Seguridad
- JWT con expiración controlada y roles diferenciados.
- PIN de 4 dígitos para cierres diarios (protección contra cierres accidentales).
- Sanitización de inputs vía Joi en todos los endpoints de escritura.

---

## 🛠️ Stack Tecnológico

| Capa | Tecnología |
|---|---|
| Frontend | HTML5, CSS3, JavaScript vanilla |
| Backend | Node.js, Express |
| Base de datos | MySQL (mysql2/promise) |
| Autenticación | JWT |
| Validación | Joi |
| Integración | Google Sheets API v4 |
| Deployment | Cloud hosting (PaaS) |

---

## 📊 Impacto del Proyecto

- **Tiempo de registro de servicio:** reducido de ~5 min en Excel a <1 min en la app.
- **Errores de duplicación de clientes:** eliminados con validación de cédula y placa en tiempo real.
- **Generación de cierres diarios:** automatizada (antes era manual celda por celda en Sheets).
- **Visibilidad de errores:** antes los errores del frontend se perdían en la consola del navegador; ahora se centralizan en un panel en vivo.

---

## 🚧 Desafíos Resueltos

| Problema | Solución |
|---|---|
| Placa con cédula falsa en vehículo existente | Permití edición de datos del cliente al corregir una orden abierta, manteniendo la guarda de doble orden abierta |
| Cierres diarios fallaban sin mensaje claro | Corregí el frontend para mostrar el error real del backend (409/401/400) en vez de un genérico |
| Formulario de nueva orden no se limpiaba | Implementé `limpiarFormulario()` con manejo explícito de `undefined` vs `null` vs `""` |
| Duplicación de servicios por doble click | Agregué bloqueo de botón mientras se procesa la petición |

---


## 👤 Autor

**Edwin Alexander Medina Martinez** — Fullstack Developer en construcción 
🔗 [GitHub](https://github.com/Alexmedina-Dev)  
📧 alexandermedi53h@gmail.com

---

