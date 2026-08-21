# Despliegue y versiones de la landing

## Cómo se despliega

El sitio es una **app de EasyPanel** conectada a GitHub:

| Ajuste              | Valor                |
| ------------------- | -------------------- |
| Repositorio         | `jariass2/qaizn-web` |
| Rama                | `main`               |
| Ruta de compilación | `/`                  |

EasyPanel sirve la raíz del repo como sitio estático. **Todo lo que llega a
`main` se publica.** No hay paso de build: los `.html` del repo son el sitio.

Consecuencia práctica: `index.html` es la portada, y cualquier otro `.html` en
la raíz queda accesible por su nombre de archivo. Así se sirven también
`privacidad.html` y `aviso-legal.html`, que comparten `legal.css` y están
enlazadas desde el pie de la portada.

## Versiones de la landing

| Archivo        | URL                     | Qué es                                                      |
| -------------- | ----------------------- | ----------------------------------------------------------- |
| `index.html`   | `/`                     | **En producción.** Dirección Rams: paleta lino, standalone.  |
| `clasico.html` | `/clasico.html`         | La anterior. Build empaquetado (~525 KB).                    |

Las dos llevan el mismo contenido y las mismas secciones. Cambian el diseño y
la tipografía, no el mensaje.

Ambas están desplegadas siempre. La que decide qué ve quien entra por la raíz
es **solo `index.html`**.

## Cambiar de versión en producción

Volver a poner la clásica de portada:

```bash
git checkout main
git pull

cp index.html rams.html     # guarda la actual antes de sobrescribirla
cp clasico.html index.html

git add -A
git commit -m "Vuelve la portada a la versión clásica"
git push
```

En teoría EasyPanel redespliega solo y en un minuto la raíz sirve la nueva.

> **En la práctica el webhook falla a menudo.** Ha habido tandas de varios
> commits que se quedaron sin publicar durante horas sin dar ningún error.
> Después de cada push, **verifica** que ha salido:
>
> ```bash
> curl -s https://www.qaizn.com/ | diff -q - <(git show main:index.html) \
>   && echo "en vivo = main" || echo "NO desplegado"
> ```
>
> Si no ha salido, entra al panel de EasyPanel y lanza el deploy a mano.

Deshacer el último cambio de portada, sin más:

```bash
git checkout main
git revert HEAD
git push
```

> El `cp` de seguridad del primer paso importa: `clasico.html` es un build
> empaquetado que **no se regenera desde este repo**. Si lo sobrescribes sin
> copia, recuperarlo pasa por el historial de git.

## Previsualizar antes de publicar

En local, sin desplegar nada:

```bash
python3 -m http.server 8000
```

Y abre `http://localhost:8000/`.

## Notas

- `index.html` (Rams) carga las tipografías desde Google Fonts.
  `clasico.html` las lleva embebidas en su propio bundle.
- Archivos históricos que también están en la raíz y por tanto son públicos:
  `index_old.html`, `qaizn2.html`, `hero-neobrutalist-backup.html`,
  `index_bundled_backup.html`. No están enlazados desde ningún sitio, pero
  cualquiera que sepa el nombre puede abrirlos. Si eso molesta, hay que
  borrarlos del repo.

## Formulario de contacto

El formulario de `index.html` envía por **SimplyForms**: un endpoint que
recibe el envío, lo reenvía a tu email y lo descarta. No guarda copia. No hay
backend ni base de datos, que es lo que permite que el sitio siga siendo
estático.

Se eligió por dónde está alojado: **Alemania, sobre servidores de Hetzner**.
Los datos del formulario no salen del Espacio Económico Europeo, y eso es lo
que declara la [política de privacidad](privacidad.html) en su tabla de
encargados del tratamiento. Si algún día se cambia de proveedor, esa tabla
hay que actualizarla en el mismo commit.

### Estado: activo

El ID ya está puesto en `index.html` y el envío está probado contra el
endpoint real. Los mensajes llegan al email registrado en SimplyForms.

```js
const ENDPOINT = 'https://api.simplyforms.app/v1/forms/iCYIyThsapHffDWnVM1KjA';
```

Ese ID es **público**: va en el cliente por diseño y solo autoriza enviar al
email registrado. No da acceso a nada, así que no pasa nada porque esté en el
repo. Si alguna vez recibes spam por él, se regenera desde SimplyForms y se
sustituye esa línea.

> La **API key** de la cuenta es otra cosa y **nunca va en el repo ni en el
> HTML**: sirve para gestionar formularios desde su API y es privada.

El email de destino se configura **en el panel de SimplyForms**, no aquí.
Cambiar `jordi@qaizn.com` en el HTML solo cambia lo que se muestra; para
cambiar a dónde llegan los envíos hay que tocarlo en su panel.

Si el envío fallara, el visitante ve "No hemos podido enviarlo" con un enlace
a `jordi@qaizn.com`. Nadie se queda sin poder contactar.

### Qué hace el formulario

- Valida en cliente antes de enviar (los cuatro campos son obligatorios,
  el email tiene que tener forma de email) y enfoca el primer campo inválido.
- Envía en segundo plano: sin recarga de página. Estados "Enviando…",
  confirmación, o error con el email de respaldo.
- Lleva un campo trampa (`_botcheck`) oculto por CSS. Los bots lo rellenan,
  las personas no lo ven. El plan gratuito de SimplyForms **no filtra la
  trampa en servidor**, así que lo comprueba el JS: si viene marcado, se le
  enseña al bot la misma confirmación de éxito y no se envía nada.
- El prefijo `_` hace que SimplyForms excluya ese campo del cuerpo del email.
- Los campos que llegan al email: nombre (y apellidos), email, empresa,
  cargo y area, más un `subject` fijo. `cargo` es el único opcional, y si se
  deja en blanco no se envía — así el email no llega con líneas vacías.
- La API acepta `200` con `{"success": true}` y devuelve
  `{"ok": false, "code": ..., "message": ...}` al fallar. El JS trata ambos.
  Si abres la URL del endpoint en el navegador verás `EMPTY_PAYLOAD`: es la
  respuesta normal a una petición sin datos, no un fallo.

### Cambiar de proveedor

Todo lo específico de SimplyForms está en el bloque `// ── Formulario de
contacto` al final de `index.html`: la constante `ENDPOINT`, la comprobación
de la trampa y los campos que se añaden al `FormData`. Para pasar a otro
servicio basta con cambiar la URL y lo que se añade al `FormData`; el markup,
la validación y los estados no se tocan.

Antes de cambiar, comprueba dónde aloja el nuevo proveedor: si sale del EEE,
la política de privacidad deja de ser cierta.
