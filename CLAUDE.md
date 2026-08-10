# Acuerdos para la edición del CV

Este documento captura las decisiones tomadas durante la revisión y mejora del CV.

## Archivos del repo
Hay dos versiones del CV en dos idiomas (4 archivos HTML + 1 CSS compartido):

| Archivo | Idioma | Versión | Propósito |
|---|---|---|---|
| `CV_SR_detailed_es.html` | ES | Detallada | Source of truth de la historia profesional completa. Sirve también como contexto para que un LLM genere variantes cortas u orientadas a otros roles. NO se envía como PDF a postulaciones por defecto (queda en ~5 páginas). |
| `CV_SR_detailed_en.html` | EN | Detallada | Equivalente en inglés del anterior. |
| `docs/CV_es.html` | ES | Compacta (pública) | **Versión a postular** para roles senior dev → arquitecto. Objetivo: 2 páginas. Derivada de la detallada. Es la única copia de la versión corta ES (ya no existe `CV_SR_short_es.html` en el root, ver sección "Estructura del repo y GitHub Pages"). |
| `docs/CV_en.html` | EN | Compacta (pública) | Equivalente en inglés del anterior. |
| `CV_SR.css` | — | — | Estilo compartido por todas las versiones. Cambios visuales (sidebar width, justificado, etc.) aplican a todas simultáneamente. Duplicado en `docs/CV_SR.css` (ver abajo). |
| `profile_pic.jpeg` | — | — | Foto referenciada por todos los HTML. Duplicada en `docs/profile_pic.jpeg` (ver abajo). |

Los cambios se aplican en **ambos idiomas** simultáneamente. Cuando el cambio es de
contenido editorial, se aplica primero en la versión detallada; la compacta se
regenera/ajusta a partir de ahí.

## Estructura del repo y GitHub Pages

El repo publica CVs vía **GitHub Pages** desde la carpeta `docs/`. Esto impone una
separación estricta entre dónde vive cada tipo de archivo:

- **`docs/`** contiene **solo** la versión corta/pública lista para compartir o
  descargar como PDF desde el navegador: `docs/CV_es.html`, `docs/CV_en.html`
  (nombres fijos, sin sufijo `short`). Estos archivos **no tienen equivalente en
  el root** — no existen `CV_SR_short_es.html` / `CV_SR_short_en.html` en el
  root; si hay que editar la versión corta, se edita directamente en `docs/`.
- **El root** del repo contiene las versiones **detalladas** (`CV_SR_detailed_es.html`,
  `CV_SR_detailed_en.html`) y cualquier **versión alternativa** orientada a una
  postulación específica (ej. `CV_SR_hearthsim_en.html`,
  `CV_SR_hearthsim_short_en.html`). Estas nunca se mueven a `docs/`.
- **Assets (`CV_SR.css`, `profile_pic.jpeg`) van siempre duplicados**: una copia
  en el root (usada por las versiones detalladas/alternativas) y otra igual en
  `docs/` (usada por la versión pública). Cualquier cambio visual en el CSS o
  cambio de foto se replica manualmente en ambas copias.
- **Todas las referencias a `CV_SR.css` y `profile_pic.jpeg`, en todos los HTML
  (root y `docs/`), usan el prefijo `./`** (`./CV_SR.css`, `./profile_pic.jpeg`).
  Es necesario por cómo GitHub Pages resuelve rutas relativas, y se mantiene
  igual en el root por consistencia.

## Objetivo del CV
Reposicionar el perfil de **"Desarrollador Backend"** a un perfil orientado a
**roles de diseño de arquitectura** (Software Architect / Backend Architect /
Tech Lead con foco arquitectónico), sin inflar responsabilidades pasadas.

## Proceso de trabajo
- Revisamos el CV **por secciones**, una a la vez. Orden actual:
  1. Experiencia laboral (completo).
  2. Resumen / summary (completo).
  3. Aptitudes principales (sidebar) (completo).
  4. Aptitudes detalladas (completo).
  5. Certificaciones, idiomas, voluntariado, formación (completo).
  6. Contacto y metadatos del HTML (completo).
- Para cada trabajo: el usuario narra libremente lo que hizo, el asistente
  pregunta los huecos relevantes, se redacta una propuesta, se aprueba y
  recién ahí se aplica al HTML.
- Los cambios se aplican simultáneamente en **ambos idiomas** (ES/EN) en
  cuanto se aprueban.

## Reglas de redacción de bullets
- Diferenciar claramente **diseñé** vs **co-implementé bajo guía** vs
  **implementé**. Esto es crítico para roles de arquitectura: muestra
  criterio sin inflar el rol.
- Resaltar **decisiones de diseño**, **documentos de arquitectura/ADRs**,
  **participación en reuniones de diseño** y **mentoría con arquitectos**.
- Verbos preferidos: diseñé, lideré, definí, evalué, propuse, co-diseñé,
  establecí, refiné. Evitar abusar de "desarrollé" / "implementé".
- Cada trabajo termina con una línea compacta `Stack: ...` (no bullets
  sueltos por tecnología).
- Incluir un párrafo introductorio breve por puesto que dé contexto del
  producto y del equipo (tamaño, composición, posición del usuario en él).
- Sin métricas inventadas. Si no hay datos confiables, se omiten.

## Decisiones de formato y estética

### Subtítulo de cada empleo (`p.job-company`)
Formato: `Empresa - Ciudad, País · Modalidad · Idioma`. La modalidad
(Remoto/Presencial · Remote/On-site) y el idioma de trabajo
(Español/Inglés · Spanish/English) van **en el subtítulo** y NO se repiten
en la descripción del puesto. Esto evita redundancia y aligera la lectura.

### Justificado de texto
Los párrafos descriptivos y los bullets dentro de `.job` están justificados
(`text-align: justify` en `.job p` y `.job ul li`, definido en `CV_SR.css`).

### Formato de cabecera para empleos en consultora
Cuando el empleador es una consultora y el trabajo real fue para un cliente
final, el primer párrafo del puesto sigue el patrón establecido en Aditi y
se replica en Globant y P&T:

```
Cliente: <link>NombreCliente</link> (País) — <descriptor breve> (MM/AAAA – MM/AAAA).
```

Si hay un proyecto/producto identificable separado del cliente, se incluye
también enlazado (ej. Aditi → Wabtec + PDS 2.0). Aditi además mantiene un
formato de "lista de clientes" porque se esperan más asignaciones (bench).
El segundo párrafo describe equipo, sistema y contexto.

## Sección de Aptitudes (skills)

### Aptitudes Principales (sidebar)
Subset corto (5–7 ítems) y diferenciador alineado al objetivo
(arquitectura backend Java). Mezcla lenguaje + frameworks + arquitectura +
infra. Evita ítems genéricos (Docker se omite si está Kubernetes).

### Aptitudes detalladas — bloques
Bloques actuales (en este orden):
1. **Lenguajes de programación** — cada lenguaje lleva minidescripción en
   `<em>` indicando peso real (principal / secundario / formación / complementario).
2. **Frameworks y plataformas backend**.
3. **Arquitectura y diseño** — incluye keywords reconocibles (CQRS,
   hexagonal, event-driven). Cuando el conocimiento no es total se aclara
   entre paréntesis en `<em>` (ej. *experiencia en sistema diseñado bajo
   este enfoque*, *adoptada y replicada en producción*).
4. **Bases de datos** — separadas en *Relacionales* y *No relacionales*.
5. **Cloud y despliegue** — un bullet por proveedor, diferenciando
   `(uso directo)` vs `(exposición)`. Incluye CI/CD aquí.
6. **Testing** — bloque propio.
7. **Otras herramientas** — cajón final para piezas pequeñas y heterogéneas
   que no caben en las categorías anteriores.

### Reglas para skills
- **Honestidad sobre profundidad**: usar `(uso directo)` / `(exposición)` /
  `(nivel introductorio)` / `(en adopción)` cuando aplique. No inflar.
- **Soft skills NO van** en la sección de aptitudes (que es hard skills).
  Cosas como "documentación de decisiones técnicas" se quedan implícitas en
  el summary y en los bullets de experiencia.
- **Omitir tecnologías irrelevantes al objetivo** aunque se hayan tocado
  (ej. Unity → fuera).
- **Spring Data**: se omite porque el usuario lo conoce pero no lo usó en
  proyectos reales.

## Sidebar: Certificaciones / Idiomas / Voluntariado

### Orden
Dentro del sidebar el orden es: Aptitudes principales → Aptitudes detalladas
→ **Idiomas** → **Certificaciones** → **Voluntariado**. Idiomas se sube
porque para roles internacionales pesa más que las certificaciones.

### Idiomas
Usar nivel CEFR + descriptor estándar (ej. *C1 / Profesional*) en lugar de
"Avanzado". Más legible para reclutadores internacionales.

### Certificaciones
- Solo certificaciones vigentes y relevantes al objetivo. Se descartó
  Platzi 2019 (desactualizada y nivel introductorio frente a perfil senior).
- PMI: nombre oficial completo *Diploma Internacional en Gerencia de
  Proyectos (PMBOK / PMI)*, emisor real *ILEN · Universidad Nacional de
  Ingeniería (UNI), Perú*, fecha *Noviembre 2022*, duración *130 horas*.
- Certificaciones en curso se incluyen marcadas como *En curso (AAAA)*
  cuando son relevantes al objetivo. Al completarse, se marca *Completado (AAAA)*
  aunque el certificado físico/digital esté pendiente de trámite de emisión
  (no se aclara el trámite en el CV, es detalle interno).
- **Certified AI/LLM Solution Architect** (BSG Institute, certificado por
  IEEE): completado en 2026. Nombre oficial del curso — usar tal cual, sin
  traducir, en ambos idiomas del CV.

### Voluntariado
Roles históricos. Se añade un `<p><em>Roles históricos.</em></p>` debajo
del `<h2>` para señalarlo sin tener que poner fechas exactas (no recordadas).
Se agregó **Madada** (profesor de fundamentos de programación en Java).

## Formación
Solo Bachiller (UNMSM, Ingeniería de Sistemas, 03/2012 – 06/2019). Se
añade nota *Tesis en desarrollo para titulación profesional* para señalar
que el bachiller no es el techo académico actual.

## Convención de títulos de puesto
Cuando el título oficial difiere del estándar reconocible para reclutadores
internacionales, usar el formato:

> **Título Oficial (Equivalente estándar)**

Ejemplo aplicado: *"Programador de Soluciones (Desarrollador Backend Junior)"*.

## Política de links a productos / clientes
- Agregar link **solo cuando aporta contexto** y el sitio es profesional y
  está vivo.
- Linkear al **producto o cliente final**, no a la consultora (la consultora
  ya aparece como employer).
- El usuario proporciona el link; el asistente no inventa URLs.
- Estilo: enlace en línea sobre el nombre del producto/cliente, usando la
  clase CSS existente `.link` para mantener consistencia visual.
- Aplicar el link **en ambos idiomas**.

### Links acordados hasta ahora
| Empresa / Cliente | Producto | URL |
|---|---|---|
| Ebiz Latin America | B2miningdata | https://ebiz.pe/soluciones/b2m/ |
| Anka Innovations | EDAN (proyecto) | https://portal.indeci.gob.pe/respuesta/edan/ |
| Anka Innovations | INDECI (cliente) | https://www.gob.pe/indeci |
| Globant | Lulo Bank | https://www.lulobank.com/ |
| Aditi Consulting | Wabtec (corporativo) | https://www.wabteccorp.com/ |
| Aditi Consulting | Wabtec PDS / cliente CN (nota de prensa) | https://www.wabteccorp.com/newsroom/press-releases/wabtec-advances-rail-network-optimization-for-cn-with-the-launch-of-its-precision-dispatch-system |

## Versiones de Java por puesto
Útil para la sección de skills y para mantener coherencia técnica en bullets.

| Puesto | Java |
|---|---|
| Ebiz Latin America | 1.8 |
| Target HR | 1.8 |
| Anka Innovations | 11 |
| Process & Technology Solutions | 1.8 |
| Globant / Lulo Bank | 17 |
| Aditi / Wabtec PDS 2.0 | 21 |

## Orden de las experiencias
Cronología estricta descendente por **fecha de inicio** (más reciente arriba).
Cuando dos puestos se solapan, manda la fecha de inicio. Decidido al detectar
que Anka (01/2019) y P&T (12/2019) terminaban ambos en 02/2020: P&T queda
arriba de Anka. La descripción de Anka aclara la naturaleza paralela del
rol (co-fundador/CTO).

## Anécdotas y contenido reservado para entrevista
Hay material valioso que no encaja como bullet de CV pero sí como historia
para entrevistas (por ejemplo, la reunión con Google ofreciendo migración
Azure → GCP en Ebiz). Estas se registran aquí para no perderlas, pero **no**
van al CV.

### Reservado
- **Ebiz / Google GCP**: ante la ausencia simultánea del arquitecto y su
  backup, el usuario acompañó al jefe de sistemas como interlocutor técnico
  en una reunión informal con representantes de Google que ofrecían facilitar
  una migración Azure → GCP. Buena historia de exposición temprana a
  decisiones de plataforma cloud.
- **Globant / Lulo Bank — bug XIRR (versión larga)**: el cálculo de TIR
  fallaba porque la librería usaba el método de Newton sobre `BigDecimal`,
  pero al necesitar exponentes fraccionarios caía en `Math.pow(double,double)`
  (porque `BigDecimal.pow` nativo solo acepta exponentes enteros). Con
  ciertos valores la aproximación oscilaba alrededor de la raíz sin nunca
  alcanzar la tolerancia decimal, agotando el límite del bucle y devolviendo
  un valor incorrecto. Solución: librería con potencia
  `BigDecimal`-a-`BigDecimal` + ajuste de precisión decimal. La versión
  corta de la anécdota sí entró al CV; los detalles del método de Newton y
  oscilación quedan para entrevista.
- **Globant / salida**: dejó Globant porque Aditi le ofreció algo mejor.
  Estándar omitir motivos de salida en el CV.

## Versión compacta (`docs/CV_es.html` / `docs/CV_en.html`)

Versión derivada de la detallada, optimizada para postular a roles **Senior
Backend Developer con miras a arquitecto** (2 páginas objetivo). Vive solo en
`docs/` (ver "Estructura del repo y GitHub Pages"). Reusa el mismo `CV_SR.css`
(la copia en `docs/`). Decisiones de poda específicas de la compacta:

### Header / summary
- Resumen acortado a ~5 líneas. Se elimina la enumeración explícita de
  dominios (banca/ferrocarriles/etc. se mantiene; *e-procurement* y
  detalles secundarios se condensan). Se conserva el posicionamiento de
  arquitectura y la mención CTO ×2.
- Se incorpora en `docs/CV_es.html` y `docs/CV_en.html` un bloque
  oculto (`.hidden_prompt`) redactado como párrafo narrativo neutral (no
  imperativo) y anclado a toda la trayectoria (dominios, progresión de
  rol, Java 8→21, cloud/on-prem, educación y gestión de proyectos). Este
  bloque **no se usa** en las versiones detalladas.

### Sidebar
- Orden ajustado: **Contacto → Aptitudes Principales → Idiomas →
  Certificaciones → Formación**. Formación baja al sidebar como bloque
  mínimo (título + universidad + años) para liberar espacio en el main.
- **Voluntariado: fuera** en la compacta. No aporta a roles senior técnicos
  y consume espacio. Se mantiene en la detallada.
- **Certificaciones**: cada una colapsada a una sola línea
  (`emisor · año` o `emisor · estado`). Sin duración en horas ni nombre
  académico extendido.
- **Formación**: se omite la nota de tesis para ahorrar línea.

### Experiencia
- **Puestos detallados: 5** (Origen 360, Aditi, Globant, Anka, Ebiz). Los
  dos puestos antiguos y cortos se colapsan en una sola línea final:
  > *Experiencia previa: Process & Technology Solutions (Entel, ...) y
  > Target HR (Intralot, UNICON, ...). Detalle disponible bajo solicitud.*
  Justificación: ambos son <5 meses, >6 años atrás, no aportan al
  posicionamiento senior/arquitecto y su detalle ya vive en la versión
  detallada.
- **Bullets por puesto: 3–4** (vs 5–7 en la detallada). Se priorizan los
  que muestran *diseñé / co-diseñé / lideré / definí*. Se fusionan o
  eliminan los de implementación pura, mantenimiento evolutivo y los
  contextos de equipo extensos.
- Se conservan los **párrafos introductorios** pero recortados (mismo
  patrón consultora→cliente; equipo descrito en una frase, no en dos).
- **Línea `Stack:`** se mantiene íntegra (es valor denso, no se recorta).
- **Anka**: se omite el bullet de la línea VR/Unity (irrelevante al
  objetivo). Firebase Auth y MapStruct se omiten como bullets propios pero
  se conservan en la línea Stack.
- **Globant**: el bullet de mantenimiento evolutivo y el bullet de
  Python se fusionan al de TIR/XIRR o se compactan.
- **Ebiz**: los microservicios de archivos y logs se fusionan en un
  bullet único; notificaciones (Twilio/SendGrid) y service evaluation se
  omiten por menor peso arquitectónico.

### Aptitudes
- Cada categoría se reduce a **1 línea agrupada** (CSV con `·` o coma),
  no listas verticales largas.
- Se quitan los matices de profundidad `(uso directo)` / `(exposición)` /
  `(nivel introductorio)` / `(en adopción)`. Se conservan solo los de
  lenguajes (`(principal)` / `(secundario)` / `(complementario)`) porque
  diferencian el perfil.
- **Bloque Testing**: fusionado al cajón "Otros".
- **JasperReports, Apache Tomcat**: omitidos en la compacta (no aportan al
  objetivo).
- Categorías finales: Lenguajes · Backend · Arquitectura y diseño · Bases
  de datos · Cloud y despliegue · Otros.

### Reglas para mantener sincronizadas detallada y compacta
- Los cambios **editoriales de fondo** (nuevo trabajo, cambio de título,
  reescritura de bullet clave) se aplican primero en la detallada y luego
  se reflejan en la compacta.
- Los cambios **de poda específicos de la compacta** (ej. quitar un
  bullet) NO se replican hacia la detallada.
- Los cambios de **links / datos de contacto / metadatos** se aplican en
  los 4 archivos a la vez.

## Estado del progreso (experiencia laboral)
- [x] **Ebiz Latin America** (06/2017 – 09/2018) — aplicado en ES y EN.
- [x] **Target HR** (12/2018 – 04/2019) — clientes Intralot y UNICON. Aplicado ES/EN.
- [x] **Anka Innovations** (01/2019 – 02/2020) — co-founder / CTO. Aplicado ES/EN.
- [x] **Process & Technology Solutions** (12/2019 – 02/2020) — cliente Entel. Aplicado ES/EN.
  *Solape aclarado: Anka era proyecto paralelo como socio/CTO; P&T fue empleo dentro de ese período.*
- [x] **Globant** (03/2020 – 05/2022) — cliente Lulo Bank, equipo back-processes.
  Título: Desarrollador Backend Semi-Senior / Mid-level Backend Developer. Aplicado ES/EN.
- [x] **Aditi Consulting** (05/2022 – 04/2026) — cliente Wabtec, proyecto PDS 2.0 (cliente final CN, 05/2022 – 03/2026). Stack Java 21 + Quarkus + Kafka + PostgreSQL/AWS RDS + EKS. Proyecto Wabtec **finalizado**; contrato con Aditi cerrado en 04/2026. Título: Senior. Aplicado ES/EN.
- [x] **Origen 360 / Pezconfiable** (11/2025 – actualidad) — CTO. Startup peruana de pesca artesanal + trazabilidad. Colaboración por entregables (no fulltime, no part-time formal; freelance-like). Stack Java 21 + Quarkus + Python + PostgreSQL + Keycloak + AWS EC2. Equipo: 1 back (usuario) + 1 front, con LLMs como acelerador. Aplicado ES/EN arriba de Aditi.

**Nota sobre solapes**: Decidido NO mencionar explícitamente que Origen 360 corre en paralelo a Aditi; las fechas hablan solas (consistente con el tratamiento de Anka/P&T anterior, donde tampoco se etiquetó "paralelo" en el bullet final).

## Contacto y metadatos del HTML

### Sección de contacto
- **Dirección física completa: fuera.** Reemplazada por ubicación simple
  `Lima, Perú · GMT-5` (`Lima, Peru · GMT-5` en EN). Reduce PII innecesaria
  y aporta el dato realmente útil para roles remotos/internacionales:
  ciudad y zona horaria.
- Se mantienen teléfono (con código de país), email y LinkedIn.
- GitHub / portfolio: pendiente de decisión del usuario sobre cómo
  presentar miniproyectos personales.

### Metadatos HTML
- **`<title>` único cambio relevante** porque algunos conversores
  HTML→PDF lo usan como título del documento PDF. Estandarizado a
  `Sergio Robles - CV - Arquitecto de Software Backend` /
  `Sergio Robles - CV - Backend Software Architect`.
- `lang="es"` / `lang="en"` se mantiene (importa para accesibilidad
  en lectores de PDF).
- `<meta description>`, keywords, OG tags: **omitidos** porque el CV se
  envía como PDF, no se publica como página web.

## Confidencialidad / NDA

Pasada de revisión sobre el historial laboral para evitar exponer información
cubierta por NDA o que dañe reputacionalmente a clientes. Criterios aplicados:

- **No nombrar artefactos internos por su nombre código**: librerías, módulos
  o tipos de entidad con nombres internos (ej. `number-pool`, `R43`) se
  describen por **función** ("librería interna de reserva concurrente de
  identificadores correlativos", "el tipo de restricción con la lógica de
  negocio más compleja del módulo"). Aporta lo mismo al lector y no es
  trazable de vuelta al producto.
- **No atribuir defectos en producción al cliente**: describir el defecto
  técnico que el usuario resolvió, sin mencionar el impacto de negocio que
  haya tenido en el cliente. Aplicado a Lulo Bank: se conserva el detalle
  técnico (XIRR / `BigDecimal` / convergencia) y se elimina "generaba
  asientos contables incorrectos".
- **No describir madurez/precariedad del cliente**: comentarios tipo "sin
  CI/CD", "despliegue manual", "sin tests" se omiten o suavizan; pintan
  mal al cliente y a la consultora sin aportar al perfil. Aplicado a P&T /
  Entel.
- **No exponer topología interna de infraestructura**: cifras concretas de
  cluster (nº de masters/workers), VPC, subredes, etc. se reemplazan por la
  tecnología sin la cifra. Aplicado a Ebiz (AKS sin "2 masters + 5 workers").
- **Sí se conservan**: nombre del cliente y del producto cuando ya son
  públicos (notas de prensa, sitios oficiales, contratos públicos), nombre
  de obligaciones regulatorias públicas (ej. TDA), tecnologías y patrones
  arquitectónicos, descripción funcional del módulo.

Anécdotas con detalle sensible que sí pueden contarse en entrevista (no en
CV) van a la sección **"Anécdotas y contenido reservado para entrevista"**.

## Información pendiente de aclarar (global)
- Métricas de impacto por proyecto (volúmenes, escala, tamaño de equipos
  liderados).
- Certificaciones cloud (AWS / GCP / Azure Architect): ¿tiene, planea?
- GitHub / portfolio público: ¿incluir?
- Tecnologías omitidas a confirmar: Terraform, OpenAPI/Swagger, gRPC,
  RabbitMQ, Redis, observabilidad (Prometheus/Grafana), service mesh.
- Rol objetivo exacto: Software Architect / Solutions Architect /
  Tech Lead-Architect / Backend Architect.
