# bestias galería — landing "próximamente"

Landing animada de espera para **bestias galería** (Dresde 3, Col. Juárez, CDMX).
Sitio estático, sin build ni dependencias: la ilustración va en SVG inline y todo el
CSS/JS está embebido en `index.html`. Lo único externo es la tipografía de Google Fonts
y los tres audios de `sfx/`.

Dominio: **bestias.gallery**

## Archivos

- `index.html` — la página completa.
- `CNAME` — dominio para GitHub Pages.
- `favicon.svg` — ícono de pestaña (la "b").
- `sfx/` — rugidos reales (`dino.mp3`, `dragon.mp3`, `gallina.mp3`) + `list.json`.
- `ilustracion bestias.svg`, `LOGO_01.svg` — originales de referencia.

## Qué hace

**Base**
- Ilustración de la fachada con paleta y estilo de línea; el pájaro está al frente y su
  cola es opaca (tapa la cornisa, como debe ser).
- Logo "b" que se dibuja al cargar y hace un fundido suave en cada cambio de paleta.
- Lámparas con péndulo, pájaro que brinca y parpadea.
- Fondo de azulejos que se deforma con el cursor.
- Paleta que rota sola cada 10 s (terracota, verde, azul, negro).
- Cuenta regresiva, captura de correo, redes y contacto.

**Al hacer clic en un cuadro** (`index.html`, bloque "Efectos al hacer clic")
Cada cuadro tiene su efecto y *se contagia* a otras partes del sitio al azar
(pájaro, lámparas, letrero, contador, logo…). A veces cae en todo el sitio.
Todo termina con una sacudida y regresa.

| Cuadro | Efecto |
|---|---|
| 1 | glitch (bandas desplazadas) |
| 2 | aberración cromática |
| 3 | se derrite como tinta |
| 4 | pixelado |
| 5 | sacudida |
| 6 | onda |

Además suena un rugido al azar: se mezclan los 3 samples reales de `sfx/` con
4 bestias sintetizadas en el navegador (Web Audio: formantes + distorsión + reverb).

**A los 15 s sin actividad** la bestia se duerme: ronca y una onda sale del centro
de la pantalla hacia afuera, deformando la ilustración y empujando cada bloque con
un retraso proporcional a su distancia al centro. Cualquier movimiento la despierta.

## Ajustes rápidos

| Qué | Dónde |
|---|---|
| Fecha de apertura | `const LAUNCH=new Date(2026,8,15,19,0,0)` (mes base 0: 8 = septiembre) |
| Intensidad de los efectos | variable CSS `--fxk` (`.illus .fxel{--fxk:2.6}`) |
| Velocidad de la onda del ronquido | `const VEL=760` (px/s) |
| Ciclo del ronquido | `const PERIODO=4400` (ms); la onda visual lo hereda |
| Tiempo de inactividad | `const IDLE_MS=15000` |
| Grosor de trazo del letrero | variable CSS `--bold` |

### Agregar o cambiar sonidos

Suelta los MP3 en `sfx/` y agrégalos a `sfx/list.json`. Se cargan solos y entran a la
mezcla. Si `list.json` no existe, el sitio usa solo los sintetizados.

Los audios actuales vienen de Mixkit ([licencia](https://mixkit.co/license/#sfxFree):
uso comercial y personal, sin atribución obligatoria).

## Publicar

```bash
cd "BESTIAS WEB"
git init && git add . && git commit -m "bestias galería"
git branch -M main
git remote add origin https://github.com/<usuario>/<repo>.git
git push -u origin main
```

En GitHub: **Settings → Pages → Branch `main` / root**. El archivo `CNAME` ya apunta
a `bestias.gallery`; falta configurar el DNS en GoDaddy (registros A al rango de
GitHub Pages + CNAME de `www`).

## Pendientes

- [ ] Imagen `og.png` (1200×630) para el preview al compartir el link.
- [ ] Conectar el formulario de correos a un servicio real (hoy solo confirma en pantalla).
- [ ] Confirmar la fecha de apertura.
