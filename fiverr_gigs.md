# Plan de gigs para Fiverr

Notas de planificación para un perfil freelancer en Fiverr, complementario al
CV. Basado en el perfil actual: backend senior (Java/Quarkus), 2× CTO,
orientación a arquitectura de software.

## Perfil de Fiverr — About (máx. 600 caracteres)

No reutilizar el summary del CV tal cual (está escrito para reclutadores, en
tono de búsqueda de empleo). Versión reescrita para hablarle directo al
comprador de un gig:

> Hi, I'm Sergio — a software engineer with 9+ years building backend
> systems and APIs in Java, and CTO for two startups, defining their tech
> stack and cloud infrastructure from scratch. I've worked across banking,
> railways, and telecom, building software that's reliable and built to
> last.
>
> On Fiverr I offer custom-coded websites (no WordPress, deployed on
> Firebase for near-zero hosting costs) and backend/architecture
> consulting for teams needing a senior technical opinion.
>
> Fluent in English and Spanish. Clear, honest communication — no
> surprises, no over-promising.

## Orden de lanzamiento sugerido

1. Páginas web custom (Firebase) — mercado amplio, entregable visual, ciclo de venta corto, genera reviews rápido.
2. Code review / audit backend — alta percepción de valor, bajo riesgo para el comprador.
3. Consulting / diseño de arquitectura — requiere reputación previa en la plataforma para justificar el precio.

---

## Gig 1: Páginas web custom sobre Firebase

**Gig Title:** "I will create a fast custom website with Firebase hosting, not WordPress"

**Category:** Programming & Tech
**Subcategory:** Website Development
**Service Type:** Custom Websites
**Website Type:** Business
**Programming Language:** JavaScript, TypeScript, HTML/CSS, React
**Website Features:** Landing Page, Form, Analytics, Gallery, FAQ, Admin Panel, User Authentication
**Search Tags:** custom website, firebase hosting, react website, build website, business website

**Pitch:** sitios 100% customizables (sin WordPress), desplegados en Firebase
Hosting para minimizar costes de desarrollo y despliegue.

**Stack:**

| Capa | Elección | Por qué |
|---|---|---|
| Frontend | Next.js (static export) o Astro | Genera HTML estático, Firebase Hosting lo sirve desde CDN global |
| Formularios / datos simples | Firestore o Firebase Realtime DB | Sin servidor propio |
| Auth (si se necesita) | Firebase Auth | Ya conocido de Anka Innovations |
| Hosting | Firebase Hosting | Free tier cubre la mayoría de sitios pequeños; dominio custom gratis |
| CMS opcional | Sanity o Contentful (free tier) | Si el cliente quiere editar contenido sin tocar código |

**Niveles:**

- **Basic (~$150–250):** Landing page estática (1 página), diseño desde template acordado, Firebase Hosting configurado, dominio conectado.
- **Standard (~$350–600):** Sitio de 3–5 páginas + formulario de contacto (Firestore o Formspree) + Google Analytics.
- **Premium (~$700–1200):** Sitio completo + panel básico para que el cliente edite textos/imágenes (Sanity CMS).

**Paquetes (Fiverr):**

| | Basic | Standard | Premium |
|---|---|---|---|
| **Nombre** | Starter Landing Page | Business Website | Full Custom Website + CMS |
| **Descripción** | Custom coded single-page website, fully responsive, deployed on Firebase Hosting with your domain. | Custom 3-5 page website with contact form and Google Analytics, hosted on Firebase. | Full custom website with CMS admin panel, user authentication, and Firebase Hosting deployment. |
| **Precio** | $90 | $220 | $450 |
| **Number of Pages** | 1 | 5 | 10 |
| **Content Upload** | ✔ | ✔ | ✔ |
| **Delivery Time** | 3 días | 5 días | 10 días |
| **Revisions** | 1 | 2 | 3 |

*Precios de arranque (sin reviews aún). Subir gradualmente una vez alcanzadas
~10–15 reviews con buen rating (4–8 semanas de actividad estimadas).*

**Gig Extras:**

Activar:
- Additional page ($30 por página adicional)
- Additional revision ($15, +1 día de entrega)
- Opt-in form ($25, +1 día de entrega)
- Autoresponder integration ($40, +2 días de entrega)

No activar:
- Extra fast delivery — descartado a propósito, para no interrumpir las
  actividades regulares del freelancer.
- Additional plugin installation — no aplica, no se usan plugins de CMS de
  terceros.
- E-commerce functionality / Additional product — fuera de alcance del gig;
  un e-commerce real es un proyecto grande, mejor cotizarlo aparte como
  Custom Offer.
- Payment Integration — implica seguridad y cumplimiento (PCI) que no
  encajan en un extra de precio fijo; mejor como Custom Offer aparte.

**Gig Description:**

> Tired of clunky WordPress themes and slow, bloated websites? I build
> 100% custom-coded websites using React, deployed on Firebase Hosting —
> Google's global CDN infrastructure. That means fast load times, solid
> security, and near-zero hosting costs for you, since you own your own
> free-tier Firebase account.
>
> As a senior backend developer and former CTO, I bring real engineering
> discipline to every project: clean code, responsive design, and a site
> built exactly to your needs — no page builders, no plugin bloat, no
> monthly subscription fees.
>
> What you get:
> - Fully custom, hand-coded website (not a template)
> - Fast, secure hosting on Firebase (Google Cloud infrastructure)
> - Responsive design for mobile and desktop
> - Source code delivered to you
> - Clear communication and realistic timelines
> - Available in English and Spanish — website content and client
>   communication, your choice
>
> Perfect for small businesses, professionals, and startups who want a
> fast, modern, low-maintenance website without ongoing platform fees.
>
> Message me before ordering if you have specific requirements!

**FAQ:**

- **Do I need my own Firebase account?** Yes, you'll create a free
  Firebase account (takes 5 minutes) and I'll handle all the technical
  setup. You stay the owner of your website, domain, and data.
- **Will hosting cost me anything?** Firebase's free tier (Spark plan)
  covers most small business websites. You'd only pay if your traffic
  grows far beyond typical usage.
- **Do I get the source code?** Yes, you receive the full source code
  once the project is delivered and paid.
- **Can you connect my custom domain?** Yes, connecting an existing
  domain is included in every package.
- **What if I need more pages or features later?** You can order
  Additional Page extras, or contact me for a custom quote for bigger
  features like e-commerce.

**Buyer Requirements (Your Questions):**

1. Do you already have a domain name, or do you need help purchasing one? (Required)
2. Do you already have a Google/Firebase account, or do you need guidance to create one? (Yes, I have one / No, I need help) (Required)
3. Do you have your content ready (text, logo, images), or should I use placeholder content initially? (Required)
4. Do you have any design references or existing branding (colors, logo, fonts)? (Optional)
5. How many pages do you need beyond the ones included in your chosen package? (Optional)

**Gig Gallery (pendiente de generar — hasta 3 imágenes, 1 video, 2 PDFs):**

No hay material todavía porque la trayectoria previa es backend/CTO, no
sitios web custom entregados a clientes. Plan para completarlo:

- **Imágenes (3):**
  1–2. Construir 1–2 sitios demo reales con el stack del gig (Next.js/Astro
     + Firebase Hosting), desplegados de verdad, y tomarles screenshots
     reales (no mockups). Doble uso: sirven también como proyecto de
     portfolio personal (tema pendiente en el CV).
  3. Un banner de marketing propio (Canva/Figma) con la propuesta de valor
     en texto: "Custom Websites · React · Firebase Hosting · No WordPress"
     + foto o logo.
- **Video (opcional):** screen-recording corto (30–60s, Loom/OBS) de un
  sitio demo funcionando (scroll, responsive en mobile, velocidad de
  carga), narrado en inglés.
- **PDFs (2):**
  1. One-pager de proceso: brief → desarrollo → revisión → entrega, qué
     incluye cada paquete.
  2. Mini case study de un sitio demo: problema ficticio del "cliente",
     solución, stack usado, resultado (ej. velocidad de carga).

Orden sugerido: primero 1 sitio demo real → 2 screenshots + 1 banner →
lanzar el gig con eso. Video y PDFs se pueden sumar después sin bloquear
el lanzamiento.



**Add-on recomendado:** mantenimiento mensual mínimo (actualizaciones, SSL
auto-renovado, monitoreo). Firebase lo automatiza casi todo, así que el margen
es alto.

**Transparencia y propiedad de la cuenta:**

- No hace falta explicar Firebase en detalle técnico en el pitch de venta;
  alcanza con hablar en términos de beneficio ("hosting en infraestructura
  de Google, carga rápida global, costos mínimos"). Pero sí conviene dejarlo
  explícito en el brief/entregable, para transparencia y evitar reclamos
  futuros.
- **La cuenta de Firebase debe crearla y ser propiedad del cliente**, no del
  freelancer. El freelancer se agrega como colaborador/editor del proyecto.
  Motivos:
  - El cliente queda como dueño real del proyecto, dominio, datos y
    facturación; evita disputas de propiedad al terminar el contrato.
  - Protege legalmente al freelancer (no queda como "responsable de datos"
    de terceros si el sitio tiene formularios/usuarios).
  - Facilita el offboarding: al terminar el contrato simplemente se remueve
    el acceso del freelancer, sin que el cliente pierda nada.
- **Ventaja comercial directa:** al ser la cuenta del cliente, mientras el
  sitio se mantenga dentro del free tier de Firebase (plan Spark), el
  cliente no paga hosting. El freelancer cobra únicamente por el desarrollo
  inicial y por mantenimientos ocasionales, no por hosting recurrente. Esto
  es un diferenciador de venta fuerte frente a competidores que revenden
  hosting con margen.

**Entrega de código fuente:**

- Para webs simples se entrega el código fuente completo al cliente al
  finalizar y cobrar. Si más adelante necesita mantenimiento, se puede
  volver a pedir el código en ese momento (no hace falta retenerlo para
  garantizar el mantenimiento recurrente).
- No se usa un template propio: cada sitio se construye con ayuda de IA,
  usando webs anteriores como guía/referencia de estructura y estilo.
- Aclarar en el contrato/brief inicial dos puntos con el cliente:
  1. Permiso para usar capturas de pantalla del sitio (no el sitio en vivo)
     como muestra de portfolio.
  2. El freelancer se reserva el derecho de quedarse con una copia del
     código fuente para referencia propia.

---

## Gig 2: Code review / audit de backend

**Pitch:** auditoría escrita de un código base Java/Spring/Quarkus, con
hallazgos y recomendaciones concretas.

**Ejemplos de entregable:**

- Revisión de código base Java/Spring/Quarkus con reporte escrito.
- Configuración de pipeline CI/CD para un microservicio Java en AWS/GCP.
- Integración de un message broker (Kafka u otro) en un servicio existente.

---

## Gig 3: Consulting / diseño de arquitectura

**Pitch:** no ofertar como "arquitecto" (título que no se busca en Fiverr),
sino en términos del dolor del comprador.

**Ejemplos de entregable:**

- *"I'll design the backend architecture for your startup"* → diagrama de componentes + decisiones de diseño documentadas.
- Sesión de consultoría técnica (60/90 min por videollamada) con notas escritas posteriores.
- *"I'll help you choose the right tech stack for your product"*.
