# Conjunto Residencial — Plataforma Web

> Plataforma web integral para la gestión y comunicación de un conjunto residencial. Diseñada para centralizar información administrativa, documentación oficial, directorio de personal y sistema de peticiones para residentes.

---

## Problema / Objetivo

Un conjunto residencial carecía de una plataforma digital unificada. La información administrativa, los comunicados, la documentación oficial y las peticiones de los residentes se manejaban de forma fragmentada, generando confusión y demora en la respuesta.

**Objetivo:** Crear una aplicación web accesible, responsiva y fácil de usar que sirviera como punto central de información y gestión para propietarios, arrendatarios y administración.

---

## Funcionalidades Principales

### Cartelera Digital
- Comunicados semanales de administración
- Anuncios de aseo y zonas comunes
- Información relevante para residentes
- Navegación por secciones con menú colapsable

### Documentación Oficial
- Acceso a documentos del conjunto (reglamentos, actas, acuerdos)
- Sección de asambleas con archivos descargables
- Organización por categorías para fácil consulta

### Directorio de Personal
- Información de contacto del equipo administrativo
- Personal de seguridad y vigilancia
- Comité de convivencia
- Revisor fiscal

### Sistema de Peticiones (PQR)
- Formulario completo de Peticiones, Quejas y Reclamos
- Validación de campos obligatorios en cliente y servidor
- Integración con **Google reCAPTCHA** para prevenir spam
- Envío de correos electrónicos vía **PHPMailer**
- Sistema de radicación con código único de seguimiento
- Soporte para carga de archivos adjuntos

### Extras
- **Google Maps** integrado con ubicación del conjunto
- Botón flotante de **WhatsApp** para contacto directo
- Widget de horarios de atención con ventana modal
- Diseño 100% responsivo (mobile, tablet, desktop)
- Optimización SEO completa (meta tags, Open Graph, Schema.org)
- Lazy loading de imágenes para mejor rendimiento
- Efecto de scroll suave optimizado con `requestAnimationFrame`

---

## Arquitectura

```
Conjunto/
├── index.html                    ← Página principal (home)
├── style.css                     ← Estilos principales
├── reponsive.css                 ← Media queries responsivas
├── java.js                       ← Lógica principal (scroll, lazy loading, modal, WhatsApp)
├── favicon.ico
│
├── 1_Cartelera/                  ← Sección de comunicados
│   ├── Cartelera.html
│   ├── styles.css
│   ├── reponsive.css
│   ├── java1.js
│   └── Informacion/              ← Archivos de comunicados
│
├── 2_Documentacion/              ← Sección de documentación oficial
│   ├── Documentacion.html
│   ├── style.css
│   ├── reponsive.css
│   ├── java2.js
│   └── Documentos/               ← PDF y documentos del conjunto
│
├── 3_Personal/                   ← Directorio de personal de Administración, Consejo de Administración y Convivencia
│   ├── Personal.html
│   ├── style.css
│   ├── reponsive.css
│   ├── java3.js
│   └── *.pdf, *.avif             
│
├── 4_Reportes/                   ← Sistema de PQR
│   ├── Reportes.php              ← Formulario PQR
│   ├── enviar.php                ← Backend de envío de correos
│   ├── styles.css
│   ├── reponsive.css
│   ├── java4.js
│   ├── .htaccess                 ← Reglas de seguridad Apache
│   └── PHPMailer/                ← Librería de envío de correos
│
└── assets/                       ← Imágenes y medios
    ├── 1Logoconjunto.avif
    ├── LogoConsejoAd.avif
    ├── LogoConvi.avif
    ├── logo.png
    ├── vistaConjunto.avif
    ├── Horarios.jpg
    └── torremovil.avif
```

---

## Stack Tecnológico

| Capa | Tecnología |
|------|-----------|
| **Frontend** | HTML5, CSS3, JavaScript (vanilla) |
| **Backend** | PHP 7.4+ |
| **Diseño responsivo** | CSS Media Queries (mobile-first) |
| **Tipografía** | Google Fonts — Lato |
| **Formularios** | Bootstrap 5.3 (solo en PQR) |
| **Seguridad** | Google reCAPTCHA v2, .htaccess |
| **Email** | PHPMailer |
| **Mapas** | Google Maps Embedded API |
| **Imágenes** | Formato AVIF (compresión moderna) |
| **SEO** | Meta tags, Open Graph, Schema.org (JSON-LD) |

---

## Decisiones Técnicas

### Por qué vanilla JS y no un framework
El proyecto era un sitio informativo con interacciones limitadas (modales, scroll, lazy loading). Usar React o Vue habría añadido complejidad innecesaria y peso al bundle sin beneficio real para el usuario final.

### Por qué PHP para el backend
El requisito era un formulario que enviara correos electrónicos a la administración. PHP es el estándar para este tipo de integraciones en hosting compartido, y PHPMailer resuelve el envío de forma robusta sin dependencias externas complejas.

### Formato AVIF para imágenes
Se eligió AVIF por su excelente compresión (hasta 50% menor que JPEG con misma calidad). Los navegadores modernos lo soportan nativamente, y se implementó fallback para navegadores antiguos.

### SEO completo desde el inicio
Se implementaron meta tags descriptivos, Open Graph para compartir en redes sociales, y Schema.org en JSON-LD para que los buscadores entiendan la estructura del contenido. Esto es crítico para un sitio de conjunto residencial que los residentes deben encontrar fácilmente.

---

## Retos y Aprendizajes

1. **PQR con validación dual** — La validación del formulario se hizo tanto en cliente (JavaScript) como en servidor (PHP) para seguridad. El reCAPTCHA previene abusos sin complicar la experiencia del usuario.

2. **Sistema de radicación automático** — Cada petición recibe un código único de seguimiento. Simple pero efectivo para el volumen de un conjunto residencial.

3. **Imágenes de personal sin exponer datos** — Las fotos del personal se comprimieron en AVIF y se organizaron por categoría, manteniendo calidad visual con tamaño mínimo.

4. **Hosting compartido** — El proyecto fue desplegado en hosting convencional con soporte PHP. Se usó `.htaccess` para headers de seguridad y reescritura de URLs.

---

## Resultado

- **Plataforma activa** durante el periodo de contrato con el conjunto residencial
- **Centralización de información** que antes estaba dispersa en documentos físicos y grupos de WhatsApp
- **Sistema de PQR** que permitió a los residentes radicar peticiones de forma ordenada y con seguimiento
- **Acceso mobile** optimizado para que los residentes consultaran información desde su celular (uso principal)
- **Documentación digital** que eliminó la necesidad de imprimir y distribuir documentos físicos

---

## Estado del Proyecto

> **Inactivo** — El conjunto residencial decidió no renovar el dominio ni el hosting. El proyecto fue entregado y funcionó correctamente durante su periodo de operación.

---

## Autor

**Edwin Alexander Medina Martínez**
🔗 [GitHub](https://github.com/Alexmedina-Dev)  
📧 alexandermedi53h@gmail.com
- Desarrollo completo: Frontend + Backend + Diseño + Deploy
- Año: 2024

---

## Licencia

Proyecto privado — Desarrollado como encargo para un conjunto residencial en Colombia.
