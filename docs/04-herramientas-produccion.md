# 04 · Herramientas de producción

Catálogo de las herramientas elegidas por los socios y guía para decidir cuál usar según el
video. Datos de GitHub consultados el 2026-11-12. Los repositorios se referencian por
enlace; no se copian aquí.

Todavía no se ha instalado ni probado ninguna: los minutos por pieza y la calidad real se
medirán en la Ola 1.

## 1. Catálogo

### Corte de clips

| Herramienta | Qué hace | Costo y licencia | Notas |
|---|---|---|---|
| [Clipspeed](https://www.clipspeed.ai/) | Detecta y corta clips desde videos largos; subtítulos; publicación automática | De pago: US$19, 39 o 99 al mes; prueba de 3 días por US$1. Sin marca de agua desde US$39 (según su propio sitio, con contradicciones) | Choca con el presupuesto de US$0. Alternativa gratuita: ffmpeg + Whisper |

### Motor de composición

| Herramienta | Qué hace | Costo y licencia | Notas |
|---|---|---|---|
| [HyperFrames](https://github.com/heygen-com/hyperframes) (HeyGen) | Convierte HTML en video; pensado para que lo maneje un agente | Gratis, Apache 2.0, sin costo por render | Requiere Node.js 22+, FFmpeg y Chrome; render local |

### Estilos y recetas listas

| Herramienta | Qué hace | Licencia | Notas |
|---|---|---|---|
| [Lemo Opuscar](https://github.com/lemomo-ai/lemo-opuscar) | 99 estilos de película hechos con código, cada uno con su prompt y demo | Licencia propia: revisar antes de uso comercial | Punto de partida para definir el estilo de un canal |
| [Video ShotCraft](https://github.com/Vincentwei1021/video-shotcraft) | Skill para videos promocionales: 124 recetas de plano, sincronía con el ritmo, diseño de sonido | Apache 2.0 | Usa Remotion, cuya licencia tiene condiciones propias para empresas |
| [pixelfx](https://github.com/patch-gg/pixelfx) | 244 efectos de pixel art, más un skill para crear nuevos | MIT | Estética retro o de videojuego |
| [Claude Animation Base](https://github.com/JohnHeibel/ClaudeAnimationBase) | Kit para dibujos animados pintados a mano con p5.js; incluye un personaje con 31 emociones | MIT | El personaje incluido es ajeno: crear uno propio para un canal |

### 3D

| Herramienta | Qué hace | Licencia | Notas |
|---|---|---|---|
| [Three.js](https://github.com/mrdoob/three.js) | Biblioteca 3D para el navegador | MIT | Base de las dos siguientes |
| [React Three Rapier](https://github.com/pmndrs/react-three-rapier) | Física (colisiones, gravedad) para escenas 3D en React | MIT | Para objetos que caen, chocan o se apilan |
| [React Postprocessing](https://github.com/pmndrs/react-postprocessing) | Efectos de imagen: brillo, desenfoque, grano | MIT | Acabado visual de escenas 3D |
| [Blender MCP](https://github.com/ahujasid/mcp-for-blender) | Controla Blender desde un modelo de lenguaje | MIT | Requiere Blender instalado; el render es lento y exige buen equipo |

### Audio

| Herramienta | Qué hace | Licencia | Notas |
|---|---|---|---|
| [librosa](https://github.com/librosa/librosa) | Análisis de audio en Python: ritmo, tempo, energía | ISC | Para sincronizar cortes y animaciones con la música |

### Bibliotecas de prompts (referencia, no software)

| Recurso | Qué contiene | Licencia |
|---|---|---|
| [awesome-opus5-5-videos](https://github.com/yihui-dev/awesome-opus5-5-videos) | Videos virales hechos con código y los prompts que los generaron | MIT |
| [opus-video-prompts](https://github.com/joeseesun/opus-video-prompts) | 54 casos con prompts listos para copiar | Sin licencia declarada: usar como inspiración, no copiar textual |

## 2. Guía de selección: qué video, qué herramienta

| Tipo de pieza | Herramienta principal | Apoyo | Esfuerzo |
|---|---|---|---|
| Clip de stream subtitulado | Clipspeed, o ffmpeg + Whisper | HyperFrames para título o marco | Bajo |
| Clip con contexto (título, dato, reacción escrita) | HyperFrames | Clipspeed para el corte | Bajo–medio |
| Explicativo con gráficos 2D y texto animado | HyperFrames | Lemo Opuscar para el estilo; bibliotecas de prompts | Medio |
| Datos, rankings, comparativas (finanzas, deportes) | HyperFrames | librosa si va al ritmo de la música | Medio |
| Promocional o reseña de producto | Video ShotCraft | librosa | Medio |
| Estética retro o gamer | pixelfx | HyperFrames para componer | Bajo–medio |
| Historia con personaje animado | Claude Animation Base | Personaje propio | Alto |
| Escena 3D en navegador (objetos, física, simulaciones) | Three.js + React Three Rapier | React Postprocessing | Alto |
| 3D realista o cinematográfico | Blender MCP | — | Muy alto |
| Pieza sincronizada con música | librosa + HyperFrames | Video ShotCraft | Medio |
| Sin idea de estilo todavía | Bibliotecas de prompts y Lemo Opuscar | — | Solo exploración |

## 3. Cómo elegir

1. **Línea A (clipping):** corte + subtítulos + marco. No usar 3D ni animación: el tiempo
   por pieza manda.
2. **Línea B (original):** empezar con HyperFrames y un estilo de Lemo Opuscar. Es la
   combinación de menor esfuerzo que da identidad visual propia.
3. **Un estilo por canal.** El estilo elegido se fija en la guía del canal y no se comparte
   con otro, para cumplir la regla 16 de gobernanza.
4. **3D y Blender solo con motivo.** Se justifican si el formato del canal depende de ello y
   la capacidad lo permite.
5. **Costo por pieza.** Los estilos de esfuerzo alto solo caben en canales de baja
   frecuencia.

## 4. Advertencias

- **Uso de suscripciones.** Generar video con código consume mucho uso de Claude. Con una
  sola cuenta Pro desde diciembre, este será un límite práctico de piezas por semana;
  medirlo en la Ola 1.
- **Licencias.** Lemo Opuscar tiene licencia propia y opus-video-prompts no declara
  ninguna. Leer ambas antes de publicar piezas derivadas.
- **Remotion.** Video ShotCraft depende de Remotion, que no es código abierto pleno y pide
  licencia de pago a empresas sobre cierto tamaño. Para dos socios debería ser gratuito;
  confirmar en su licencia.
- **Equipo.** HyperFrames y Blender renderizan en el computador local: el tiempo de render
  cuenta como tiempo de producción.
- **Clipspeed.** Decisión pendiente (ver `00-decisiones-fundacionales.md`, tensión 3).

## 5. Pruebas previstas para la Ola 1

| Prueba | Qué se mide |
|---|---|
| Un clip con Clipspeed (prueba de US$1) frente a ffmpeg + Whisper | Minutos humanos, calidad de subtítulos, costo |
| Una pieza explicativa de 45 s con HyperFrames | Minutos humanos, tiempo de render, uso de Claude consumido |
| Tres estilos de Lemo Opuscar para el primer canal original | Cuál se sostiene con menos retoques |
