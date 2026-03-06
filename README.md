<center>

# Literary Blog

![Astro](https://img.shields.io/badge/Astro-0C1222?style=for-the-badge&logo=astro&logoColor=FDFDFE)
![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)
![Decap CMS](https://img.shields.io/badge/Decap%20CMS-6E2C8C?style=for-the-badge&logo=decap-cms&logoColor=white)
![Decap Bridge](https://img.shields.io/badge/Decap%20Bridge-4A90E2?style=for-the-badge&logo=auth0&logoColor=white)
![pnpm](https://img.shields.io/badge/pnpm-F69220?style=for-the-badge&logo=pnpm&logoColor=white)

  <img src="./docs/assets/home_preview.webp">
  <img src="./docs/assets/blog_preview.webp">
</center>

---

Website built with Astro. The repository separates source code from content through a workflow based on two branches and an update script.

## Branches

- **master** – Astro application source code.
- **editorial_workflow** – Blog content (markdown and images).

## Content workflow

Content is managed in isolation. In `master` there is a script that downloads a ZIP from the `editorial_workflow` branch and copies it to the corresponding directories (`src/content`, `src/assets/images`), respecting nested `.gitignore` files to avoid versioning the content.

```bash
pnpm blog:sync
```

## CMS and authentication

- **Decap CMS** interface available at `/admin\*\* for content editing and management. This route provides access to the administrative dashboard where authorized users can create, edit, and publish blog posts without touching the codebase.

![](./docs/assets/cms_preview_02.webp)

- **Decap Bridge** manages identity login with GitHub for secure authentication.

Changes made through the CMS are automatically committed to the `editorial_workflow` branch.

For detailed configuration options, customizations, and authentication setup, refer to the official **[Decap CMS Documentation](https://decapcms.org/docs/)**.

## Available at:

- Evennode: http://quemeimporta.eu-4.evennode.com/
- Render: https://quemeimporta.onrender.com
- Vercel: https://quemeimporta.vercel.app
- Netlify: https://quemeimporta.netlify.app
- Cloudflare Pages: https://quemeimporta.pages.dev
- Deno Deploy: https://quemeimporta.rodnye.deno.net/
- Github Pages: https://rodnye.github.io/literary-blog/

## Local installation

```bash
git clone https://github.com/rodnye/literary-blog.git
cd literary-blog
pnpm install
pnpm blog:sync # Optional, but the blog will be empty
pnpm dev
```

---

Useful links:

- [Astro Docs](https://astro.build)
- [Decap CMS Documentation](https://decapcms.org/docs/)
