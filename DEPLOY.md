# Despliegue y versiones de la landing

## Cómo se despliega

El sitio es una **app de EasyPanel** conectada a GitHub:

| Ajuste             | Valor                |
| ------------------ | -------------------- |
| Repositorio        | `jariass2/qaizn-web` |
| Rama               | `main`               |
| Ruta de compilación | `/`                  |

EasyPanel sirve la raíz del repo como sitio estático. **Todo lo que llega a
`main` se publica.** No hay paso de build: los `.html` del repo son el sitio.

Consecuencia práctica: `index.html` es la portada, y cualquier otro `.html` en
la raíz queda accesible por su nombre de archivo.

## Versiones de la landing

| Archivo      | URL                    | Qué es                                                         |
| ------------ | ---------------------- | -------------------------------------------------------------- |
| `index.html` | `qaizn.com`            | **La que está en producción.** Build empaquetado (~525 KB).     |
| `rams.html`  | `qaizn.com/rams.html`  | Dirección alternativa: paleta lino, Dieter Rams. Standalone.    |

Ambas llevan el mismo contenido y las mismas secciones. Cambian el diseño y la
tipografía, no el mensaje.

Las dos están desplegadas siempre. La que decide qué ve el visitante que entra
por `qaizn.com` es **solo `index.html`**.

## Cambiar de versión en producción

Poner la versión Rams en producción:

```bash
git checkout main
git pull

cp index.html index-clasico.html   # guarda la actual antes de sobrescribirla
cp rams.html index.html

git add -A
git commit -m "Cambia la portada a la dirección Rams"
git push
```

EasyPanel redespliega solo. En un minuto `qaizn.com` sirve la nueva.

Volver a la anterior:

```bash
git checkout main
git revert HEAD      # deshace el commit del cambio
git push
```

O, si ya hay commits encima:

```bash
cp index-clasico.html index.html
git commit -am "Vuelve a la portada clásica"
git push
```

> El `cp index.html index-clasico.html` del primer paso importa: `index.html`
> es un build empaquetado que no se regenera desde este repo. Si lo
> sobrescribes sin copia, recuperarlo pasa por el historial de git.

## Previsualizar antes de publicar

En local, sin desplegar nada:

```bash
python3 -m http.server 8000
```

Y abre `http://localhost:8000/rams.html`.

## Notas

- **El formulario de contacto no envía a ninguna parte.** Ni en `index.html` ni
  en `rams.html`: es markup estático, sin `<form>`, sin `action` y sin handler.
  Para capturar leads de verdad hay que conectarlo a un endpoint.
- `rams.html` carga las tipografías desde Google Fonts. `index.html` las lleva
  embebidas en el propio bundle.
- Archivos históricos que también están en la raíz y por tanto son públicos:
  `index_old.html`, `qaizn2.html`, `hero-neobrutalist-backup.html`,
  `index_bundled_backup.html`. No están enlazados desde ningún sitio, pero
  cualquiera que sepa el nombre puede abrirlos. Si eso molesta, hay que
  borrarlos del repo.
