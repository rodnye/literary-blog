---
title: Blog con Astro y Decap CMS
description: Cómo separar el código del contenido en un blog con Astro y Decap CMS
pubDate: 2026-03-01T05:32:00.000-05:00
heroImage: /src/assets/images/uploads/astro.jpeg
---

> Esto es una publicación de pruebas, será borrada más adelante por la autora

Mantener un blog técnico o literario implica un desafío común: gestionar el contenido (artículos, imágenes) sin que este interfiera con el código fuente o viceversa. En mi repositorio `rodnye/literary-blog` encontrarás una solución práctica para este problema, construida con **Astro** y **Decap CMS**, ahora desplegada en **Cloudflare Pages**.

La premisa es simple pero efectiva: **el código y el contenido viven en ramas diferentes de Git** y se sincronizan solo cuando es necesario. Aquí te explico cómo funciona.

## La arquitectura de dos ramas

El proyecto se organiza en dos ramas principales con propósitos claramente definidos:

*   **`master`**: Contiene todo el código fuente de la aplicación Astro. Aquí residen los componentes, estilos, configuraciones y la lógica del sitio. El contenido del blog no está versionado en esta rama.
*   **`editorial_workflow`**: Actúa como el "depósito de contenido". En esta rama se guardan todos los archivos Markdown de los posts y las imágenes, organizados en las carpetas correspondientes.

Esta separación permite que el desarrollo del sitio y la creación de contenido sean procesos independientes y limpios.

## Sincronización bajo demanda con un script

Para unir ambos mundos de manera controlada, el proyecto incluye un script inteligente que se ejecuta con un comando de pnpm:

```bash
pnpm blog:sync
```

¿Qué hace este comando?

1.  Se ejecuta desde la rama `master`.
2.  Descarga un archivo ZIP de la rama `editorial_workflow` directamente desde GitHub.
3.  Extrae el contenido y lo copia en las carpetas locales adecuadas (`src/content` para los posts y `src/assets/images` para las imágenes).
4.  Respeta reglas de `.gitignore` específicas para asegurar que este contenido sincronizado no se añada accidentalmente al historial de la rama `master`.

De esta forma, el contenido "semilla" o las últimas actualizaciones se integran en el entorno de desarrollo o producción solo cuando tú lo decides.

## Gestión de contenido con Decap CMS

Para que la experiencia de escritura sea cómoda, el blog integra **Decap CMS** (anteriormente Netlify CMS). Puedes acceder a la interfaz de administración en la ruta `/admin` de tu sitio.

La autenticación se realiza directamente con tu cuenta de GitHub. Cuando un autor crea o edita un post a través de esta interfaz, los cambios se confirman (commit) automáticamente en la rama `editorial_workflow`. Esto mantiene el flujo de trabajo editorial sin que el escritor necesite tocar la línea de comandos.

## Despliegue en Cloudflare Pages

El sitio está configurado para desplegarse automáticamente en **Cloudflare Pages** desde la rama `master`. Cada vez que se fusionan cambios en `master` (ya sea código nuevo o una sincronización de contenido), Cloudflare Pages se encarga de construir y publicar la versión actualizada del blog.

Este cambio de Netlify a Cloudflare Pages mantiene todas las ventajas del flujo de trabajo original, ofreciendo un rendimiento excelente y una integración continua sin complicaciones.

## Cómo probarlo localmente

Si quieres ver cómo funciona todo en conjunto, los pasos son muy sencillos:

1.  Clona el repositorio: `git clone https://github.com/rodnye/literary-blog.git`
2.  Entra en la carpeta: `cd literary-blog`
3.  Instala las dependencias con pnpm: `pnpm install`
4.  (Opcional) Sincroniza el contenido semilla: `pnpm blog:sync`. Si omites este paso, el blog arrancará vacío, listo para que añadas tu propio contenido a través del CMS.
5.  Inicia el servidor de desarrollo: `pnpm dev`

Puedes ver el resultado en vivo en [quemeimporta.netlify.app](https://quemeimporta.netlify.app) (aunque el dominio aún refleje el proveedor anterior, el sitio ahora funciona sobre Cloudflare).

## Tecnologías clave

*   **Astro**: Para construir un sitio web rápido y optimizado.
*   **Decap CMS**: Para una gestión de contenido amigable.
*   **pnpm**: Como gestor de paquetes rápido y eficiente.
*   **Cloudflare Pages**: Para el despliegue y la integración continua.

Este enfoque es ideal para blogs o sitios donde el contenido debe ser gestionado por un equipo editorial sin acceso al código, manteniendo un repositorio limpio y un flujo de trabajo profesional.
