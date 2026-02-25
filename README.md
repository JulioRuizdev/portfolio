# Julio Ruiz — Portfolio

Portfolio personal de DevOps Engineer. Construido con **Astro** + **Tailwind CSS**.

## Stack
- [Astro](https://astro.build) — framework estático
- [Tailwind CSS](https://tailwindcss.com) — estilos utilitarios
- Deploy en [Vercel](https://vercel.com)

## Desarrollo local

```bash
# 1. Instalar dependencias
npm install

# 2. Iniciar servidor de desarrollo (http://localhost:4321)
npm run dev

# 3. Build de producción
npm run build

# 4. Preview del build
npm run preview
```

## 🐳 Docker local

```bash
# Build y levantar
docker compose up -d --build

# Ver logs
docker compose logs -f

# Bajar
docker compose down
```

Accede en `http://localhost`

---

## 🚀 Deploy en DigitalOcean (CI/CD automático)

### 1. Setup inicial en el Droplet (una sola vez)

```bash
ssh julio@<IP_DROPLET>

# Instalar Docker
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
newgrp docker

# Clonar el repo
mkdir -p ~/apps && cd ~/apps
git clone https://github.com/JulioRuizdev/portfolio.git
cd portfolio

# Primer deploy manual
docker compose up -d --build
```

### 2. Secrets en GitHub

Ve a tu repo → **Settings → Secrets and variables → Actions** y agrega:

| Secret | Valor |
|--------|-------|
| `DO_HOST` | IP de tu Droplet |
| `DO_USER` | `julio` |
| `DO_SSH_KEY` | Contenido de tu clave privada SSH (`~/.ssh/id_ed25519`) |

### 3. Flujo automático

Cada `git push` a `main` dispara el pipeline:

```
push → build (Node 20) → SSH al droplet → git pull → docker compose up --build
```

## Estructura

```
src/
├── components/
│   ├── Nav.astro       ← Navegación + theme toggle
│   ├── Hero.astro      ← Sección principal + terminal
│   ├── About.astro     ← Sobre mí + stats
│   ├── Skills.astro    ← Stack técnico
│   ├── Projects.astro  ← Proyectos (editar aquí)
│   └── Contact.astro   ← Contacto + redes
├── layouts/
│   └── Layout.astro    ← HTML base, meta tags
├── pages/
│   └── index.astro     ← Página principal
└── styles/
    └── global.css      ← Variables CSS, dark/light mode
```

## Agregar un proyecto nuevo

Edita `src/components/Projects.astro` y agrega un objeto al array `projects`:

```js
{
  num: '04',
  status: 'live',        // 'live' | 'wip'
  statusLabel: 'Live',
  title: 'Nombre del proyecto',
  desc: 'Descripción corta del proyecto.',
  stack: ['Terraform', 'AWS'],
  href: 'https://github.com/JulioRuizdev/mi-repo',
}
```
