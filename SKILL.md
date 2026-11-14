---
name: equipo
description: Crea contigo tu propio equipo de skills de Claude Code adaptado a tu negocio, como el que usamos en Sell Your AI (una edita los reels, otra hace los carruseles, otra las miniaturas de YouTube y otra busca clientes y escribe el primer mensaje). Te pregunta qué haces y qué tareas repites cada semana, elige contigo de 2 a 4 skills, le pide ejemplos de tu estilo, escribe cada skill a medida en ~/.claude/skills/<nombre>/ con sus pasos, herramientas y reglas de calidad, la prueba con un caso real, la ajusta y te deja una carpeta «Mi equipo» con qué hace cada una y cómo llamarla. Nunca publica ni envía nada sin tu OK. Úsala cuando digan /equipo, «comenta EQUIPO», «mi equipo de skills», «crea mis skills», «quiero un equipo dentro de Claude», «no quiero contratar un editor» o «qué skills me hago para mi negocio».
---

# /equipo: tu equipo entero dentro de Claude

Una skill es un archivo `SKILL.md` dentro de `~/.claude/skills/<nombre>/` que le explica a Claude cómo hacer un
trabajo concreto, siempre igual y con tu estilo. Esta skill no hace el trabajo: **crea contigo las skills que lo
harán**, una por cada tarea que repites cada semana.

Al terminar, el usuario tiene:
- de 2 a 4 skills nuevas en `~/.claude/skills/<nombre>/SKILL.md`, probadas con un caso suyo;
- una carpeta `~/Mi-equipo/` con `EQUIPO.md` (quién es quién, qué hace cada una, cómo llamarla y qué necesita) y los
  ejemplos de estilo que ha compartido.

## Cómo hablar
- Español de España, cercano, frases cortas, sin tecnicismos. Si usas uno (ffmpeg, LUFS), explícalo en media línea.
- **Una pregunta cada vez.** Espera la respuesta antes de seguir. Si la respuesta es corta, no insistas: decide tú y
  dilo.
- No inventes cifras ni resultados («te ahorrará X horas»). Si quieres hablar de tiempo, pregúntale cuánto le lleva hoy.
- **Nunca publiques, subas ni envíes nada** (posts, emails, mensajes, repos) sin un «sí» explícito del usuario para esa
  pieza concreta. Esto también va escrito dentro de cada skill que crees.
- No toques skills que ya tenga. Si un nombre ya existe en `~/.claude/skills/`, propón otro (`editor-2`, `mis-reels`…).

## Paso 1. Qué haces y qué repites
Pregunta, de una en una:
1. «¿A qué te dedicas y a quién vendes?» (una o dos frases bastan; si tiene web o Instagram, que lo pegue y léelo).
2. «¿Qué tareas haces cada semana que te gustaría quitarte de encima?» Dale ideas si se queda en blanco:
   editar reels, carruseles, miniaturas de YouTube, buscar clientes y escribir el primer mensaje, propuestas o
   presupuestos, contestar emails, resúmenes de llamadas, informes para clientes, guiones, facturas.
3. Por cada tarea que diga: «¿Cuánto te lleva hoy y quién la hace?» (para priorizar, no para prometer nada).

Resume en 4-5 líneas lo que has entendido y espera su visto bueno.

## Paso 2. Elegir el equipo (2-4 skills)
Propón de 2 a 4 skills, la más útil primero. Para cada una: nombre corto en minúsculas y sin tildes (será el
comando, p. ej. `/reels`), qué hace en una frase y qué le pasará él (un vídeo, una idea, una web…).
Criterio: tarea que repite mucho, con un resultado que se puede revisar y que Claude puede hacer en su ordenador.
Si pide más de 4, empieza por 4 y deja el resto apuntado en `EQUIPO.md` como «Siguientes».
Espera que elija o cambie.

## Paso 3. Crear cada skill a medida (una detrás de otra)
Para cada skill elegida, en este orden:

### 3.1 Su estilo
Pide ejemplos, de uno en uno:
- **Vídeo**: 2-3 reels que le gusten (suyos o de otros): enlace o archivo. Pregunta formato (vertical 9:16, horizontal,
  cuadrado), subtítulos (sí/no, estilo), música (suya / sin) y si sale él a cámara.
- **Carruseles**: 2-3 carruseles que le gusten, sus colores, su tipografía y su logo si tiene.
- **Miniaturas**: 2-3 miniaturas que le gusten y si sale él (si sale, que aporte sus propias fotos; nunca uses la cara
  de otra persona).
- **Buscar clientes**: su web, su cliente ideal, zona e idioma, y un mensaje que ya haya mandado y le funcione.
- **Textos (propuestas, emails, guiones)**: 2-3 textos suyos para sacar su tono.

Si puedes, mira los ejemplos de verdad (WebFetch, una skill de ver vídeos si la tiene, o capturas que te pase) y
resume el estilo en 5 líneas: ritmo, tamaños, colores, tono, qué evita. Guarda los ejemplos y ese resumen en
`~/Mi-equipo/estilos/<nombre>/`. Enséñale el resumen y espera su OK.

### 3.2 Herramientas
Mira qué tiene instalado (`which ffmpeg node python3`, `python3 -c "import faster_whisper"`…) y dile en una línea qué
falta y para qué. Instala solo con su sí. Herramientas habituales:
- **Vídeo**: `ffmpeg` (cortar, montar, sonido), `faster-whisper` (transcribir en local, gratis), Node.js +
  `playwright` (pintar subtítulos y gráficos con HTML).
- **Carruseles y miniaturas**: `playwright` o `Pillow` (montar las imágenes a su tamaño: 1080×1350 carrusel,
  1280×720 miniatura). Generar imágenes con IA es opcional: solo si ya tiene un servicio y una clave propia, y avisando
  antes de lo que cuesta.
- **Buscar clientes**: búsqueda web (WebSearch/WebFetch) y, si hace falta, Playwright MCP
  (`claude mcp add playwright -- npx @playwright/mcp@latest`) para páginas públicas. Gmail solo para dejar borradores
  o enviar con su aprobación.

### 3.3 Escribir el SKILL.md
Crea `~/.claude/skills/<nombre>/SKILL.md` con esta forma (ver el ejemplo en `DOCUMENTO.md`):
1. **Frontmatter**: `name: <nombre>` y `description:` en una sola línea con qué hace, qué recibe, qué entrega y
   frases con las que se dispara («/<nombre>», «edítame este reel», etc.). Es lo que Claude lee para saber cuándo usarla.
2. **Qué entrega** y dónde lo deja (una carpeta de proyecto por trabajo).
3. **Su estilo**: el resumen del paso 3.1 y la ruta a `~/Mi-equipo/estilos/<nombre>/`.
4. **Pasos** numerados, cortos, con los comandos concretos.
5. **Reglas de calidad** (las de abajo según el tipo, más las que pida él).
6. **Revisión antes de entregar**: qué mirar (fotogramas, la imagen a tamaño real, el CSV) y enseñárselo.
7. **Línea roja**: «No publiques, subas ni envíes nada sin el OK del usuario para esa pieza».

Si la skill necesita scripts (p. ej. quitar silencios), escríbelos en `~/.claude/skills/<nombre>/scripts/`, cortos y
comentados, y que el SKILL.md diga cómo llamarlos.

**Reglas de calidad para vídeo** (meterlas siempre en una skill de edición):
- Cortes solo en silencio real: ninguna palabra cortada, ni la primera sílaba ni la última consonante. No fiarse solo
  del tiempo que da Whisper: buscar el final real con la energía del audio y dejar 80-120 ms de margen.
- Quitar trabas y tomas repetidas (quedarse con la última buena) y muletillas largas.
- Ningún silencio de más de 0,25 s dentro del montaje (solo un respiro breve al final). Comprobarlo con un script
  después de montar y arreglarlo sin esperar a que lo vea el usuario.
- Subtítulos palabra a palabra, sincronizados, en la zona segura de Instagram (en vertical 1080×1920: nada en los
  ~250 px de arriba, nada por debajo de ~1500 px y nada pegado a la derecha, donde van los botones), y nunca encima
  de la cara.
- Música bajo la voz (que la voz se entienda siempre) y el resultado final a −14 LUFS. Solo música que el usuario
  tenga derecho a usar.
- Colores naturales; mirar fotogramas de los momentos clave antes de entregar.

**Reglas de calidad para carruseles y miniaturas**:
- De una referencia se copia la estructura y la idea, nunca el texto ni las imágenes de otro.
- Una idea por slide, legible en 2 segundos; la miniatura se tiene que leer a tamaño pequeño (unos 320 px de ancho).
- El texto con letras se monta por código, no lo escribe la IA dentro de la imagen.
- Solo su cara o la de quien haya dado permiso; nada de logos o marcas ajenas sin motivo.

**Reglas de calidad para buscar clientes**:
- Solo datos públicos de negocios y profesionales; nada de perfiles privados, menores ni datos sensibles.
- Solo el email que el propio negocio publica para que le escriban (web, perfil, Google). Nunca adivinar ni comprar
  emails.
- Cada problema o frase del cliente, con su cita literal y el enlace; si no hay cita, no hay punto.
- Primer mensaje corto, con sus palabras, quién eres, por qué le escribes y cómo darse de baja.
- **Nunca enviar sin aprobación**, mensaje a mensaje. Respetar el RGPD y la LSSI y llevar una lista de no contactar.
- Si quiere algo ya hecho, la nuestra es pública:
  https://github.com/deniscorral3am/buscador-de-clientes-skill

**Reglas para textos (propuestas, emails, guiones)**: su tono (sacado de sus ejemplos), sin inventar cifras ni casos,
lo que falte entre [corchetes] para que lo rellene él.

## Paso 4. Probar y ajustar
Con cada skill recién creada:
1. Pídele un caso real (un vídeo en bruto, un tema de carrusel, el título de un vídeo, su web…).
2. Llama a la skill como lo haría él (`/<nombre>`) y sigue sus pasos de verdad.
3. Enséñale el resultado y pregunta: «¿Qué cambiarías?».
4. Cada cosa que diga se convierte en una regla dentro del SKILL.md (no solo se arregla esta vez). Repite hasta que le
   valga, como mucho 3 vueltas por skill en esta sesión; lo que quede, apúntalo en `EQUIPO.md` como pendiente.

## Paso 5. La carpeta «Mi equipo»
Crea `~/Mi-equipo/EQUIPO.md` con:
- una tabla: skill · qué hace · cómo llamarla (`/<nombre>` y una frase de ejemplo) · qué le pasas · dónde deja el
  resultado;
- herramientas instaladas y lo que falta;
- pendientes y «Siguientes» skills;
- cómo mejorarlas: «cuando algo no te guste, dile a Claude "añade esta regla a /<nombre>"».

Abre la carpeta (`open ~/Mi-equipo` en Mac) y despídete con la tabla en el chat y un recordatorio: cada skill mejora
cada vez que le corriges algo.

## Lo que nunca hace esta skill
- Publicar, subir, enviar o programar nada sin el OK del usuario.
- Pedir o guardar contraseñas; las claves de servicios, solo en variables de entorno o archivos `.env` suyos.
- Copiar la cara, la voz, los textos o los datos de otra persona.
- Prometer resultados o cifras.
