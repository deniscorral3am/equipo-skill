# Tu equipo dentro de Claude

La guía de las skills que usamos (editor de reels, carruseles, miniaturas y buscador de clientes) y la skill de Claude
Code que crea contigo tu propio equipo de skills, adaptado a tu negocio.

| Parte | Qué tienes |
|---|---|
| El equipo que usamos | Las 4 skills explicadas: qué hacen y qué les pides |
| Una skill por dentro | Un `SKILL.md` de ejemplo, corto y comentado |
| Crea la tuya | Los pasos para montar tu primera skill en 10 minutos |
| La skill `/equipo` | Te pregunta qué haces, elige contigo de 2 a 4 skills, las crea con tu estilo, las prueba y te deja la carpeta «Mi equipo» |
| El buscador de clientes | Enlace a la skill pública: [buscador-de-clientes-skill](https://github.com/deniscorral3am/buscador-de-clientes-skill) |
| El prompt | Para pegarlo en Claude Code sin instalar nada |

Hecho por Denís Corral · [@deniscorralvillarraso](https://instagram.com/deniscorralvillarraso) · [Sell Your AI](https://sellyourai.io)

## Cómo usarlo

- **Solo leer:** abre [`DOCUMENTO.md`](DOCUMENTO.md). Al final está el prompt para pegar en Claude Code.
- **Como skill de Claude Code:**

  ```bash
  git clone https://github.com/deniscorral3am/equipo-skill ~/.claude/skills/equipo
  ```

  Abre Claude Code y escribe `/equipo`.

Según las skills que elijas, te pedirá instalar `ffmpeg`, Python 3 con `faster-whisper` o Node.js con `playwright`
(siempre con tu permiso). Nunca publica ni envía nada sin tu OK.

## Licencia

MIT
