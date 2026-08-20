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
la raíz queda accesible por su nombre de archivo.

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

EasyPanel redespliega solo. En un minuto la raíz sirve la nueva.

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

El formulario de `index.html` envía por **Web3Forms**: un endpoint que
reenvía cada envío a tu email. No hay backend ni base de datos, que es lo que
permite que el sitio siga siendo estático.

### Falta un paso para activarlo

1. Entra en https://web3forms.com, escribe `hola@qaizn.com` y pulsa
   "Create Access Key". Te llega la clave por email. No hay que crear cuenta.
2. En `index.html`, busca esta línea y pega la clave:

   ```js
   const ACCESS_KEY = 'PEGA_AQUI_TU_ACCESS_KEY';
   ```

3. `git commit` + `git push`. EasyPanel redespliega y el formulario funciona.

Mientras la clave sea el placeholder, el envío falla de forma controlada:
el visitante ve "No hemos podido enviarlo" con un enlace a `hola@qaizn.com`.
Nadie se queda sin poder contactar.

### Qué hace el formulario

- Valida en cliente antes de enviar (los cuatro campos son obligatorios,
  el email tiene que tener forma de email) y enfoca el primer campo inválido.
- Envía en segundo plano: sin recarga de página. Estados "Enviando…",
  confirmación, o error con el email de respaldo.
- Lleva un campo trampa (`botcheck`) oculto por CSS. Los bots lo rellenan,
  las personas no lo ven; Web3Forms descarta esos envíos.
- Los campos que llegan al email: nombre, email, empresa, area.

### Cambiar de proveedor

Todo lo específico de Web3Forms está en el bloque `// ── Formulario de
contacto` al final de `index.html`: la constante `ACCESS_KEY`, la URL del
`fetch` y los tres campos que se añaden al `FormData`. Para pasar a Formspree
u otro servicio basta con cambiar la URL y lo que se añade al `FormData`; el
markup, la validación y los estados no se tocan.
