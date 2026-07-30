# slemanz.com

Personal portfolio and blog built with [Hugo](https://gohugo.io/) and the [hugo-coder](https://github.com/luizdepra/hugo-coder) theme.

Available in English and Portuguese (BR).

## Structure

```
sleman-coder/
├── content/
│   ├── about.md / about.pt-br.md         # About page
│   ├── projects/                         # Projects page + hardware gallery
│   ├── contact.md / contact.pt-br.md     # Contact page
│   └── posts/                            # Blog posts
├── static/images/                        # Avatar and images
├── themes/hugo-coder/                    # Theme
├── hugo.toml                             # Site configuration
└── README.md
```

## Requirements

### Install Hugo on Ubuntu/Debian

```bash
sudo apt update
sudo apt install hugo
```

Verify installation:

```bash
hugo version
```

If the version from `apt` is too old (hugo-coder needs v0.110+), install the latest from the official release:

```bash
# Check latest version at https://github.com/gohugoio/hugo/releases
wget https://github.com/gohugoio/hugo/releases/download/v0.141.0/hugo_extended_0.141.0_linux-amd64.deb
sudo dpkg -i hugo_extended_0.141.0_linux-amd64.deb
```

## Build & Run

### Development server (live reload)

```bash
hugo server -D
```

Open [http://localhost:1313](http://localhost:1313) in your browser.

### Build for production

```bash
hugo --minify
```

The static site will be generated in the `public/` directory, ready to deploy.

## Deploy

The `public/` folder can be deployed to any static hosting:

**GitHub Pages:**
```bash
hugo --minify
# push the public/ folder to your gh-pages branch
```

**Netlify:** just connect the repo and set build command to `hugo --minify`.

## Adding content

### New blog post

```bash
hugo new posts/my-new-post.md
```

For the Portuguese version, create `posts/my-new-post.pt-br.md` with the same slug.

### Avatar

Replace `static/images/avatar.jpg`.

## Customization

All configuration is in `hugo.toml`. The main things you might want to change:

- `baseURL`: your domain
- `params.author`: your name
- `params.info`: tagline shown on homepage
- `params.social`: social media links
- `params.avatarURL`: path to your photo
