# Acuerdos para la edición del CV

Este documento captura las decisiones tomadas durante la revisión y mejora del CV
(`CV_SR_editable.html` en español y `CV_SR_editable_english.html` en inglés).

## Objetivo del CV
Reposicionar el perfil de **"Desarrollador Backend"** a un perfil orientado a
**roles de diseño de arquitectura** (Software Architect / Backend Architect /
Tech Lead con foco arquitectónico), sin inflar responsabilidades pasadas.

## Proceso de trabajo
- Revisamos el CV **por secciones**, una a la vez. Orden actual:
  1. Experiencia laboral (en curso, cronológicamente desde la más antigua).
  2. (Pendiente) Resumen / summary.
  3. (Pendiente) Aptitudes principales (sidebar).
  4. (Pendiente) Aptitudes detalladas.
  5. (Pendiente) Certificaciones, idiomas, voluntariado, formación.
  6. (Pendiente) Metadatos del HTML (`<title>`, etc.).
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
| Anka Innovations | EDAN (INDECI) | https://portal.indeci.gob.pe/respuesta/edan/ |
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

## Estado del progreso (experiencia laboral)
- [x] **Ebiz Latin America** (06/2017 – 09/2018) — aplicado en ES y EN.
- [x] **Target HR** (12/2018 – 04/2019) — clientes Intralot y UNICON. Aplicado ES/EN.
- [x] **Anka Innovations** (01/2019 – 02/2020) — co-founder / CTO. Aplicado ES/EN.
- [x] **Process & Technology Solutions** (12/2019 – 02/2020) — cliente Entel. Aplicado ES/EN.
  *Solape aclarado: Anka era proyecto paralelo como socio/CTO; P&T fue empleo dentro de ese período.*
- [x] **Globant** (03/2020 – 05/2022) — cliente Lulo Bank, equipo back-processes.
  Título: Desarrollador Backend Semi-Senior / Mid-level Backend Developer. Aplicado ES/EN.
- [x] **Aditi Consulting** (05/2022 – actualidad) — cliente Wabtec, proyecto PDS 2.0 (cliente final CN, 05/2022 – 03/2026). Stack Java 21 + Quarkus + Kafka + PostgreSQL/AWS RDS + EKS. Proyecto Wabtec **finalizado**; usuario actualmente en bench. Título: Senior. Aplicado ES/EN.
- [x] **Origen 360 / Pezconfiable** (11/2025 – actualidad) — CTO. Startup peruana de pesca artesanal + trazabilidad. Colaboración por entregables (no fulltime, no part-time formal; freelance-like). Stack Java 21 + Quarkus + Python + PostgreSQL + Keycloak + AWS EC2. Equipo: 1 back (usuario) + 1 front, con LLMs como acelerador. Aplicado ES/EN arriba de Aditi.

**Nota sobre solapes**: Decidido NO mencionar explícitamente que Origen 360 corre en paralelo a Aditi; las fechas hablan solas (consistente con el tratamiento de Anka/P&T anterior, donde tampoco se etiquetó "paralelo" en el bullet final).

## Información pendiente de aclarar (global)
- Métricas de impacto por proyecto (volúmenes, escala, tamaño de equipos
  liderados).
- Certificaciones cloud (AWS / GCP / Azure Architect): ¿tiene, planea?
- GitHub / portfolio público: ¿incluir?
- Tecnologías omitidas a confirmar: Terraform, OpenAPI/Swagger, gRPC,
  RabbitMQ, Redis, observabilidad (Prometheus/Grafana), service mesh.
- Rol objetivo exacto: Software Architect / Solutions Architect /
  Tech Lead-Architect / Backend Architect.
