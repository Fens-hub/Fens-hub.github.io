# fennyotieno

Portfolio built with the [Nerdy](https://github.com/hugo-themes/nerdy) Hugo theme.

## Requirements
Hugo extended 0.162.1+, Node.js 24+, Go.

## Run
```
npm install
hugo mod get github.com/hugo-themes/nerdy
npm run server      # http://localhost:1313
npm run build       # output in public/
```

## Edit
- Sidebar, bio, stats, stack: `data/sidebar.yaml`
- Terminal commands: `data/terminal/`
- This Week log: `data/home/this-week.yaml`
- Articles: `content/posts/<subject>/<topic>/your-post.md`
- Avatar: `assets/images/avatar.jpg`
- Domain: `baseURL` in `hugo.yaml`
