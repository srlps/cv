# Metodología de estimación de tiempo y tokens (referencia genérica)

> **Esto NO es específico de Gris Estudio.** Es una metodología pensada para estimar, en
> cualquier proyecto de software, cuánto tiempo (en días de trabajo) y cuántos tokens de LLM va a
> costar implementar una lista de features, cuando el desarrollo lo hace **una sola persona**
> apoyada en un agente de código (GitHub Copilot) usando dos modelos según la complejidad de la
> tarea: uno rápido/económico para tareas simples y uno más potente para tareas complejas (en este
> momento, Claude Sonnet y Claude Opus respectivamente, en sus versiones más recientes).
>
> Se escribió esta metodología primero, de forma independiente, para poder aplicarla después de
> forma consistente en [hitos_de_implementacion.md](hitos_de_implementacion.md) (sección de
> estimaciones al final de cada hito) y para poder reutilizarla en futuros proyectos sin tener que
> reinventar los criterios cada vez.

## 1. Unidad de trabajo: la "feature"

No se estima el hito completo de un solo salto — se estima abajo (bottom-up) sobre un conjunto de
**features relativamente grandes**: unidades de trabajo con alcance propio, que se pueden describir
en una frase (p. ej. "CRUD de clientes", "motor de alertas de gasto vs. presupuesto"), que
normalmente terminan en una funcionalidad usable/probable de punta a punta, y que no son tan
pequeñas como una tarea de un solo archivo ni tan grandes como un hito entero.

Regla práctica: si al describir la feature necesitás la palabra "y" para juntar dos cosas que no
dependen una de la otra, probablemente son dos features, no una.

## 2. Clasificación de complejidad

Cada feature se clasifica en una de cuatro categorías. La clasificación es lo único que hay que
decidir "a mano" por feature; todo lo demás (días, tokens) sale de la tabla de abajo.

| Categoría | Cuándo aplica | Modelo principal | Duración típica | Turnos típicos de agente | Tokens típicos por turno | Tokens totales estimados |
|---|---|---|---|---|---|---|
| **Simple** | Sigue un patrón ya resuelto antes en el mismo proyecto (otro CRUD parecido, otra pantalla con la misma forma, lógica directa sin reglas de negocio nuevas) | Sonnet | 1–1.5 horas | 6–10 | 8k–15k | ~80k–150k |
| **Moderado** | Entidad o flujo nuevo, con reglas de negocio propias, pero construido sobre arquitectura/patrones que el proyecto ya definió | Sonnet (con alguna revisión puntual en Opus para decisiones de diseño) | 2–3 horas | 10–16 | 12k–20k | ~150k–300k |
| **Complejo** | Motor/engine que otras partes del sistema van a reusar, integración externa ya conocida en el proyecto pero con reglas nuevas, o decisión de arquitectura no trivial | Opus (diseño y partes críticas) + Sonnet (implementación de detalle) | 1–2 días | 16–28 | 20k–40k | ~400k–900k |
| **Complejo — primera vez** | Igual que Complejo, pero sin ningún patrón previo en el proyecto para apoyarse (primera integración externa del proyecto, primer pipeline de despliegue, primer sistema de autenticación, etc.) | Opus | 2–4 días (rara vez 5) | 20–35 | 25k–45k | ~600k–1.2M |

Las duraciones de Simple y Moderado son cortas a propósito: asumen un desarrollador con criterio
de ingeniería ya formado, que sabe darle contexto al agente, armar bien el arnés (harness) de la
tarea y revisar el resultado sin tener que iterar mucho. No son duraciones genéricas para
cualquier desarrollador — están calibradas contra el ritmo real de trabajo de este desarrollador
en particular.

Los rangos de "turnos" y "tokens por turno" no son una medición real de este proyecto (todavía no
hay historial) — son un punto de partida razonable basado en cómo trabaja un agente de código
moderno: cada turno suele incluir leer algunos archivos de contexto, escribir o modificar código, y
a veces correr una validación. Cuantos más archivos toca una feature y más iteraciones de
corrección necesita, más turnos y más tokens por turno.

## 3. De complejidad a días

Simple y Moderado se miden directamente en **horas** (son bien menores a una jornada completa).
Complejo y Complejo — primera vez se miden en **días completos**, asumiendo una jornada de ~4 horas
efectivas de trabajo (con el margen normal de que un día complejo se extienda un poco más esa misma
tarde, o se corte ahí y el resto pase al día siguiente si el desarrollador ya se cansó).

$$
\text{horas}_{\text{feature}} = \text{duración típica de su categoría (Simple/Moderado)}
$$

$$
\text{días}_{\text{feature}} = \text{duración típica de su categoría (Complejo/Complejo — primera vez)}
$$

Para totalizar a nivel de hito, las duraciones en horas se convierten a fracción de día dividiendo
entre 4 y se suman al resto de features ya expresadas en días:

$$
\text{días}_{\text{hito}} = \sum_{\text{Complejo(s)}} \text{días}_{\text{feature}} \; + \; \frac{\sum_{\text{Simple/Moderado}} \text{horas}_{\text{feature}}}{4}
$$

Se reporta como rango (mínimo–máximo), no como número puntual, porque a este nivel de detalle
(antes de escribir código real) sigue habiendo incertidumbre real. Se asume:

- Jornada de ~4 horas efectivas de trabajo por día.
- Un solo desarrollador, sin paralelismo entre features.
- El desarrollador ya conoce el dominio del negocio (no hay tiempo de "aprendizaje del negocio"
  incluido, solo tiempo de implementación con asistencia de IA).

## 4. De complejidad a tokens

$$
\text{tokens}_{\text{feature}} \approx \text{turnos}_{\text{feature}} \times \text{tokens por turno}_{\text{feature}}
$$

$$
\text{tokens}_{\text{hito}} = \sum_{\text{features del hito}} \text{tokens}_{\text{feature}}
$$

El "tokens por turno" ya incluye tanto lo que el agente lee (contexto: archivos abiertos,
resultados de búsqueda, salidas de comandos) como lo que genera (código, explicaciones). Los
turnos con Opus consumen más tokens por turno (más contexto, respuestas más largas por el
razonamiento) pero suelen necesitarse menos turnos para llegar al mismo resultado que con Sonnet en
una tarea igual de compleja; por eso el total no crece linealmente entre categorías.

## 5. De tokens a costo en dólares (GitHub Copilot)

GitHub Copilot factura por **créditos**, a razón de **100 créditos = 1 USD**, y cada modelo tiene un
precio distinto en créditos por millón de tokens según el tipo de token (input, output, cache
read, cache write). Estos precios se guardan en una tabla aparte para poder actualizarlos el día
que cambien, sin tener que tocar el resto de la metodología:

| Modelo | Input (créditos/M tokens) | Output (créditos/M tokens) | Cache read (créditos/M tokens) | Cache write (créditos/M tokens) |
|---|---|---|---|---|
| Sonnet | 200 | 1000 | 20 | 250 |
| Opus | 500 | 2500 | 50 | 625 |

El "tokens totales estimados" de la sección 2 es una mezcla de estos cuatro tipos, no un solo tipo.
Como un agente de código reenvía en cada turno el historial de la conversación y los archivos ya
leídos, la mayor parte de ese contexto ya estaba cacheado de turnos anteriores (cache read, muy
barato); una porción menor es contexto genuinamente nuevo este turno (input fresco, o contexto que
recién se cachea); y el resto es lo que el modelo genera (output). Se asume el mismo perfil de
mezcla para ambos modelos:

| Tipo de token | % del total estimado por turno |
|---|---|
| Input (contexto nuevo, no cacheado) | 15% |
| Output (código/texto generado) | 15% |
| Cache read (contexto ya cacheado en turnos anteriores) | 55% |
| Cache write (contexto nuevo que se cachea recién este turno) | 15% |

Con las dos tablas de arriba, el costo en dólares por millón de tokens totales, por modelo, es:

$$
\text{USD/M tokens}_{\text{modelo}} = \frac{\displaystyle\sum_{\text{tipo}} \%_{\text{tipo}} \times \text{precio}_{\text{tipo,modelo}}}{100}
$$

Con los precios y la mezcla de arriba, esto da (redondeado):

| Modelo | USD por millón de tokens (mezcla estimada) |
|---|---|
| Sonnet | ~$2.29 |
| Opus | ~$5.71 |

Y el costo de una feature sale de multiplicar sus tokens totales estimados (en millones) por la
tarifa mezclada de su modelo asignado:

$$
\text{costo}_{\text{feature}} (\text{USD}) = \frac{\text{tokens}_{\text{feature}}}{1{,}000{,}000} \times \text{USD/M tokens}_{\text{modelo}}
$$

$$
\text{costo}_{\text{hito}} (\text{USD}) = \sum_{\text{features del hito}} \text{costo}_{\text{feature}}
$$

Si los precios de Copilot cambian, alcanza con actualizar la primera tabla de esta sección (y, si
cambia mucho el patrón de uso de cache, la segunda) — las fórmulas y los totales aplicados en
`hitos_de_implementacion.md` se recalculan a mano a partir de esas dos tablas.

## 6. Costo del tiempo del desarrollador (USD)

Además de lo que cuesta la IA, la otra mitad real del costo de una feature es el tiempo del
desarrollador. Se calcula aparte de la sección anterior porque parte de una tarifa distinta: el
valor de mercado de tu tiempo como ingeniero, no el precio de un proveedor de LLMs.

| Concepto | Valor |
|---|---|
| Sueldo mensual de referencia | 7,000 USD |
| Mercado de referencia | Remoto/internacional, para un perfil senior backend (9 años) en transición a arquitecto de software, full-stack en proyectos personales, con certificación IEEE en arquitectura de sistemas con LLM |
| Jornada con la que se calcula ese sueldo | 8 horas/día, 5 días/semana (jornada de oficina completa — **no** las 4h/día que este proyecto en particular recibe) |
| Días laborables asumidos por mes | 20 |
| Horas de referencia por mes | 160 (20 × 8) |
| Tarifa por hora resultante | **~$43.75/hora** |

> Esta tabla es la que hay que editar si cambia tu sueldo de referencia, tu jornada de referencia,
> o los días laborables asumidos por mes — el resto de la sección se recalcula a partir de ella.

$$
\text{tarifa}_{\text{hora}} = \frac{\text{sueldo mensual de referencia}}{\text{días laborables/mes} \times \text{horas de jornada completa}}
$$

La tarifa por hora es la misma sin importar cuántas horas al día le dediques realmente a un
proyecto puntual — las 4h/día de la sección 3 son una restricción de agenda (cuánto tiempo *tienes*
para este proyecto), no un descuento sobre el valor de tu hora. Por eso el costo de tiempo de una
feature se calcula sobre las horas que la sección 3 ya estimó que le vas a dedicar (directas para
Simple/Moderado, o días × 4h para Complejo/Complejo — primera vez):

$$
\text{costo}_{\text{feature}}^{\text{tiempo}} (\text{USD}) = \text{horas dedicadas}_{\text{feature}} \times \text{tarifa}_{\text{hora}}
$$

$$
\text{costo}_{\text{hito}}^{\text{tiempo}} (\text{USD}) = \sum_{\text{features del hito}} \text{costo}_{\text{feature}}^{\text{tiempo}}
$$

Esto da, por categoría de complejidad (a la tarifa de arriba):

| Categoría | Horas dedicadas | Costo de tiempo estimado |
|---|---|---|
| Simple | 1–1.5 horas | ~$43.75–$65.63 |
| Moderado | 2–3 horas | ~$87.50–$131.25 |
| Complejo | 1–2 días (4–8 horas) | ~$175.00–$350.00 |
| Complejo — primera vez | 2–4 días (8–16 horas) | ~$350.00–$700.00 |

El costo total real de una feature es la suma del costo de IA (sección 5) más este costo de
tiempo — son dos rubros distintos (uno se le paga a GitHub Copilot, el otro es el valor de tu
tiempo) que conviene ver por separado y también sumados:

$$
\text{costo}_{\text{feature}}^{\text{total}} (\text{USD}) = \text{costo}_{\text{feature}}^{\text{IA}} + \text{costo}_{\text{feature}}^{\text{tiempo}}
$$

## 7. Días comprometidos con el cliente

Todo lo anterior da un **rango** (mínimo–máximo) por feature y por hito. Ese rango es información
tuya, no algo que le sirva a un cliente — necesita un solo número por hito para poder planificar.

Ninguno de los extremos del rango es buena idea como compromiso:

- **Sumar el pesimista de cada feature** infla el hito de más: el margen de cada feature individual
  tiende a consumirse igual haya o no imprevistos (Ley de Parkinson / síndrome del estudiante), así
  que protegerte feature por feature desperdicia colchón en vez de usarlo donde realmente hace
  falta.
- **Sumar el promedio de cada feature** es tu mejor apuesta real, pero como compromiso tiene ~50% de
  probabilidad de quedarse corto por hito, y un hito tiene pocas features (4–6) — no hay muestra
  suficiente para que los errores se cancelen entre sí.

En vez de proteger cada feature, el colchón se agrupa **una sola vez, a nivel de hito** (idea de
Critical Chain / PERT: el colchón agregado al final de una cadena de tareas es más eficiente que la
suma de colchones individuales):

$$
\text{días comprometidos}_{\text{hito}} = \text{promedio}_{\text{hito}} + 0.5 \times (\text{pesimista}_{\text{hito}} - \text{promedio}_{\text{hito}}) = \frac{\text{promedio}_{\text{hito}} + \text{pesimista}_{\text{hito}}}{2}
$$

donde, usando los mismos rangos por feature de la sección 3:

$$
\text{promedio}_{\text{hito}} = \sum_{\text{features}} \frac{\text{m\'inimo}_{\text{feature}} + \text{m\'aximo}_{\text{feature}}}{2}
\qquad
\text{pesimista}_{\text{hito}} = \sum_{\text{features}} \text{m\'aximo}_{\text{feature}}
$$

Ese es el **único número de días que se muestra al cliente** por hito (no el rango). Es también la
base de la relación comercial: como el cliente paga **por hito** (precio fijo), no por hora, los
días comprometidos son el compromiso de entrega — si te demoras más de eso, el riesgo y el costo
extra son tuyos, no del cliente.

Por eso el costo de tiempo del desarrollador (sección 6) que se reporta a nivel de hito **no usa el
rango**, usa los días comprometidos:

$$
\text{horas comprometidas}_{\text{hito}} = \text{días comprometidos}_{\text{hito}} \times 4
$$

$$
\text{costo comprometido de tiempo}_{\text{hito}} (\text{USD}) = \text{horas comprometidas}_{\text{hito}} \times \text{tarifa}_{\text{hora}}
$$

El costo de IA (sección 5) **sí sigue siendo un rango**: no es una fecha de entrega, es gasto real
que varía con el uso real del agente, y no hay ninguna razón de negocio para fijarlo a un solo
número.

## 8. Ajustes que hay que aplicar a mano

- **Primera vez en el proyecto:** cualquier feature que dependa de una tecnología/integración que
  el proyecto usa por primera vez sube al menos una categoría (ver "Complejo — primera vez"),
  aunque el feature en sí parezca simple. Esto es lo que justifica que la configuración inicial
  (scaffold, autenticación, hosting, persistencia) se estime aparte y más cara que features
  parecidas más adelante en el proyecto.
- **Reutilización de un motor ya construido:** si una feature solo aplica un motor/engine que ya se
  construyó en una feature anterior (p. ej. una segunda checklist sobre el mismo motor de
  revisión), baja al menos una categoría respecto a la que construyó el motor original.
- **Requerimiento aún no confirmado con el dueño del producto:** si el alcance exacto todavía no
  está confirmado (marcado como "a confirmar" en la documentación de arquitectura), se estima con
  el límite superior del rango de su categoría, no el inferior, para no subestimar.

## 9. Cómo se aplicó en este proyecto

En [hitos_de_implementacion.md](hitos_de_implementacion.md), cada hito (incluyendo el "Hito 0" de
configuración inicial previo al primer hito de Fiorella) tiene, como última subsección, una tabla
de features con su categoría, modelo, días, tokens, costo de IA en USD y costo de tiempo del
desarrollador en USD, seguida de los días comprometidos con el cliente y el costo de tiempo
calculado sobre esos días comprometidos (no sobre el rango), más una línea de costo total (IA +
tiempo comprometido) por hito, todo según esta metodología. Esa subsección es **de uso interno**
(para que el desarrollador planifique tiempo y costo) y se mantiene separada de la descripción en
lenguaje natural de cada hito, que es la que se puede compartir con Fiorella.

## 10. Recalibración

Estos números son un punto de partida, no una promesa. Apenas se termine de implementar el Hito 0 y
el Hito 1 reales, conviene volver a esta tabla y ajustar los rangos de "turnos típicos" y "tokens
por turno" (sección 2), el perfil de mezcla de tokens (sección 5) y la tarifa de referencia del
desarrollador (sección 6) con los datos reales observados (por ejemplo, revisando el historial de
sesiones de Copilot, o si cambia tu tarifa de mercado), para que la estimación de los hitos
siguientes sea más precisa. Si un hito real termina consistentemente muy por debajo o muy por
encima de sus días comprometidos, ajusta el factor 0.5 de la sección 7 (más chico si sueles terminar
antes, más grande si sueles terminar después) en vez de solo ajustar los rangos por categoría.
