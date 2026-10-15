# Lander

A responsive fallback page for hostnames with no configured website. Self-contained HTML, CSS and inline SVG, with a small script to show the requested hostname and retry the request. No build step or external assets.

## Deploy with Coolify

1. Push this repository to your Git provider.
2. Add an application in Coolify and select this repository.
3. Choose the Dockerfile build pack with `/Dockerfile` as the Dockerfile location.
4. Set the exposed application port to 80 and deploy.
5. Configure your reverse proxy to route unmatched hostnames to this container. Deploying this application alone does not configure a catch-all route. Keep existing application routes at a higher priority.

The container returns this page with HTTP 404 for every requested path. `/healthz` returns HTTP 200 for health checks. Search engine indexing is disabled. TLS for unmatched hostnames must be handled by your proxy and certificate configuration.

## Local preview

Open `index.html` in a browser, or serve it with a local static server. A static preview displays the design but does not reproduce the Nginx 404 responses.

```sh
docker build -t lander .
docker run --rm -p 18744:80 lander
```

Visit http://localhost:18744. Edit `index.html` to customize the page.
