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
| **ffmpeg + Whisper** (en uso) | ffmpeg corta, reencuadra a vertical y quema subtítulos; Whisper transcribe el audio con marcas de tiempo | Gratis y de código abierto; corren en el computador local | Opción elegida por ahora. No detecta sola los mejores momentos: los elige un socio o un modelo de lenguaje sobre la transcripción |
| [Clipspeed](https://www.clipspeed.ai/) | Detecta y corta clips desde videos largos; subtítulos; publicación automática | De pago: US$19, 39 o 99 al mes; prueba de 3 días por US$1. Sin marca de agua desde US$39 (según su propio sitio, con contradicciones) | En reserva: se reevalúa cuando haya ingresos que lo paguen |

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

### Clipping

| Tipo de pieza | Herramienta principal | Apoyo | Esfuerzo |
|---|---|---|---|
| Clip de streamer o de noticia con el formato del canal | ffmpeg + Whisper | librosa para ubicar picos de audio | Bajo–medio |
| Plantilla animada del canal (fondo, marco, título) | HyperFrames | Se construye una vez y se reutiliza | Medio, una sola vez |

Detalle en [`05-sop/01-flujo-clipping.md`](05-sop/01-flujo-clipping.md).

### Contenido propio: familias de estilo

Cada canal original fija una familia principal; de ella sale la herramienta.

| Familia | Cómo se ve | Herramienta motor | Apoyo | Esfuerzo |
|---|---|---|---|---|
| A · Explicativo y datos | Tipografía cinética, gráficos, rankings | HyperFrames (`/style-sampling` y bloques del registro) | librosa | Medio |
| B · Cinematográfico por estilo | Acuarela, neón, noticiero, collage | Lemo Opuscar | Bibliotecas de prompts | Medio–alto |
| C · 8 bits / pixel / gamer | Pixel art y efectos de videojuego | pixelfx, compuesto en HyperFrames | librosa | Bajo–medio |
| D · Personaje animado | Dibujo pintado a mano con personaje | Claude Animation Base, con personaje propio | — | Alto |
| E · 3D en navegador | Objetos, física, simulaciones | Three.js + React Three Rapier + React Postprocessing | — | Alto |
| F · 3D realista | Escenas cinematográficas | Blender MCP | — | Muy alto |
| G · Promo de producto | Capturas reales animadas al ritmo | Video ShotCraft | librosa | Medio |

Cómo elegir la familia y los pasos de cada rama:
[`05-sop/02-flujo-contenido-original.md`](05-sop/02-flujo-contenido-original.md).

## 3. Cómo elegir

1. **Clipping:** corte + subtítulos + formato del canal. Sin 3D ni animación compleja: el
   tiempo por pieza manda.
2. **Contenido propio:** empezar por la familia A o B, que dan identidad visual con el menor
   esfuerzo.
3. **Una familia y un estilo por canal**, fijados en su biblia y no compartidos con otro
   canal (regla 16 de gobernanza).
4. **Familias D, E y F solo con motivo:** canales de baja frecuencia o piezas insignia.
5. **Probar antes de adoptar:** una pieza de prueba con el tiempo anotado.

### Notas de instalación (según los README, sin probar aún)

| Herramienta | Cómo se usa con Claude Code |
|---|---|
| HyperFrames | `claude plugin marketplace add heygen-com/hyperframes` y `claude plugin install hyperframes@hyperframes`; después `/hyperframes:hyperframes`. Trae un registro de unos 450 bloques (transiciones, títulos, subtítulos, gráficos, 3D) |
| Lemo Opuscar | `claude plugin marketplace add lemomo-ai/lemo-opuscar` y `claude plugin install lemo-opuscar@lemolab`; se pide la película nombrando el estilo. Recomienda esfuerzo alto del modelo |
| Claude Animation Base | Clonar el repositorio y pedir el video tras leer `ANIMATION_GUIDE.md`. Requiere Node.js, Chrome y ffmpeg; sin tarjeta gráfica dedicada el render es lento |
| Video ShotCraft | `npx skills add Vincentwei1021/video-shotcraft` |
| pixelfx | Biblioteca sin dependencias; incluye un skill para crear efectos nuevos |

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
- **Clipspeed.** Fuera del flujo por ahora; se trabaja solo con opciones gratuitas.
- **Selección de momentos.** Sin Clipspeed, encontrar el momento que vale la pena es trabajo manual o de un modelo sobre la transcripción. Es el paso que más tiempo puede costar en la línea de clipping.

## 5. Pruebas previstas para la Ola 1

| Prueba | Qué se mide |
|---|---|
| Un clip completo con ffmpeg + Whisper (transcribir, elegir momento, cortar, subtitular) | Minutos humanos por paso, calidad de subtítulos en español |
| Una pieza explicativa de 45 s con HyperFrames | Minutos humanos, tiempo de render, uso de Claude consumido |
| Tres estilos de Lemo Opuscar para el primer canal original | Cuál se sostiene con menos retoques |
