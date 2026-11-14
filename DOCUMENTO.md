# El equipo que usamos

Ibas a contratar un editor en Fiverr. Antes, mira esto: en nuestra carpeta de skills de Claude hay un equipo entero.
Una edita todos los reels, otra hace los carruseles, otra las miniaturas de YouTube y otra busca clientes en redes y
escribe el primer mensaje, que aprobamos antes de enviar.

Aquí tienes qué hace cada una, cómo es una skill por dentro y cómo crear la tuya. Las nuestras llevan nuestros datos,
nuestra marca y nuestra cara, así que no las compartimos tal cual (salvo la de buscar clientes, que es pública). Lo
que sí te damos es la skill `/equipo`, que crea **contigo** las tuyas, adaptadas a tu negocio.

---

## 1. Qué es una skill

Una skill es una carpeta dentro de `~/.claude/skills/` con un archivo `SKILL.md`. Ese archivo le explica a Claude
Code cómo hacer un trabajo concreto: qué recibe, qué pasos sigue, qué herramientas usa, qué reglas de calidad cumple y
qué entrega. Escribes `/nombre` (o lo pides con tus palabras) y Claude lo hace siempre igual, con tu estilo.

La diferencia con un prompt suelto: la skill **aprende**. Cada vez que corriges algo, se añade como regla y no vuelve
a pasar.

---

## 2. Las 4 skills que usamos

### El editor (`/editor`)
**Qué hace:** le pasas el vídeo en bruto (o solo tu voz) y te lo devuelve listo para publicar.
- Transcribe en tu ordenador con Whisper y marca lo que sobra: arranques fallidos, frases repetidas (se queda con la
  última toma buena) y muletillas.
- Corta solo en silencio real, sin comerse ninguna palabra, ni la primera sílaba ni la última letra.
- Quita los huecos: ningún silencio de más de 0,25 s dentro del montaje.
- Pasa a vertical, ajusta el color, pone subtítulos palabra a palabra en la zona segura de Instagram (sin tapar la
  cara ni quedar debajo de los botones), títulos y gráficos sincronizados con lo que dices.
- Mete música por debajo de la voz y deja el volumen final a −14 LUFS (el nivel estándar de las redes).
- Antes de entregar, mira fotogramas de los momentos clave.

**Qué le pides:** «edítame este vídeo», «quítale los silencios», «ponle subtítulos y música», «hazlo como este reel».

**Herramientas:** ffmpeg, faster-whisper, Node.js con Playwright. Todo en local, sin pagar por minuto.

### El carrusel (`/carrusel`)
**Qué hace:** le pasas el enlace de un carrusel que funciona y hace uno nuevo para tu marca.
- Le hace rayos X a la referencia: gancho, palanca (curiosidad, contraste, lista…), estructura y CTA.
- Te propone ángulos sacados de tu negocio y escribe el texto con tu voz, una idea por slide.
- De la referencia coge la estructura, **nunca el texto ni las imágenes**.
- Genera las fotos (con tu cara, si quieres salir) y monta las slides a 1080×1350 con tu tipografía y tus colores.
  Lo que lleva letras se monta por código, porque la IA las estropea.
- Te enseña la hoja con todas las slides antes de nada.

**Qué le pides:** «hazme un carrusel como este» + el enlace.

### El miniaturero (`/miniaturero`)
**Qué hace:** miniaturas de YouTube en 4K (y su copia a 1280×720) en estilos que ya hemos probado: texto grande
detrás de la persona, una tele o pantalla con un titular, un escenario o una pizarra.
- Si le pasas el vídeo, lo transcribe y te propone 2-3 titulares de 2 a 4 palabras.
- Genera la escena con IA, pone la cara real (a partir de tus fotos) y monta el texto por código.
- Revisa que la cara se parezca, que el texto no tape la frente y que se lea en pequeño.

**Qué le pides:** «hazme una miniatura para este vídeo» o el título del vídeo.

### El buscador de clientes (`/buscador-de-clientes`) · pública
**Qué hace:** le pegas tu web y te deja una lista de clientes potenciales con el primer mensaje escrito.
- Deduce tu cliente ideal de tu web y te lo enseña para que lo apruebes.
- Busca perfiles y negocios públicos que encajan (Instagram, LinkedIn, TikTok, YouTube, Reddit, foros, reseñas, webs).
- Monta la ficha de cada uno con sus problemas, lo que sueña y sus objeciones, **citando sus palabras exactas con el
  enlace**.
- Solo usa el email que el propio negocio publica para que le escriban.
- Escribe el primer mensaje con sus palabras y **solo lo envía cuando tú apruebas cada uno**, respetando el RGPD y la
  LSSI. Todo queda en un CSV.

**Qué le pides:** «búscame clientes» + tu web.

**Descárgala:** https://github.com/deniscorral3am/buscador-de-clientes-skill

---

## 3. Cómo se ve una skill por dentro

Un ejemplo corto y genérico (una skill que quita silencios a un vídeo):

````markdown
---
name: silencios
description: Quita los silencios y las tomas repetidas de un vídeo sin cortar ninguna palabra y lo deja listo para revisar. Úsala cuando diga /silencios, «quítale los silencios a este vídeo» o pase un MP4 para limpiar.
---

# /silencios

Entrega: `<nombre>-limpio.mp4` en una carpeta nueva junto al vídeo.

## Pasos
1. Transcribe el vídeo con faster-whisper (palabra a palabra, con tiempos).
2. Marca lo que sobra: arranques fallidos, frases repetidas (quédate con la última buena) y silencios.
3. Corta con ffmpeg solo en silencio real, con 80-120 ms de margen alrededor de cada palabra.
4. Comprueba que no queda ningún silencio de más de 0,25 s. Si queda, arréglalo.
5. Saca 4 fotogramas de los cortes y míralos.

## Reglas
- Ninguna palabra cortada, ni al principio ni al final.
- Si dudas en un corte, escucha esa ventana antes de cortar.

## Antes de entregar
Enséñale al usuario la lista de cortes y el vídeo. No lo publiques ni lo subas a ningún sitio.
````

Lo importante:
- **`description`**: es lo que lee Claude para saber cuándo usarla. Pon qué hace, qué recibe y las frases con las
  que la pedirás.
- **Pasos** cortos y en orden.
- **Reglas**: cada fallo que corriges se convierte en una regla.
- **Revisión y línea roja**: qué mirar antes de entregar y nada sale sin tu OK.

---

## 4. Crea la tuya en 10 minutos

1. **Instala la skill `/equipo`:**
   ```bash
   git clone https://github.com/deniscorral3am/equipo-skill ~/.claude/skills/equipo
   ```
2. **Abre Claude Code y escribe `/equipo`.**
3. **Contesta sus preguntas** (de una en una): a qué te dedicas y qué tareas repites cada semana.
4. **Elige de 2 a 4 skills** de las que te propone (editar reels, carruseles, miniaturas, buscar clientes,
   propuestas…).
5. **Pásale ejemplos de tu estilo:** 2-3 reels, carruseles o miniaturas que te gusten y algún texto tuyo para el tono.
6. **Pruébala con un caso real** y dile qué cambiarías. Cada corrección queda como regla.
7. **Mira tu carpeta `~/Mi-equipo/`:** ahí tienes qué hace cada skill y cómo llamarla.

La primera skill es la que más cuesta. Las siguientes van más rápido porque Claude ya conoce tu negocio y tu estilo.

---

## 5. El prompt

Si prefieres no instalar nada, pega esto en Claude Code:

```text
Quiero montar mi propio equipo de skills de Claude Code para mi negocio, como un equipo que me quite el trabajo que
repito cada semana. Hazme las preguntas de una en una y en español de España:

1. Pregúntame a qué me dedico y a quién vendo (si te paso mi web o mi Instagram, léelos).
2. Pregúntame qué tareas repito cada semana (editar reels, carruseles, miniaturas de YouTube, buscar clientes y
   escribir el primer mensaje, propuestas, emails…) y cuánto me llevan hoy.
3. Propónme de 2 a 4 skills, la más útil primero, con un nombre corto (será el comando) y qué hace cada una.
   Espera a que elija.
4. Para cada skill elegida:
   - pídeme 2-3 ejemplos de mi estilo (reels, carruseles, miniaturas o textos que me gusten) y resúmeme el estilo
     en 5 líneas;
   - mira qué herramientas tengo (ffmpeg, faster-whisper, Node.js, playwright…) e instala solo con mi permiso;
   - crea ~/.claude/skills/<nombre>/SKILL.md con frontmatter (name y description en una línea con disparadores),
     qué entrega, mi estilo, pasos numerados, reglas de calidad y revisión antes de entregar.
   Reglas de calidad mínimas:
   - Vídeo: cortes sin comerse ninguna palabra, ningún silencio de más de 0,25 s, subtítulos en la zona segura de
     Instagram sin tapar la cara, música bajo la voz y volumen final a −14 LUFS.
   - Carruseles y miniaturas: de una referencia solo la estructura, nunca su texto ni sus imágenes; texto montado por
     código; que se lea en pequeño.
   - Buscar clientes: solo datos públicos, solo el email que publica el propio negocio, citas literales con enlace,
     nunca enviar sin mi aprobación mensaje a mensaje, RGPD y LSSI.
5. Prueba cada skill con un caso real mío, enséñame el resultado y convierte cada corrección en una regla del SKILL.md.
6. Déjame una carpeta ~/Mi-equipo/ con EQUIPO.md: qué hace cada skill, cómo llamarla, qué le paso y dónde deja el
   resultado.

Nunca publiques, subas ni envíes nada sin mi OK. No inventes cifras ni resultados.
```

---

Hecho por Denís Corral · [@deniscorralvillarraso](https://instagram.com/deniscorralvillarraso) ·
[Sell Your AI](https://sellyourai.io)
