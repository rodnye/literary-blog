# Literary Blog

![Astro](https://img.shields.io/badge/Astro-0C1222?style=for-the-badge&logo=astro&logoColor=FDFDFE)
![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)
![Decap CMS](https://img.shields.io/badge/Decap%20CMS-6E2C8C?style=for-the-badge&logo=decap-cms&logoColor=white)
![Decap Bridge](https://img.shields.io/badge/Decap%20Bridge-4A90E2?style=for-the-badge&logo=auth0&logoColor=white)
![Netlify](https://img.shields.io/badge/Netlify-00C7B7?style=for-the-badge&logo=netlify&logoColor=white)
![pnpm](https://img.shields.io/badge/pnpm-F69220?style=for-the-badge&logo=pnpm&logoColor=white)

Sitio web personal construido con Astro, disponible en [quemeimporta.netlify.app](https://quemeimporta.netlify.app). El repositorio separa el código fuente del contenido mediante un flujo basado en dos ramas y un script de actualización.

## Ramas

- **master** – Código fuente de la aplicación Astro.
- **editorial_workflow** – Contenido del blog (markdown e imágenes).

## Flujo de contenido

El contenido se gestiona de forma aislada. En `master` hay un script que descarga un ZIP de la rama `editorial_workflow` y lo copia en los directorios correspondientes (`src/content`, `public/images`), respetando `.gitignore` anidados para evitar versionar el contenido.

```bash
pnpm storage:update
```

## CMS y autenticación

- **Decap CMS** interfaz en `/admin` para editar contenido.
- **Decap Bridge** gestiona el identity login con GitHub.

Los cambios se comitean automáticamente en la rama `editorial_workflow`.

## Instalación local

```bash
git clone https://github.com/rodnye/literary-blog.git
cd literary-blog
pnpm install
pnpm storage:update # Opcional, pero el blog estará vacío
pnpm dev
```

---

Enlaces de interés:
- [Docs de Astro](https://astro.build)
- [Decap CMS](https://decapcms.org/docs/)
