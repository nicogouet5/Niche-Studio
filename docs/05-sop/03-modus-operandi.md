# 05 · SOP · Modus operandi

Manual operativo de los dos flujos: qué herramienta usa cada agente, dónde viven sus entradas
y salidas, cómo se ejecuta cada paso y en qué estado queda la tarea en ClickUp. Fecha: 2026-11-13.

Los detalles de cada agente (misión, límites, prompts, puntajes) están en
[`01-flujo-clipping.md`](01-flujo-clipping.md) y [`02-flujo-contenido-original.md`](02-flujo-contenido-original.md).
Este documento no los repite: los une en un solo recorrido. Si algo cambia aquí, cambia también
en esos dos archivos y en los documentos de ClickUp.

**Estado de prueba:** ✅ probado en el entorno de trabajo · ⚠️ no probado · ⏳ pendiente de decidir.

---

## 1. Herramientas

### 1.1 Instaladas y en uso

| Herramienta | Para qué | Agentes | Estado | Versión / nota |
|---|---|---|---|---|
| ffmpeg | Extraer audio, cortar, reencuadrar 9:16, fondos, subtítulos | C3, O6, O8 | ✅ | 6.1 |
| librosa | Picos de volumen y mapa de golpes para sincronía | C2, O6 (transversal) | ✅ | 1.0.1 |
| faster-whisper (Whisper) | Transcripción con marcas de tiempo | C2 | ⚠️ | 1.2.1. La descarga del modelo estaba bloqueada en el entorno de prueba; el modelo `small` es el punto de partida |
| Claude / ChatGPT / Gemini | Motor de los agentes de nivel 0 | C1a, C1b, C4, O1–O5, O7–O9 | ✅ | Suscripciones ya contratadas |
| ClickUp | Seguimiento por etapa | Todos | ✅ | Plan gratuito; listas de pipeline creadas el 2026-11-13 |
| Google Drive | Archivos de video, audio, transcripciones y renders | Todos | ✅ | Estructura en [`00-base-compartida.md`](00-base-compartida.md) |
| Este repositorio | SOP, prompts, plantillas y scripts | — | ✅ | |

### 1.2 Motores de producción de video (según familia de estilo)

| Herramienta | Familia | Requisitos | Estado | Licencia |
|---|---|---|---|---|
| [HyperFrames](https://github.com/heygen-com/hyperframes) | A, y plantillas de clipping; C como compositor | Node.js 22+, FFmpeg, Chrome; render local | ⚠️ | Apache 2.0 |
| [Lemo Opuscar](https://github.com/lemomo-ai/lemo-opuscar) | B | Plugin de Claude Code; esfuerzo alto del modelo | ⚠️ | Propia: revisar antes de uso comercial |
| [pixelfx](https://github.com/patch-gg/pixelfx) | C | Sin dependencias; se compone en HyperFrames | ⚠️ | MIT |
| [Claude Animation Base](https://github.com/JohnHeibel/ClaudeAnimationBase) | D | Node.js, Chrome, ffmpeg; render lento sin GPU dedicada | ⚠️ | MIT. Su personaje es ajeno: usar uno propio |
| [Three.js](https://github.com/mrdoob/three.js) + [React Three Rapier](https://github.com/pmndrs/react-three-rapier) + [React Postprocessing](https://github.com/pmndrs/react-postprocessing) | E | Node.js; captura de fotogramas | ⚠️ | MIT |
| [Blender MCP](https://github.com/ahujasid/mcp-for-blender) | F | Blender instalado; render pesado | ⚠️ | MIT |
| [Video ShotCraft](https://github.com/Vincentwei1021/video-shotcraft) | G | Remotion (`npx skills add Vincentwei1021/video-shotcraft`) | ⚠️ | Apache 2.0; Remotion tiene licencia propia para empresas |

⚠️ Ninguna rama de familia se ha probado todavía en el estudio. La primera pieza de cada familia
se produce como prueba y se anota su tiempo real antes de adoptarla (regla 5 de `04`).

### 1.3 Reserva y pendientes

| Herramienta | Estado | Criterio |
|---|---|---|
| Clipspeed | En reserva | Solo se reevalúa cuando haya ingresos que lo paguen |
| Motor de voz (texto a voz) | ⏳ | Opción abierta o voz propia de un socio; se elige en la Ola 1 probando español |
| Bibliotecas de prompts (awesome-opus5-5-videos, opus-video-prompts) | Referencia | Solo para explorar estilos antes de fijar la biblia; no se copian prompts literales |

---

## 2. Equipos

Hay dos computadores: **Mac M1** (socio 1) y **PC con GPU** (socio 2). Cualquier herramienta
puede correr en cualquiera; el SOP no asigna herramientas a equipos. La única diferencia práctica:
los renders pesados (HyperFrames con muchas capas, Blender, Claude Animation Base, Three.js con
captura de fotogramas) tardan menos en el PC con GPU.

Antes de empezar una sesión de trabajo, verificar en el equipo que se usará:

```bash
ffmpeg -version | head -1
python3 -c "import librosa, numpy; print('librosa', librosa.__version__)"
python3 -c "import faster_whisper; print('faster-whisper ok')"
node --version
```

Los comandos de instalación de cada herramienta están en el README de su repositorio (ver sección 1)
y en la sección 3 de `04-herramientas-produccion.md`. Ninguno se ha probado en los equipos del
estudio: la primera instalación se anota en el registro de pruebas de la Ola 1.

---

## 3. Protocolo común de ejecución

Todo agente, en cualquier nivel, sigue el mismo protocolo:

1. **Tomar la tarea.** La tarea de ClickUp está en el estado de entrada del agente (ver sección 5).
   Se asigna a quien lo ejecuta y se anota la hora de inicio en el campo de minutos.
2. **Preparar las entradas.** Los archivos se leen desde su ruta en Drive (sección 6).
   Nada se trabaja desde copias sueltas fuera de la estructura.
3. **Ejecutar.** Nivel 0: se pega el prompt vigente de la página de ClickUp del agente, con las
   entradas, en el modelo de lenguaje. Nivel 1: se lanza el script o comando del SOP.
4. **Guardar la salida** con el nombre de la sección 6, en la carpeta de la pieza.
5. **Revisar contra el criterio "Aprobado si"** del agente. Si no cumple, se corrige una vez; si
   vuelve a fallar, se anota la causa en la tarea y se escala a la persona.
6. **Avanzar el estado** de la tarea y **anotar los minutos humanos** del paso.
7. **Puerta humana** si el siguiente paso es G1, G2, G3 o G4: no se avanza sin ella.

Reglas que aplican a todos los agentes: nada se publica sin puerta humana (Regla 15 de `03`);
sin fila en el registro de derechos no hay publicación (Regla 13); un cambio a la vez (Regla 19).

---

## 4. Runbook · Flujo de clipping

Carriles: streamers y noticias, con cuentas separadas. Lista ClickUp: ✂️ Pipeline Clipping.

### Paso 1 · Caza (C1a y C1b)

- **Cuándo:** C1a una vez al día; C1b dos veces (mañana y tarde).
- **Cómo:** nivel 0. Pegar en el modelo el mapa de streamers o de medios del canal, tendencias
  y resultados recientes, con el prompt de C1a o C1b de `01-flujo-clipping.md`.
- **Salida:** cola de fuentes con enlace, motivo, puntaje y, en noticias, nivel de sensibilidad.
  Cada fila se crea como tarea en **Detectado**.
- **Minutos a anotar:** ronda de caza, por lote.

### Paso 2 · Momentos (C2)

```bash
# 1. Audio para transcribir y analizar
ffmpeg -i fuente.mp4 -vn -ac 1 -ar 16000 audio.wav

# 2. Picos de volumen (probado)
python3 picos.py audio.wav

# 3. Transcripción con marcas de tiempo (no probado: verificar en el equipo)
python3 transcribir.py audio.wav es > subs.srt
```

Los scripts `picos.py` y `transcribir.py` están en la sección C2 de `01-flujo-clipping.md`.
Después, el modelo de lenguaje recibe transcripción y picos con el prompt del Minero y devuelve
`momentos.md`. La tarea pasa a **Momentos**.

### Paso 3 · Corte y formato propio (C3)

Elegir la disposición del canal (A, B, C o D) y ejecutar el comando correspondiente de
`01-flujo-clipping.md` (todos probados con ffmpeg 6.1, salida 1080×1920). Para la disposición A,
el fondo de marca vive en `Niche-Media/clipping/<canal>/_plantilla/`.

Revisar: subtítulos sincronizados, título sin tapar la cara, corte sin medias palabras.
La tarea pasa a **Editado**.

### Paso 4 · Paquete del Facilitador (C4)

- **Herramienta:** modelo de lenguaje con el prompt de C4 de `01-flujo-clipping.md`.
- **Entradas:** clips de C3, `momentos.md`, colas de C1a y C1b, resultados de 14 días.
- **Salida:** `entrega.md` en la carpeta de la fuente. La tarea pasa a **Entregado**.

### Paso 5 · Decisión humana (G1)

La persona revisa `entrega.md` y los clips, marca el checklist de G1 en la tarea y decide el orden.
Estados: **Aprobado G1** → publicar → **Publicado** (con la hora) → a las 48 h y 7 días anotar
vistas, retención y seguidores → **Medido**.

### Retroalimentación semanal

Una vez por semana: qué fuentes rindieron (ajusta C1a y C1b), qué tipo de momento funcionó
(ajusta C2), qué disposición retuvo (un cambio a la vez, en la ficha del canal) y reclamos
(fuentes a evitar). Detalle en la sección 5 de `01-flujo-clipping.md`.

---

## 5. Runbook · Flujo de contenido propio

Lista ClickUp: 🎨 Pipeline Original. Cada canal tiene una biblia y una familia de estilo fijadas.

| Paso | Agente | Herramienta | Entrada | Salida | Puerta | Estado ClickUp |
|---|---|---|---|---|---|---|
| Biblia | O1 | Modelo de lenguaje | Nicho, referencias, informe del Analista | `biblia.md` | — | (fuera del pipeline) |
| Temas | O2 | Modelo de lenguaje + tendencias | Biblia, recomendaciones del Analista | Backlog puntuado | **G1** | Idea → Puntuada → G1 Temas |
| Datos | O3 | Modelo de lenguaje + fuentes oficiales | Tema aprobado | `datos.md` con fuentes | — | Investigación |
| Guion | O4 | Modelo de lenguaje | Biblia, tema, `datos.md` | `guion.md` con 3 hooks | **G2** | Guion → G2 Guion |
| Storyboard | O5 | Modelo de lenguaje + catálogo `04` | Guion aprobado | `storyboard.md` con rama | — | Arte |
| Producción | O6 | Herramienta de la rama (sección 1.2) | Storyboard, activos | Video maestro 1080×1920 | **G3** | Motion → Render → G3 Corte final |
| Versiones | O7 | Modelo de lenguaje + TTS | Corte final, mercado | Versiones localizadas | — | Localizado |
| Paquete | O8 | Modelo de lenguaje + ffmpeg | Versiones finales | Paquete por plataforma | Control de `03` | Programado |
| Resultados | O9 | Hoja de métricas | Métricas 48 h y 7 días | Informe semanal | **G4** | Medido |

### Producción por familia (O5 → O6)

O5 escribe en `storyboard.md` la familia del canal y envía la pieza a una sola rama:

| Familia | Preparación obligatoria (antes de O6) | Comando o acción de O6 |
|---|---|---|
| A · Explicativo | Datos verificados; gráficos decididos | Composición HTML con bloques de HyperFrames; render |
| B · Cinematográfico | Estilo elegido en Lemo Opuscar; storyboard aprobado | Construir según `DIRECTOR.md` y `STYLE.md` del estilo |
| C · 8 bits | Paleta y resolución de pixel fijadas en la biblia | Efectos pixelfx sobre composición de HyperFrames |
| D · Personaje | Hoja de modelo del personaje (vistas, emociones) | Plano a plano con hojas de contacto |
| E · 3D navegador | Maqueta de escena y cámara | Escena en Three.js; física con Rapier; Postprocessing; captura de fotogramas |
| F · 3D realista | Maqueta en baja calidad | Blender controlado por el agente; render final |
| G · Promo | Capturas reales y permiso o programa de afiliados | Storyboard con recetas de plano; animación en Remotion |

Si la pieza va al ritmo de la música, librosa genera el mapa de golpes antes de O6 (transversal).

### Cadencia semanal

| Momento | Actividad |
|---|---|
| Inicio de semana | G4 (informe de la semana anterior) y G1 (temas) |
| Primera mitad | Investigación, guiones y G2 en lote |
| Segunda mitad | Storyboard, producción y G3 en lote |
| Cierre | Empaque y programación de la semana siguiente |

---

## 6. Agentes, herramientas y ubicaciones

Resumen para ubicar cualquier paso. Rutas dentro de `Niche-Media/` en Drive.

| Agente | Nivel | Herramienta | Entrada en Drive | Salida en Drive | Estado de entrada → salida |
|---|---|---|---|---|---|
| C1a Cazador de streamers | 0 | Modelo de lenguaje | `clipping/<canal>/_plantilla/` (mapa) | Cola de fuentes en la tarea | — → Detectado |
| C1b Cazador de noticias | 0 | Modelo de lenguaje | Mapa de medios por país | Cola de noticias en la tarea | — → Detectado |
| C2 Minero | 1 + 0 | ffmpeg, faster-whisper, librosa, modelo | `<fecha>_<fuente>/fuente/` | `transcripcion/`, `momentos.md` | Detectado → Momentos |
| C3 Cortador-editor | 1 | ffmpeg, HyperFrames | `momentos.md`, `_plantilla/` | `clips/` | Momentos → Editado |
| C4 Facilitador | 0 | Modelo de lenguaje | `clips/`, `momentos.md`, colas | `entrega.md` | Editado → Entregado |
| O1 Estratega | 0 | Modelo de lenguaje | `original/<canal>/` | `biblia.md` | — |
| O2 Investigador | 0 | Modelo de lenguaje | `biblia.md` | Backlog en la lista | Idea → Puntuada |
| O3 Documentalista | 0 | Modelo de lenguaje + fuentes | Tema | `<ID>/datos.md` | Investigación |
| O4 Guionista | 0 | Modelo de lenguaje | `datos.md` | `<ID>/guion.md` | Guion |
| O5 Director de arte | 0 | Modelo de lenguaje | `guion.md`, `activos/` | `<ID>/storyboard.md` | Arte |
| O6 Productor de motion | 1 (render) | Herramienta de la rama | `storyboard.md`, `activos/` | `<ID>/proyecto/`, `<ID>/render/` | Motion → Render |
| O7 Localizador | 0 | Modelo de lenguaje + TTS | `render/` | `<ID>/publicar/<mercado>/` | Localizado |
| O8 Empaquetador | 0 | Modelo de lenguaje + ffmpeg | `publicar/` | Paquete por plataforma | Programado |
| O9 Analista | 0 | Hoja de métricas | Métricas de cada pieza | Informe semanal | Medido |

---

## 7. Convenciones

- **Identificadores:** clip `C-<canal>-<fecha>-<n>`; pieza original `O-<canal>-<n>`. El mismo ID
  en Drive, en el nombre de la tarea de ClickUp y en el registro de derechos.
- **Registro de derechos:** columnas del punto 4 de `03-governance-minimo.md`.
- **Minutos:** cada paso anota minutos humanos en la tarea. Sin ese dato no se decide qué automatizar.
- **Niveles:** se sube de nivel tras unas 30 ejecuciones estables con tiempo medido (Regla 8). Ningún
  nivel salta la puerta humana.

---

## 8. Fuente de verdad y mantenimiento

- **Fuente de verdad:** este repositorio. Los documentos de ClickUp son copias para uso diario.
- **Cambio de prompt o herramienta:** se hace aquí primero, con fecha; luego se copia a ClickUp.
- **Cambio de familia de un canal:** lo decide G4 y queda en la biblia; no se cambia en mitad de un lote.

## 9. Pendientes

- ⚠️ Probar faster-whisper en los equipos del estudio (la descarga del modelo estaba bloqueada).
- ⚠️ Probar cada motor de familia con una pieza de prueba y anotar tiempo.
- ⏳ Elegir motor de voz en español.
- ⏳ Vistas de tablero en ClickUp para las dos listas.
- ⏳ Confirmar en la Ola 1 la conversión de visitas en ingresos (hipótesis en `01-flujo-clipping.md`, sección 6).
