# despliegue

Web 1 del examen de despliegue: **Tueste Lento**, tienda ficticia de café con catálogo, filtros y cesta.
Es un único `index.html` estático, sin compilación. La web 2 está en el repo `despliegue2`.

```bash
sudo git clone https://github.com/Skyfreefury/despliegue.git /var/www/web1
sudo chown -R www-data:www-data /var/www/web1
```

Nginx la sirve en el puerto 8081 con `root /var/www/web1;`.
