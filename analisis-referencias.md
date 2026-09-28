# Análisis de referencias — Página de Participación / Consultas Públicas

Notas de análisis (sin implementación) para construir una página de **consultas públicas** con la
lógica funcional de Ministerio Abierto (GBA) pero con la estética visual del sitio del CAM
(Municipalidad de La Plata).

---

## 1. Referencia funcional: Ministerio Abierto — Consultas Públicas

URL listado: https://ministerioabierto.minfra.gba.gob.ar/consultas-publicas
URL detalle: https://ministerioabierto.minfra.gba.gob.ar/consultas/consulta-mercedes-paseo-parque-independencia

### 1.1 Página de listado (`/consultas-publicas`)

**Header institucional**
- Logo "Ministerio Abierto" + logo del Ministerio + escudo de la Provincia (3 marcas alineadas a la izq).
- Nav: Inicio / Participá (dropdown) / Más información (dropdown).
- Acciones a la derecha: toggle modo oscuro, "Iniciar sesión", botón de menú hamburguesa.

**Hero**
- Fondo con gradiente/imagen abstracta (tonos violeta-celeste-rosa, efecto "vidrio/facetado").
- Ícono de personas en atril (participación) centrado.
- Título "Consultas públicas" + bajada explicativa (1-2 líneas).

**Bloque explicativo (fondo oscuro)**
- 3 párrafos: qué es una consulta pública, objetivo, beneficios.
- 5 acordeones (FAQ tipo collapse):
  - ¿Cómo funcionan?
  - ¿Qué asuntos pueden tratarse?
  - ¿Qué asuntos no pueden tratarse?
  - ¿Cómo participar?
  - ¿Qué ocurre después de la consulta?

**Listado + filtros (sidebar izquierda tipo faceted search)**
- Filtro "Estado": Todas / Participación programada / Participación abierta / Instancia participativa finalizada.
- Filtro "Ejes de gestión" (categorías temáticas, ej. Gestión Integrada del Recurso Hídrico, Conectividad y logística, Energía, Infraestructura de Ciudades, Infraestructura del Cuidado).
- Filtro "Etiquetas" (multi-select largo: organismos, localidades, préstamos/financiamiento, temas).
- Buscador de texto libre ("Buscar por título o descripción").
- Resultado: grilla/lista de **cards tipo artículo**, cada una con:
  - Imagen de portada.
  - Badge de estado ("Instancia participativa finalizada", etc.).
  - Título (link a detalle).
  - Fecha/modalidad (ej. "Miércoles 26 de agosto de 2026 - Presencial").
  - Categoría/sección.
  - Eje de gestión.
  - Chips de etiquetas (organismo, localidad, préstamo).
  - Rango de fechas de participación ("19/08/2026 – 01/09/2026").
- Mensaje de estado vacío: "No hay consultas para los filtros seleccionados."

### 1.2 Página de detalle de una consulta

URL ejemplo: `/consultas/consulta-mercedes-paseo-parque-independencia`

**Estructura:**
- Breadcrumb/etiqueta superior: "Consultas públicas".
- H1 con el nombre completo del proyecto.
- Subtítulo con fecha y modalidad (Presencial/Virtual).
- Dos tabs/anclas: "Metadatos" / "Secciones" (probablemente colapsan la sidebar en mobile).
- **Sidebar de metadatos** (complementary):
  - Estado (badge).
  - Inicio de participación (fecha y hora).
  - Cierre de participación (fecha y hora).
  - Sección (ej. "Consultas públicas").
  - Ejes de gestión.
  - Etiquetas (localidad, organismos, líneas de financiamiento).
- **Cuerpo de contenido** (texto narrativo en varios párrafos):
  1. Contexto institucional del proyecto (quién lo ejecuta, en el marco de qué plan/financiamiento).
  2. Objetivo y alcance técnico del proyecto (ejes de obra).
  3. Detalles logísticos de la instancia (fecha, hora, lugar físico) y mención a que los aportes fueron incorporados al informe final.
- **Archivos para descargar**: lista con ícono, nombre de archivo y peso (ej. PDF 1.4 MB), enlazando a almacenamiento externo (DigitalOcean Spaces en este caso).
- **Enlaces relevantes**: lista de links externos (Google Drive: resumen de proyecto, EIAS).
- **Galería**: carrusel de imágenes con miniaturas + botones anterior/siguiente + modal "Ver imagen N".
- **Comentarios**: sección con contador, selector de orden ("Más recientes"), botón "Recargar comentarios", estado de carga tipo skeleton/alert. Si la instancia está finalizada, probablemente los comentarios quedan en modo lectura.
- **Navegación rápida lateral** (ancla flotante): Volver arriba / Archivos / Enlaces relevantes / Galería / Comentarios.
- **Footer** institucional: logo, redes sociales (FB/X/IG/YouTube/Telegram/TikTok/Twitch), columnas de links (Secciones del sitio, Provincia de Buenos Aires, Legales).

### 1.3 Notas funcionales clave a replicar
- Sistema de **estados de la consulta** (programada / abierta / finalizada) que determina si se puede comentar/participar.
- **Taxonomía de filtros** de 3 niveles: estado, eje temático, etiquetas libres (multi-tag).
- Buscador de texto full-text sobre título/descripción.
- Cada consulta tiene: fecha de inicio/cierre de participación, modalidad (presencial/virtual/mixta), organismo(s) responsable(s), localidad(es), línea de financiamiento (si aplica).
- Detalle con: narrativa institucional + archivos descargables + enlaces externos + galería + comentarios + metadatos en sidebar.
- Mecanismo de comentarios con orden configurable y recarga manual (sugiere que se cargan vía API/async, tipo componente embebido — podría ser un servicio externo de moderación de comentarios, ya que compañía "democraciaenred" aparece en la URL de los archivos, posiblemente el proveedor de la plataforma completa, sugiere que corren sobre una plataforma "CONSUL" o similar de participación ciudadana).

---

## 2. Referencia estética: CAM — Municipalidad de La Plata

URL: https://cam.laplata.gob.ar/index.html

### 2.1 Identidad visual

**Tipografías** (Google Fonts cargadas):
- `Archivo` (principal, cuerpo y títulos, pesos 100–900) — es la fuente base del `<body>`.
- `Arimo` (secundaria/alternativa, 400–700).
- `Poppins` (posible uso en algún componente puntual).
- Íconos: Font Awesome (`font-awesome.min.css`).

**Paleta de color**
- Celeste/turquesa institucional principal: `rgb(40, 187, 221)` ≈ `#28BBDD` (color de texto en botones, acento).
- Gradiente de header/hero: `linear-gradient(#1278BA → #02A5C0)` (azul más profundo hacia turquesa), dirección vertical.
- Gradiente de sección "preguntas"/FAQ: mismo par de azules.
- Sección "portfolio" con split de fondo: gris claro `#EDEDED` (60%) + turquesa `#02A5C0` (40%), gradiente duro tipo "banda".
- Colores por categoría de trámite (cada card tiene su propio color de franja superior):
  - Licencias de Conducir → `#2EABE2` (celeste)
  - Habilitaciones Comerciales → `#5970F6` (azul-violeta)
  - APR → `#00A19A` (verde azulado/teal)
  - Obras Particulares → `#F39200` (naranja)
  - Catastro → verde (visual, no confirmado en hex)
  - Planeamiento y Ordenamiento Ambiental → rojo/coral (visual)
  - Mesa General de Entradas → gris neutro
- Fondo general de la página: blanco.

**Componentes / patrones de UI**
- Botones tipo **pill** totalmente redondeados (`border-radius: 50px`), fondo blanco con texto celeste (o inverso, celeste con texto blanco), usados para CTAs destacados ("+ Información", "Sacar turno +").
- **Cards de categoría/servicio** ("single-features"): fondo blanco, franja superior de color sólido (según categoría) con ícono de línea en blanco centrado, y debajo el nombre del trámite en el color de esa categoría. Esquinas redondeadas (~15-20px aprox.), sombra suave.
- **Fotos institucionales** con bordes muy redondeados, enmarcadas sobre fondo turquesa a modo de "tarjeta flotante".
- **Bloque de estadísticas** (contador grande de trámites realizados, % satisfacción, etc.) sobre fondo azul sólido, números grandes en blanco.
- **Testimonios** en cards blancas con comillas grandes, superpuestas sobre una foto de fondo con overlay azul semitransparente, con paginador de puntos (dots) abajo.
- **Galería de videos** en formato vertical tipo "stories" (thumbnails 9:16), con flechas de navegación circulares tipo carrusel.
- **Mapa embebido** (Google Maps) con card de información flotante sobre el mapa (nombre, dirección, rating).
- **Footer** simple: fondo azul sólido, logos institucionales centrados (CAM / La Plata Capital / Municipalidad de La Plata), sin mucho texto.
- Botón flotante "volver arriba" (circular, celeste, esquina inferior derecha, siempre visible al scrollear).

### 2.2 Tono / lenguaje visual general
- Diseño limpio, gubernamental pero cálido (uso de curvas, degradados suaves, mucho blanco).
- Fuerte codificación por color: cada área/servicio tiene un color identitario propio, consistente entre ícono, franja y texto.
- Fotografía real de la gestión (empleados atendiendo, vecinos) en vez de ilustraciones genéricas.
- Métricas de impacto (números grandes) como elemento de confianza/transparencia.
- Testimonios reales de vecinos como prueba social.

---

## 3. Síntesis: cómo combinar ambos

**Estructura/funcionalidad → tomar de Ministerio Abierto:**
- Página de listado con hero explicativo + FAQ acordeón + filtros por estado/eje/etiquetas + buscador + grilla de cards de consultas.
- Página de detalle con: hero, sidebar de metadatos, cuerpo narrativo, archivos descargables, enlaces relevantes, galería de imágenes, sección de comentarios, navegación rápida ancla, footer con redes y links institucionales.
- Taxonomía de datos por consulta: título, imagen, estado, fecha(s), modalidad, eje temático, etiquetas (organismo/localidad/financiamiento), descripción, archivos, links, galería.

**Estética/UI → tomar del CAM:**
- Tipografía `Archivo` como fuente principal.
- Paleta: azul institucional `#1278BA`/`#02A5C0` como gradiente de hero/header, turquesa `#28BBDD` como acento de botones y links.
- Un color distintivo por "eje de gestión" o categoría (siguiendo el patrón de las cards de trámites: franja de color + ícono blanco + texto del mismo color).
- Botones pill totalmente redondeados para CTAs (ej. "Participar", "Ver consulta").
- Cards de consulta con franja/ícono de color por eje temático (en vez de solo imagen genérica), esquinas muy redondeadas, sombra suave.
- Bloque de métricas de impacto (ej. "X consultas realizadas", "Y% de participación") en la home o en el listado, con números grandes sobre fondo azul.
- Testimonios de vecinos participantes (si hay datos) en cards con comillas grandes sobre foto con overlay.
- Footer con fondo azul sólido y logos institucionales, más columnas de links legales/secciones (mezclando el footer más completo de Ministerio Abierto con el estilo visual simple del CAM).
- Botón flotante "volver arriba" circular celeste.

## 4. Decisiones de stack y datos (definidas)

**Rol del proyecto:** construir una **maqueta/prototipo** de las páginas públicas (listado + detalle de
consultas). El sistema real (backend, base de datos, panel de moderación) lo va a implementar
después el equipo de Modernización de la Municipalidad, en el stack que ellos definan. No
corresponde a este proyecto resolver esa parte — solo dejar clara la estructura de datos y de
pantallas para que sea fácil de tomar como referencia.

**Stack técnico:** Astro (generador de sitio estático).
- Genera HTML/CSS/JS puro, deployable en cualquier servidor (no ata a un lenguaje de backend, algo
  relevante porque el hosting va a ser un servidor propio municipal cuya tecnología aún no está
  definida).
- Permite componentizar (header, card de consulta, acordeón FAQ, galería, formulario, etc.) y generar
  las páginas de detalle de cada consulta a partir de datos, sin duplicar HTML a mano.

**Fuente de datos:** archivos locales mockeados dentro del proyecto (sin backend real):
- `src/data/consultas/*.json` (o Markdown con front-matter), un archivo por consulta, seg├║n la
  taxonomía definida en la sección 5.
- Sirve además como **propuesta de contrato de datos** para el equipo de Modernización.
- **Comentarios/participación**: se simulan solo en el front (sin persistencia real ni moderación
  real) para mostrar la UX del flujo. Ver detalle en sección 5.3.

## 5. Instructivo legal municipal — "Procedimiento de Consulta Pública para Proyectos de Obras e
Intervenciones" (aporte al modelo de datos y contenidos)

Se recibió y analizó el instructivo interno de la Municipalidad de La Plata que regula el circuito
administrativo de las consultas públicas (Dependencia Requirente ↔ Autoridad de Aplicación). Es un
documento de procedimiento **interno/legal**, no de UI — no define pantallas, pero sí aporta datos y
reglas de contenido que la maqueta debe reflejar para ser realista y correcta.

### 5.1 No entra en el alcance de la maqueta
- El circuito administrativo interno (carátula de expediente, Nota de Solicitud de Apertura,
  intervención de la Autoridad de Aplicación, dictado de Disposiciones) es proceso **interno**, no
  pantallas públicas. No se modela como interfaz.
- No se construye backend, expedientes, ni sistema de gestión documental.

### 5.2 Datos/campos que suma al modelo de cada consulta
- **Expediente / denominación formal**: `"CONSULTA PÚBLICA – [PROYECTO] – [DEPENDENCIA
  REQUIRENTE]"` — se puede mostrar como dato adicional en metadatos (opcional, prolijo para
  realismo).
- **Dependencia Requirente**: el área municipal dueña del proyecto (distinto del "organismo/etiqueta"
  que ya teníamos — puede mapearse a ese mismo campo de etiquetas).
- **Plazos mínimos legales**: mínimo 5 días hábiles de participación; 10 días hábiles o más para
  proyectos de mayor escala/complejidad. Usar estos rangos al generar fechas de ejemplo realistas.
- **Documentos oficiales con valor de acto administrativo** (distintos de archivos técnicos comunes):
  - **Disposición de Apertura** (PDF) — publicada al abrir la consulta.
  - **Disposición de Cierre** (PDF) — publicada al finalizar, junto con el Informe Final.
- **Tipos de documentación técnica esperada** (para poblar la sección "Archivos para descargar" /
  "Enlaces relevantes" con ejemplos realistas): memoria descriptiva, planos generales, especificaciones
  técnicas particulares, renders/imágenes, presentación institucional del proyecto.
- **Explícitamente excluido de publicación**: cómputos, presupuestos oficiales, documentación
  económica del procedimiento de contratación (salvo excepción). No incluir este tipo de archivo en
  los datos mock.
- **Cantidad de presentaciones recibidas**: dato a mostrar (coincide con el contador de "comentarios"
  que ya se había visto en Ministerio Abierto).

### 5.3 Estructura del Informe Final (para consultas en estado "finalizada")
El instructivo exige que el Informe Final tenga 5 secciones fijas. Conviene mockear el contenido de
detalle de una consulta finalizada siguiendo esta estructura (en vez de un texto narrativo libre):
1. **Antecedentes** — identificación del proyecto y de la instancia realizada.
2. **Desarrollo de la consulta** — plazo de apertura y cantidad de presentaciones recibidas.
3. **Sistematización de las presentaciones** — principales cuestiones agrupadas por eje temático.
4. **Análisis técnico** — respuesta/consideración por cada eje temático.
5. **Consideraciones sobre el proyecto** — ajustes propuestos a raíz del proceso participativo.

Si no hubo presentaciones, corresponde igual un informe breve dejando constancia de eso — vale la
pena incluir un ejemplo de consulta finalizada "sin presentaciones" entre los datos mock, para mostrar
ese caso también.

### 5.4 Naturaleza de la "participación" (matiza la decisión de "comentarios reales")
El mecanismo oficial no es necesariamente un muro de comentarios abierto tipo red social: es un
**formulario digital de presentación** (observaciones/sugerencias/aportes) que la Autoridad de
Aplicación administra y luego sistematiza por eje temático en el Informe Final. Para la maqueta:
- Mockear un **formulario de participación** (nombre, contacto, observación/comentario) como
  mecanismo principal durante el estado "Participación abierta".
- Mantener también la vista tipo listado de comentarios/aportes (con contador y orden "más
  recientes", como se ve en Ministerio Abierto) para mostrar la experiencia visual completa, dejando
  claro que en producción esto requeriría moderación real antes de publicarse (estado
  "pendiente de aprobación" simulado solo en el front, sin persistencia).
- En consultas "finalizadas", el formulario deja de estar activo y en su lugar se muestra el Informe
  Final con la sistematización de lo recibido.

## 6. Pendiente de definición (para etapas posteriores, no bloquea el inicio de la maqueta)
- Paleta exacta de colores por eje temático a definir (cuántos ejes, qué color a cada uno) — se puede
  definir directamente al construir, siguiendo el patrón de color-por-categoría del CAM.
- Alcance responsive/mobile (el sitio del CAM es fuertemente mobile-first en varios bloques).
- Cantidad y variedad de consultas de ejemplo a mockear (se recomienda cubrir los 3 estados y al
  menos un caso "sin presentaciones").
