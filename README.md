# despliegue

Dos webs estáticas para practicar un despliegue con Nginx y Cloudflare Tunnel. Cada carpeta tiene un único `index.html` que no necesita compilación.

| Carpeta | Web | Puerto en el examen |
|---|---|---|
| `web1/` | Tueste Lento: tienda de café con catálogo, filtros y cesta | 8081 |
| `web2/` | Consulta vecinal de Benimaclet: encuesta por pasos con resultados | 8082 |

Ambas son ficticias. La cesta y el voto se guardan solo en el navegador (`localStorage`).

## Despliegue rápido

```bash
sudo git clone https://github.com/Skyfreefury/despliegue.git /var/www/despliegue
sudo chown -R www-data:www-data /var/www/despliegue
```

En `/etc/nginx/sites-available/miswebs`:

```nginx
server {
    listen 8081;
    root /var/www/despliegue/web1;
    index index.html;
    location / { try_files $uri $uri/ =404; }
}
server {
    listen 8082;
    root /var/www/despliegue/web2;
    index index.html;
    location / { try_files $uri $uri/ =404; }
}
```

```bash
sudo ln -sf /etc/nginx/sites-available/miswebs /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
cloudflared tunnel --url http://localhost:8081   # terminal 1
cloudflared tunnel --url http://localhost:8082   # terminal 2
```
