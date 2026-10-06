# Guía: tu equipo de 4 Bots para conseguir clientes con Grok Bot

Por **Manuel Valenzuela** ([@ingemanu](https://www.tiktok.com/@ingemanu)). Salió del taller que di en el **Grok Bot Guatemala Meetup**, en la UFM, el 3-oct-2026, organizado con Open2.

🎥 Charla completa: https://www.youtube.com/watch?v=Rml74uyvtqE&t=8141s

> ⚠️ Grok Bot está en beta: botones, nombres y límites pueden cambiar. Guía revisada el 6-oct-2026.
>
> **[Lo probé]** / **[No lo probé]** indica si yo corrí ese prompt en Grok Bot. Los prompts de esta guía están marcados **[No lo probé]**: úsalos como punto de partida y ajústalos.

Vas a armar un mini equipo de ventas con Grok Bot. Mi ejemplo: *restaurantes de Zona 10 sin página web.* Tú eliges tu nicho: dentistas, gimnasios, talleres, salones… **Es un simulacro: no se contacta a nadie.**

| Bot | Su trabajo | Entrega |
|---|---|---|
| 🔎 Scout | Encuentra negocios de tu nicho | `prospectos.csv` |
| 📊 Analista | Les pone puntaje de oportunidad | `calificados.csv` |
| 🛠️ Builder | Hace una página de demostración para el #1 | `landing.html` |
| ✉️ SDR | Escribe borradores de mensaje (no se envían) | `outreach.md` |

## Antes de empezar
1. Abre Grok Bot, inicia sesión y revisa tus créditos.
2. Anota tus variables: **[NICHO]** (ej.: *dentistas*), **[ZONA]** (ej.: *Zona 10, Ciudad de Guatemala*) y **[CANTIDAD]** (empieza con 3, máximo 5).
3. Crea los 4 Bots y pega su **description** ([Anexo A](#anexo-a--los-4-bots-descriptions-y-prompts)). ¿Pocos créditos? Usa el "Plan ahorro" (un solo Bot).

## Los 4 pasos
En el chat de cada Bot pega el prompt de su paso: **1. Scout** descubre → **2. Analista** califica → **3. Builder** construye (abre la vista previa) → **4. SDR** escribe los borradores. Si aparece **Send / Discard**, presiona **Discard**. Los Bots comparten la carpeta `/workspace`, así que cada uno lee el archivo del anterior.

## Para que te alcancen los créditos
Máximo 5 negocios · pide **búsqueda web o plugins**, no capturas de pantalla · salida en **tabla o CSV con links** · una sola landing · si el Bot da vueltas, **detenlo**.

## Reglas éticas
- **Solo información pública de negocios:** nada de datos personales, nada detrás de un login, nada en masa.
- **No se envía nada:** siempre das **Discard**. En la vida real: un mensaje honesto, fácil de rechazar, y si te dicen que no, respeta el no.
- **La landing es una demo:** dice que no es oficial y no se publica a nombre del negocio.
- **Verifica:** la IA inventa. Cada dato con su link; la responsabilidad es tuya.

## Si algo falla
| Pasa esto | Haz esto |
|---|---|
| CAPTCHA | No lo saltes. Escribe: *"Deja ese sitio y usa solo búsqueda web."* |
| Te pide login | No pongas contraseñas. Escribe: *"Sin login: solo páginas públicas."* |
| Bucle | **Stop** y luego: *"Para. Dime en 3 líneas qué tienes y qué falta."* Baja [CANTIDAD] o abre un chat nuevo. |
| Se acabó la cuota o no responde | Espera 1 minuto y reintenta una vez; si no, usa el [Anexo B](#anexo-b--versión-sin-grok-bot-para-cualquier-chat-de-ia) en cualquier chat de IA. |
| Inventa datos | *"Pon el link de cada dato; si no lo encontraste, escribe 'no encontrado'."* |

---

## Anexo A — Los 4 Bots (descriptions y prompts)

Reemplaza [NICHO], [ZONA] y [CANTIDAD] con lo que anotaste.

> 💡 **Plugins:** si en el Marketplace ves un plugin de búsqueda (Exa, Tavily o Firecrawl), conéctalo al Scout. Si te pide crear otra cuenta, sáltalo; el Bot puede usar el buscador normal.

> 💡 **Plan ahorro (un solo Bot):** crea un Bot llamado "Equipo de ventas", pega las 4 descriptions juntas en su description y luego usa los 4 prompts en orden, en el mismo chat.

### 🔎 Bot 1: Scout

**Description (reglas permanentes)** [No lo probé]
```
Eres Scout, investigador de prospectos para un ejercicio de práctica.
Reglas:
- Solo usas información pública de NEGOCIOS (nunca datos personales ni nada detrás de un login).
- Prefieres búsqueda web o plugins de búsqueda. No tomas capturas de pantalla ni navegas Google Maps salvo que te lo pida.
- Nunca buscas más de 5 negocios.
- Cada dato lleva un link como evidencia. Si no lo encuentras, escribes "no encontrado". Nunca inventas.
- Si ves un CAPTCHA o te piden login, te detienes y me avisas.
- Respuestas cortas: tabla + archivo CSV en /workspace.
```

**Prompt del paso 1: Descubrir** [No lo probé]
```
Encuentra [CANTIDAD] [NICHO] en [ZONA], Guatemala, que probablemente NO tengan página web propia. Usa búsqueda web.
Para cada uno captura:
nombre | link_maps | tiene_web (sí/no + link) | menu_o_catalogo_en_linea (sí/no + link) | redes_y_contacto_publico (Instagram, Facebook, WhatsApp o teléfono del negocio) | logo_o_fotos (link) | fuente
Para link_maps no abras Maps: arma el link así: https://www.google.com/maps/search/?api=1&query=NOMBRE+[ZONA]
Guarda todo en /workspace/prospectos.csv y muéstrame la tabla. Detente al llegar a [CANTIDAD].
```

### 📊 Bot 2: Analista

**Description (reglas permanentes)** [No lo probé]
```
Eres Analista. Calificas prospectos con un puntaje simple y explicas por qué.
Reglas:
- Trabajas con /workspace/prospectos.csv. Solo buscas en la web para confirmar un dato dudoso, nunca para buscar negocios nuevos.
- Cada señal que marques lleva su link de evidencia. Si no hay evidencia, la señal vale 0.
- No tomas capturas de pantalla.
- Respuestas cortas: tabla + CSV en /workspace.
```

**Prompt del paso 2: Calificar** [No lo probé]
```
Lee /workspace/prospectos.csv y califica cada negocio de 0 a 10 con estas señales de oportunidad:
+3 no tiene página web propia
+2 no tiene menú, catálogo o precios en línea
+2 sus redes tuvieron actividad en los últimos 30 días (está vivo y le importa lo digital)
+2 tiene buenas reseñas (4.2 o más)
+1 tiene un contacto público de negocio
Agrega las columnas: puntaje | señales | evidencia (links) | por_que_ahora (1 frase).
Ordena de mayor a menor, guarda /workspace/calificados.csv y muéstrame la tabla.
```

### 🛠️ Bot 3: Builder

**Description (reglas permanentes)** [No lo probé]
```
Eres Builder. Haces landing pages de DEMOSTRACIÓN para un ejercicio de práctica.
Reglas:
- Usas solo información pública que esté en /workspace/calificados.csv. Si falta algo, pones un texto de ejemplo entre [corchetes]; nunca inventas precios, horarios ni reseñas.
- Un solo archivo HTML, simple, que se vea bien en celular.
- No descargas fotos del negocio: usas espacios grises con la frase "foto aquí" o enlazas el logo público.
- Arriba de la página siempre va este aviso: "Demo no oficial. No está afiliada a este negocio."
- No publicas nada en internet. Solo vista previa.
```

**Prompt del paso 3: Construir** [No lo probé]
```
Toma el negocio #1 de /workspace/calificados.csv y crea /workspace/landing.html con:
1) encabezado con nombre y una frase de lo que ofrece, 2) botón de WhatsApp o llamada si hay contacto público, 3) sección de menú, servicios o catálogo (lo público o de ejemplo), 4) ubicación con el link de Maps, 5) links a sus redes.
Muéstrame la vista previa. Un solo intento; yo te pido cambios si hacen falta.
```

¿Quieres una página más trabajada? En [`templates/`](templates/) hay 3 plantillas HTML para restaurantes con un bloque editable.

### ✉️ Bot 4: SDR

**Description (reglas permanentes)** [No lo probé]
```
Eres SDR. Escribes BORRADORES de mensajes de primer contacto para un ejercicio de práctica.
Reglas:
- NUNCA envías nada. Nunca presionas Send. Todo queda como borrador o en un archivo.
- Tono amable, corto, sin presión y sin exagerar. Solo mencionas datos con evidencia en /workspace/calificados.csv.
- Cada mensaje ofrece una salida fácil (por ejemplo, "si no te interesa, no hay problema").
- Firmas como [TU NOMBRE].
```

**Prompt del paso 4: Preparar el mensaje** [No lo probé]
```
Para los 3 primeros de /workspace/calificados.csv escribe:
- un WhatsApp de máximo 60 palabras,
- un email de máximo 120 palabras con un asunto corto.
Personalízalos con 1 dato real del negocio (con evidencia) y menciona que preparé una demo de su página.
Guarda todo en /workspace/outreach.md y muéstramelo. NO envíes nada.
```
➡️ Si Grok Bot te muestra un borrador con **Send / Discard**, presiona **Discard**.

---

## Anexo B — Versión "sin Grok Bot" (para cualquier chat de IA)

Sirve en Grok, ChatGPT, Claude, Gemini o el que uses. Mismo patrón: un solo chat hace los 4 papeles, uno tras otro. Si tu chat no busca en internet, activa la búsqueda web o pega tú los links que encontraste en Google Maps.

**0. Contexto (pégalo primero)** [No lo probé]
```
Vamos a practicar un proceso de ventas en 4 pasos. Es un simulacro: no se contactará a nadie.
Reglas: solo información pública de negocios; máximo 5 negocios; cada dato con un link de evidencia o "no encontrado"; nunca inventes; respuestas cortas en tabla.
Mi nicho es [NICHO], en [ZONA], Guatemala. Responde solo "Listo".
```

**1. Descubrir** [No lo probé]
```
Busca en la web [CANTIDAD] [NICHO] en [ZONA] que probablemente no tengan página web propia.
Dame una tabla: nombre | link_maps | tiene_web (sí/no + link) | menú o catálogo en línea (sí/no + link) | redes y contacto público del negocio | logo o fotos (link) | fuente.
Para link_maps usa: https://www.google.com/maps/search/?api=1&query=NOMBRE+[ZONA]
```

**2. Calificar** [No lo probé]
```
Califica cada negocio de la tabla de 0 a 10: +3 sin web, +2 sin menú o catálogo en línea, +2 redes activas en los últimos 30 días, +2 reseñas de 4.2 o más, +1 contacto público.
Agrega: puntaje | señales | evidencia | por qué ahora (1 frase). Ordena de mayor a menor.
```

**3. Construir** [No lo probé]
```
Con la información pública del negocio #1, escribe un solo archivo HTML de landing de demostración, que se vea bien en celular: nombre y frase, botón de WhatsApp o llamada, menú o servicios, ubicación (link de Maps) y redes.
Arriba debe decir: "Demo no oficial. No está afiliada a este negocio."
No inventes precios, horarios ni reseñas: usa [texto de ejemplo]. Usa espacios grises que digan "foto aquí".
```
➡️ Copia el código en un archivo `landing.html` y ábrelo con tu navegador. Algunos chats también muestran la vista previa directamente.

**4. Preparar el mensaje** [No lo probé]
```
Para los 3 primeros escribe un WhatsApp (máx. 60 palabras) y un email (máx. 120 palabras, con asunto).
Tono amable y sin presión, 1 dato real del negocio, menciona la demo y ofrece una salida fácil. Firma: [TU NOMBRE]. Son solo borradores.
```

---

## Anexo C — Adapta el patrón a tu negocio (7 pasos)

Este flujo sirve para casi cualquier negocio que vende a otros negocios. Grok Bot es el vehículo; el patrón es tuyo.

1. **Define a quién le quieres vender.** Nicho + zona + una frase: "negocios que ___ y necesitan ___".
2. **Decide qué datos necesitas de cada uno.** Pocas columnas, las que de verdad usarías para decidir.
3. **Descubre pocos, con evidencia.** Empieza con 5. Solo fuentes públicas, con un link en cada dato.
4. **Califica con señales claras.** De 3 a 5 señales con puntos. Si no puedes explicar el puntaje, la señal no sirve.
5. **Crea algo de valor antes de pedir nada.** Una demo, un mini diagnóstico, una idea concreta para ese cliente.
6. **Prepara el mensaje, pero decide tú.** La IA hace el borrador; tú revisas, corriges y decides si envías y cuándo.
7. **Mide, ajusta y repite.** Mira qué funcionó, mejora las reglas de tus Bots y, cuando el proceso esté probado, conviértelo en una rutina.

---

## Anexo D — Variante con un Bot capitán (Lionel) [No lo probé]

En vez de crear 4 Bots a mano, creas uno solo, **Lionel**, que arma su equipo: Di María busca leads, Riquelme hace la landing y Julián escribe el email. Viene configurado para restaurantes de Zona 10; edita `skills/buscar-leads/SKILL.md` para tu nicho.

1. Crea un Bot y pega [`prompts/lionel-description.txt`](prompts/lionel-description.txt) en **Edit Profile → Description**. Avatar opcional: [`assets/lionel.png`](assets/lionel.png).
2. Pídele que guarde las 4 skills de [`skills/`](skills/): `Guarda esto como skill privada llamada "<nombre>".` y pega cada `SKILL.md`.
3. Un mensaje por paso, esperando su respuesta:
   ```
   Lionel, arma el equipo.
   ```
   ```
   Lionel, paso 1: que Di María busque 5 leads.
   ```
   ```
   Lionel, paso 2: que Riquelme haga la landing del #1 y la publique.
   ```
   ```
   Lionel, paso 3: que Julián escriba el email del #1. Me presento así: [quién eres en una línea].
   ```

Riquelme publica la demo de forma temporal (Cloudflare o here.now) con banda "Demo no oficial" y `noindex`. El claim URL de la página es tuyo: no lo muestres. Los archivos `SKILL.md` también funcionan en otros agentes que leen skills.

## Qué hay en este repo

| Carpeta | Contenido |
|---|---|
| `prompts/` | Description de Lionel |
| `skills/` | `armar-equipo`, `buscar-leads`, `hacer-landing`, `escribir-email` |
| `templates/` | Plantillas de landing para restaurantes: `comal`, `mantel`, `barra` ([cómo usarlas](templates/README.md)) |
| `assets/` | Avatares de Lionel, Di María, Riquelme y Julián |

---

Texto bajo [CC BY 4.0](LICENSE). Si lo usas o lo mejoras, cuéntame: [TikTok @ingemanu](https://www.tiktok.com/@ingemanu) · [X @vm623_](https://x.com/vm623_)
