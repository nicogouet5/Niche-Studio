# 05 · SOP · Base compartida

Módulo 5 (procedimientos) con la parte de agentes del Módulo 4. Fecha: 2026-11-13.

El estudio tiene **dos flujos de trabajo distintos**. No son un mismo pipeline con dos
configuraciones: parten de cosas diferentes, tienen agentes diferentes y se miden distinto.

| Documento | Flujo |
|---|---|
| [`01-flujo-clipping.md`](01-flujo-clipping.md) | ✂️ Clipping: cazar, cortar, dar formato, entregar |
| [`02-flujo-contenido-original.md`](02-flujo-contenido-original.md) | 🎨 Contenido propio: diseñar, producir, construir audiencia |

## 1. Por qué son dos sistemas

| | ✂️ Clipping | 🎨 Contenido propio |
|---|---|---|
| Lógica | Reactiva: el material ya existe, hay que encontrarlo rápido | Proactiva: la pieza se diseña desde cero |
| Ventaja que se busca | Velocidad, olfato y un formato visual reconocible | Criterio editorial y estilo |
| Punto de partida | El momento: un clip de streamer o una noticia de actualidad | La biblia del canal |
| Vida útil del material | Horas o días | Semanas o meses |
| Cadencia | Diaria, por lotes | Semanal, por lotes de piezas |
| Paso más caro | Encontrar el momento | Guion y composición |
| Identidad visual | Formato propio fijo por canal | Familia de estilo por canal (A–G) |
| Agentes | 5 (C1a, C1b, C2, C3, C4) | 9 (O1–O9) |
| Puertas humanas | 1, rápida, apoyada en el Facilitador | 4, editoriales |
| Métrica rectora | Vistas por clip y por hora de trabajo | Retención y seguidores por mil vistas |

## 2. Qué es un "agente" en esta etapa

Un agente es un **rol con contrato**: misión, disparador, entradas, salidas, herramientas,
límites y criterio de aprobación. Hoy cada agente lo ejecuta una persona con un prompt
documentado o un script. Se convierte en automatización solo cuando el paso demuestra ser
estable (Regla 8).

| Nivel | Qué significa | Cómo se ve |
|---|---|---|
| 0 | Persona + prompt documentado | Se pega la entrada en Claude, ChatGPT o Gemini con el prompt del agente |
| 1 | Script o skill que una persona lanza | Un comando hace el paso completo; la persona revisa la salida |
| 2 | Encadenado y programado | Los pasos se disparan solos; la persona solo atiende las puertas |

**Subir de nivel:** tras unas 30 ejecuciones con salida aceptada sin correcciones mayores y
con el tiempo por ejecución anotado. **Bajar de nivel:** si la salida empieza a requerir
correcciones frecuentes.

Las puertas humanas no suben de nivel: ninguna pieza se publica sin que una persona la
apruebe.

## 3. Infraestructura común

| Recurso | Uso | Costo |
|---|---|---|
| ClickUp (espacio "Niche") | Seguimiento de cada clip y cada pieza por etapa | Plan gratuito |
| Google Drive | Archivos de video, audio, transcripciones y renders | Incluido en la suscripción de Google ya contratada |
| Claude, ChatGPT, Gemini | Motor de los agentes de nivel 0 | Suscripciones ya contratadas |
| ffmpeg, Whisper, librosa | Corte, formato vertical, subtítulos, transcripción, picos de audio | Gratis |
| HyperFrames y catálogo de `04` | Composición de video y estilos | Gratis |
| Este repositorio | SOP, prompts, plantillas y scripts versionados | Gratis |

Cualquier herramienta puede usarse en cualquiera de los dos computadores del estudio. El SOP
no asigna herramientas a equipos; la única consideración práctica es que los renders pesados
tardan menos en el equipo con mejor tarjeta gráfica.

### Estructura de archivos en Drive

```
Niche-Media/
├── clipping/
│   └── <canal>/
│       ├── _plantilla/            fondo, marco, fuentes y estilo de subtítulos del canal
│       └── <AAAA-MM-DD>_<fuente>/
│           ├── fuente/            video original o enlace
│           ├── transcripcion/     .srt y .json
│           ├── momentos.md        candidatos del Minero
│           ├── clips/             clips terminados
│           └── entrega.md         paquete del Facilitador
└── original/
    └── <canal>/
        ├── biblia.md
        ├── activos/               logos, música, personaje, paleta
        └── <ID-pieza>/
            ├── datos.md           ficha del Documentalista
            ├── guion.md
            ├── storyboard.md
            ├── proyecto/          código de la composición
            ├── render/
            └── publicar/          versiones por mercado y plataforma
```

### Identificadores

| Tipo | Formato | Ejemplo |
|---|---|---|
| Clip | `C-<canal>-<fecha>-<n>` | `C-STR1-20261120-03` |
| Pieza original | `O-<canal>-<n>` | `O-FIN1-0007` |

El identificador es el mismo en Drive, en ClickUp y en el registro de derechos de `03`.

## 4. ClickUp

Estado actual del espacio "Niche": carpeta 🎬 Niche Studio (listas Ideas y 🗺️ Misiones ·
Roadmap, subcarpeta AGENTES), carpeta 🎵 TikTok y carpeta ▶️ YouTube, cada una con listas
por idioma.

Estructura propuesta (aún no creada):

| Lista | Dónde | Estados |
|---|---|---|
| ✂️ Pipeline Clipping | 🎬 Niche Studio | Detectado → Momentos → Editado → Entregado → Aprobado G1 → Publicado → Medido |
| 🎨 Pipeline Original | 🎬 Niche Studio | Idea → Puntuada → G1 → Investigación → Guion → G2 → Arte → Motion → Render → G3 → Localizado → Programado → Publicado → Medido |
| Fichas de agente | Subcarpeta AGENTES | Un documento por agente con su prompt vigente |

Campos personalizados sugeridos: canal, carril (streamers, noticias, campaña), fuente,
puntaje, prioridad, nivel de riesgo, familia de estilo, plataforma, minutos de trabajo.

Dos observaciones sobre la estructura actual:

- No hay carpeta de Instagram, aunque es una de las tres plataformas iniciales.
- Las carpetas están organizadas por plataforma, pero un canal del estudio es una marca que
  publica en varias plataformas. Conviene que la unidad sea la marca, con la plataforma como
  campo.

## 5. Relación con los demás documentos

| Documento | Qué aporta al SOP |
|---|---|
| [`03-governance-minimo.md`](../03-governance-minimo.md) | Registro de derechos, niveles de riesgo de cuentas, control previo a publicar |
| [`04-herramientas-produccion.md`](../04-herramientas-produccion.md) | Catálogo de herramientas y familias de estilo |
| [`02-hechos-verificados.md`](../02-hechos-verificados.md) | Políticas de plataforma que condicionan cada flujo |
| [`00-decisiones-fundacionales.md`](../00-decisiones-fundacionales.md) | Modelo de capacidad: minutos disponibles por semana |

## 6. Qué se mide desde el primer día

Sin estas tres anotaciones por pieza no hay forma de decidir después qué automatizar:

1. Minutos humanos por paso.
2. Resultado a 48 horas y a 7 días (vistas, retención, seguidores ganados).
3. Incidencias (reclamos, retiros, rechazos).
