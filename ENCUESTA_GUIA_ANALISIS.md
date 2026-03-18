# FOODIX Stars — Guía Completa de Análisis
## Encuesta de Clima Laboral 2026

---

## 1. Estructura general

| Campo DB | Tipo | Descripción |
|---|---|---|
| `id` | uuid | Clave primaria (auto) |
| `created_at` | timestamptz | Fecha/hora de envío |
| `local` | text | Código de local (ej: CH001) |
| `nivel` | text | N1, N2 o N3 |
| `subnivel` | text | Solo N2: `gerente` o `admin` |
| `e1`–`e6` | smallint | Bloque Empresa FOODIX |
| `l1`–`l7` | smallint | Bloque Líder Inmediato |
| `t1`–`t6` | smallint | Bloque Equipo |
| `m1`–`m5` | smallint | Bloque Sobre mí mismo/a |
| `p1`–`p6` | smallint | Bloque Pertenencia |
| `f1`–`f4` | smallint | Bloque Futuro en FOODIX |
| `a1`–`a6` | smallint | Bloque Ambiente de Trabajo |
| `beneficios_orden` | text[] | Array ordenado de prioridades |
| `c1`, `c2`, `c3` | text | Comentarios abiertos |

**Escala Likert:** 1 = Muy en desacuerdo / Nunca → 4 = Muy de acuerdo / Siempre

---

## 2. Locales y niveles

| Código | Marca / Local | Niveles disponibles |
|---|---|---|
| CH001 | Chios Real Audiencia | N1, N2 |
| CH002 | Chios Portugal | N1, N2 |
| CH003 | Chios (otro) | N1, N2 |
| SB001 | Simon Bolón | N1, N2 |
| SC001 | Sushi Corp 1 | N1, N2 |
| SC002 | Sushi Corp 2 | N1, N2 |
| FX001 | Foodix Planta 1 | N1, N2, N3 |
| FX002 | Foodix Planta 2 | N1, N2, N3 |

### Niveles
- **N1** — Polifuncionales y Operativos
- **N2** — Gerentes de Tienda (`subnivel=gerente`) / Auxiliares, Asistentes y Analistas (`subnivel=admin`)
- **N3** — Supervisores, Coordinadores y Jefaturas (solo FX001/FX002)

---

## 3. Preguntas Likert — detalle completo

> **⚠️ PREGUNTAS INVERSAS:** Marcadas con `[INV]`. Para calcular scores, aplicar: `score_ajustado = 5 - valor_respondido`
> Ejemplo: si respondió 1 (Muy en desacuerdo) en una pregunta inversa, el score positivo es 4.

---

### Bloque E — Sobre nuestra empresa FOODIX
*Escala: Acuerdo (1=Muy en desacuerdo → 4=Muy de acuerdo)*
*Instrucción: "Piensa en tu experiencia general trabajando en FOODIX."*

| Var | Pregunta | Tipo |
|---|---|---|
| E1 | ¿FOODIX es una empresa que busca soluciones en lugar de quedarse en los problemas? | Normal |
| E2 | ¿Te has sentido bienvenido/a y valorado/a por nosotros desde que ingresaste? | Normal |
| E3 | ¿FOODIX se preocupa por mi crecimiento y aprendizaje? | Normal |
| E4 | Siento que en FOODIX las cosas se hacen con pasión y dedicación real. | Normal |
| E5 | Siento que en FOODIX me exigen resultados, pero no se preocupan por cómo estoy. | **[INV]** |
| E6 | ¿Qué tan familiarizado/a estás con los valores de la empresa? | Normal |

---

### Bloque L — Mi Líder Inmediato
*Escala: Acuerdo (1→4)*
*Instrucción: "Piensa en tu jefe directo del día a día al responder estas preguntas."*

| Var | Pregunta | Tipo |
|---|---|---|
| L1 | Mi líder mantiene la calma y busca soluciones cuando hay problemas en la operación. | Normal |
| L2 | Mi líder me trata con respeto. | Normal |
| L3 | Mi líder demuestra que le importa cómo me siento, no solo lo que produzco. | Normal |
| L4 | Mi líder da el ejemplo trabajando con la misma entrega que nos pide. | Normal |
| L5 | Mi líder me ayuda a mejorar en mi trabajo. | Normal |
| L6 | Mi líder toma decisiones sin decirle al equipo la razón. | **[INV]** |
| L7 | Mi líder reconoce cuando hago bien mi trabajo. | Normal |

---

### Bloque T — Mi Equipo
*Escala: Acuerdo (1→4)*
*Instrucción: "Piensa en las personas con quienes trabajas día a día."*

| Var | Pregunta | Tipo |
|---|---|---|
| T1 | Mi equipo se apoya mutuamente cuando hay presión en el servicio. | Normal |
| T2 | Mis compañeros son amables y respetuosos conmigo en el día a día. | Normal |
| T3 | Mis compañeros aceptan las opiniones de los demás sin tomárselo personal. | Normal |
| T4 | Mis compañeros hacen su trabajo con dedicación y no solo "por cumplir". | Normal |
| T5 | Siento que trabajamos como un verdadero equipo, no solo como individuos en el mismo turno. | Normal |
| T6 | Cuando alguien se equivoca, mis compañeros lo critican en lugar de ayudarlo. | **[INV]** |

---

### Bloque M — Sobre mí mismo/a
*Escala: Acuerdo (1→4)*
*Instrucción: "Estas preguntas son sobre ti y cómo actúas en tu trabajo."*

| Var | Pregunta | Tipo |
|---|---|---|
| M1 | Cuando algo sale mal en mi turno, busco soluciones para corregirlo. | Normal |
| M2 | Cuando un compañero necesita ayuda en el turno, lo apoyo aunque no sea mi responsabilidad directa. | Normal |
| M3 | Me fijo en los detalles de mi trabajo aunque nadie esté mirando o revisando. | Normal |
| M4 | Cuando cometo un error, analizo qué pasó para no repetirlo. | Normal |
| M5 | **Variable según nivel/local** — ver tabla abajo | Ver tabla |

#### M5 — Pregunta variable

| Condición | Texto de M5 | Tipo |
|---|---|---|
| N3 (cualquier local) | En los momentos de más presión, me cuesta mantener la calma frente a mi equipo. | **[INV]** |
| N2 + subnivel=gerente | En los momentos de más presión, me enfoco en los resultados aunque deje de acompañar a mi equipo en el proceso. | **[INV]** |
| N2 + subnivel=admin | Cuando identifico un problema en mi área antes de que me lo señalen, lo resuelvo o lo escalo sin esperar a que alguien más lo note. | Normal |
| N1 + local=FX001 | En los momentos de más presión en línea, priorizo el volumen aunque baje la calidad del producto. | **[INV]** |
| N1 (resto de locales) | En los momentos de más presión, mi prioridad es despachar rápido. | **[INV]** |

---

### Bloque P — Mi Pertenencia en FOODIX
*Escala: Acuerdo (1→4)*
*Instrucción: "¿Cómo te sientes siendo parte de FOODIX?"*

| Var | Pregunta | Tipo |
|---|---|---|
| P1 | Cuando alguien me pregunta dónde trabajo, lo digo con gusto. | Normal |
| P2 | Recomendaría FOODIX como un buen lugar para trabajar. | Normal |
| P3 | Sé con claridad cómo lo que hago cada día impacta en la experiencia del cliente. | Normal |
| P4 | Lo que FOODIX quiere lograr como empresa coincide con lo que me importa a mí. | Normal |
| P5 | ¿Conozco los valores de FOODIX? | Normal |
| P6 | Cuando tengo un mal día en el trabajo, pienso en buscar otro empleo. | **[INV]** |

---

### Bloque F — Mi Futuro en FOODIX
*Escala: Acuerdo (1→4)*
*Instrucción: "¿Cómo te imaginas en FOODIX hacia adelante?"*

| Var | Pregunta | Tipo |
|---|---|---|
| F1 | Si me ofrecieran un trabajo similar con el mismo sueldo en otra empresa, lo tomaría. | **[INV]** |
| F2 | En los últimos 3 meses he buscado trabajo en otro lugar. | **[INV]** |
| F3 | Me quedo en FOODIX porque necesito, no porque quiera. | **[INV]** |
| F4 | Me veo trabajando en FOODIX dentro de 1 año. | Normal |

---

### Bloque A — Mi Ambiente de Trabajo
*Escala: Acuerdo (1→4)*
*Instrucción: "¿Cómo son las condiciones en tu lugar de trabajo?"*

| Var | Pregunta | Tipo |
|---|---|---|
| A1 | Recibo información clara sobre lo que tengo que hacer en mi trabajo. | Normal |
| A2 | Si tengo una idea para mejorar algo en mi área, me siento cómodo/a compartiéndola con mi líder. | Normal |
| A3 | Siento que lo que recibo de FOODIX — sueldo, beneficios y reconocimiento — vale el esfuerzo que pongo. | Normal |
| A4 | Puedo cumplir con mis tareas del turno sin sentir que el tiempo no me alcanza. | Normal |
| A5 | Cuento con las herramientas y equipos necesarios para hacer bien mi trabajo. | Normal |
| A6 | En mi turno hay situaciones que me impiden hacer bien mi trabajo. | **[INV]** |

---

## 4. Resumen de preguntas inversas

| Variable | Bloque |
|---|---|
| E5 | Empresa |
| L6 | Liderazgo |
| T6 | Equipo |
| M5 | Yo mismo (según nivel) |
| P6 | Pertenencia |
| F1, F2, F3 | Futuro |
| A6 | Ambiente |

**Total inversas fijas: 9** (+ M5 que puede ser inversa según segmento)

**Fórmula de corrección:**
```
score_ajustado = 5 - valor_respondido
```
Donde `valor_respondido` ∈ {1, 2, 3, 4}

---

## 5. Beneficios — Ranking por nivel

Los encuestados arrastran y reordenan los beneficios. Se guarda en `beneficios_orden` como array ordenado de mayor a menor preferencia (índice 0 = más valorado).

### N1 — Operativos
1. Alimentación
2. Bonos de desempeño por cumplimiento de metas
3. Cursos / Capacitaciones pagadas
4. Día libre a elección (Por Cumplimiento)
5. Reconocimiento Público (Empleado del mes, grupos de WhatsApp)
6. Tarjeta de Bono de Compras (descuento en rol de pagos)
7. Transporte

### N2 — Gerentes / Auxiliares
1. Bonos de desempeño por KPIs
2. Cursos / Capacitaciones pagadas
3. Día libre a elección
4. Reconocimiento público (Empleado del mes)
5. Reconocimiento entre compañeros
6. Transporte
7. Flexibilidad horaria
8. Capacitación técnica externa

### N3 — Supervisores y Jefaturas
1. Bonos por cumplimiento de OKRs trimestrales
2. Plan de carrera documentado
3. Flexibilidad horaria
4. Capacitación técnica externa
5. Reconocimiento por innovación y propuestas implementadas
6. Día libre adicional
7. Trabajo híbrido donde aplique
8. Participación en decisiones estratégicas

**Para análisis:** calcular puntaje de beneficio = `(n_opciones - posición) + 1`, luego sumar por beneficio para obtener ranking agregado.

---

## 6. Preguntas abiertas

| Var | Pregunta |
|---|---|
| C1 | ¿Qué verdad sobre FOODIX, tu equipo o tus líderes crees que todos piensan pero nadie se atreve a decir? |
| C2 | Si pudieras cambiar una sola cosa de FOODIX, ¿qué sería y por qué? |
| C3 | ¿Hay algo que quieras decirle a TTHH o a la Gerencia que normalmente no tienes oportunidad de expresar? |

**Para análisis:** clasificación temática (NLP/manual), sentiment analysis, frecuencia de palabras clave.

---

## 7. Dimensiones compuestas sugeridas para el análisis

| Dimensión | Variables incluidas | Descripción |
|---|---|---|
| **Índice Empresa** | E1–E6 (E5 inv) | Percepción general de FOODIX |
| **Índice Liderazgo** | L1–L7 (L6 inv) | Calidad del liderazgo directo |
| **Índice Equipo** | T1–T6 (T6 inv) | Dinámica y cohesión del equipo |
| **Índice Autoeficacia** | M1–M5 (M5 según segmento) | Actitud y desempeño personal |
| **Índice Pertenencia / eNPS** | P1–P6 (P6 inv) | Sentido de pertenencia y orgullo |
| **Índice Retención** | F1–F4 (F1, F2, F3 inv) | Intención de quedarse en FOODIX |
| **Índice Ambiente** | A1–A6 (A6 inv) | Condiciones operativas y entorno |
| **Score Global** | Promedio de todos los índices | Clima laboral general |

### Fórmula de índice (0–100)
```
índice = ((promedio_ajustado - 1) / 3) × 100
```
Donde `promedio_ajustado` = promedio de variables del bloque, con inversas ya corregidas.

### Semáforo de interpretación
| Rango | Color | Interpretación |
|---|---|---|
| 80–100 | 🟢 Verde | Fortaleza — mantener y comunicar |
| 60–79 | 🟡 Amarillo | Área de mejora — atención moderada |
| 40–59 | 🟠 Naranja | Riesgo — requiere plan de acción |
| 0–39 | 🔴 Rojo | Crítico — intervención urgente |

---

## 8. Consulta SQL base para análisis

```sql
-- Score ajustado por fila (preguntas inversas corregidas)
SELECT
  id, created_at, local, nivel, subnivel,

  -- Bloque E (E5 inverso)
  ROUND((e1 + e2 + e3 + e4 + (5-e5) + e6)::numeric / 6, 2) AS score_empresa,

  -- Bloque L (L6 inverso)
  ROUND((l1 + l2 + l3 + l4 + l5 + (5-l6) + l7)::numeric / 7, 2) AS score_liderazgo,

  -- Bloque T (T6 inverso)
  ROUND((t1 + t2 + t3 + t4 + t5 + (5-t6))::numeric / 6, 2) AS score_equipo,

  -- Bloque M (M5: inverso para N1 y N3; normal para N2+admin)
  ROUND((m1 + m2 + m3 + m4 +
    CASE WHEN nivel IN ('N1','N3') OR (nivel='N2' AND subnivel='gerente')
         THEN (5-m5) ELSE m5 END)::numeric / 5, 2) AS score_yo,

  -- Bloque P (P6 inverso)
  ROUND((p1 + p2 + p3 + p4 + p5 + (5-p6))::numeric / 6, 2) AS score_pertenencia,

  -- Bloque F (F1, F2, F3 inversos)
  ROUND(((5-f1) + (5-f2) + (5-f3) + f4)::numeric / 4, 2) AS score_futuro,

  -- Bloque A (A6 inverso)
  ROUND((a1 + a2 + a3 + a4 + a5 + (5-a6))::numeric / 6, 2) AS score_ambiente

FROM public.gth_encuesta_foodix_2026_03
ORDER BY created_at DESC;
```

```sql
-- Promedios por local y nivel
SELECT
  local, nivel,
  COUNT(*) AS n,
  ROUND(AVG(e1 + e2 + e3 + e4 + (5-e5) + e6)::numeric / 6, 2) AS empresa,
  ROUND(AVG(l1 + l2 + l3 + l4 + l5 + (5-l6) + l7)::numeric / 7, 2) AS liderazgo,
  ROUND(AVG(t1 + t2 + t3 + t4 + t5 + (5-t6))::numeric / 6, 2) AS equipo,
  ROUND(AVG(a1 + a2 + a3 + a4 + a5 + (5-a6))::numeric / 6, 2) AS ambiente,
  ROUND(AVG(p1 + p2 + p3 + p4 + p5 + (5-p6))::numeric / 6, 2) AS pertenencia,
  ROUND(AVG((5-f1) + (5-f2) + (5-f3) + f4)::numeric / 4, 2) AS retencion
FROM public.gth_encuesta_foodix_2026_03
GROUP BY local, nivel
ORDER BY local, nivel;
```

---

## 9. Análisis de beneficios (SQL)

```sql
-- Ranking agregado de beneficios (mayor puntaje = más valorado)
WITH unnested AS (
  SELECT
    local, nivel,
    beneficio,
    -- posición 0 = más valorado → puntaje inverso
    cardinality(beneficios_orden) - ordinality + 1 AS puntaje
  FROM public.gth_encuesta_foodix_2026_03,
  LATERAL unnest(beneficios_orden) WITH ORDINALITY AS t(beneficio, ordinality)
  WHERE beneficios_orden IS NOT NULL
)
SELECT
  nivel,
  beneficio,
  COUNT(*) AS menciones,
  ROUND(AVG(puntaje), 2) AS puntaje_promedio,
  SUM(puntaje) AS puntaje_total
FROM unnested
GROUP BY nivel, beneficio
ORDER BY nivel, puntaje_total DESC;
```

---

## 10. Notas para el análisis

1. **Mínimo de respuestas por local para reportar:** 3 (privacidad del encuestado)
2. **M5 debe segmentarse** por nivel antes de agregar — no sumar sin corregir la escala
3. **F2** ("he buscado trabajo") es el predictor más directo de riesgo de rotación
4. **P2** ("recomendaría FOODIX") equivale al eNPS — tratar como indicador crítico
5. **Comentarios C1–C3** procesar con análisis de texto para identificar temas recurrentes
6. Los `beneficios_orden` del mismo nivel son comparables entre sí; entre niveles NO (listas distintas)
