# vscode-nginx-certbot
Host VSCode with SSL via Nginx and Certbot

*Note: This method uses basic auth -- which is fine if you control the client devices that you're connecting with. However, you should choose an alternate solution if you cannot ensure control of the devices that will access this site.*

1. Update your DNS provider to point your domain/subdomain to the server
2. Install Docker w/compose, and clone this repo
3. Create an htaccess file at ./nginx/.htaccess (use the `htpasswd` command: `htpasswd -c ./nginx/.htpasswd myusername`)
4. Execute `docker compose up -d`
5. Execute `docker compose run --rm certbot certonly --webroot --webroot-path /var/www/certbot/ -d YOUR_DOMAIN_HERE` and follow the steps to create your SSL cert
6. Execute `docker compose down`
7. Uncomment the commented-out parts of ./nginx/conf/default.conf, and replace instances of 'YOUR_DOMAIN_HERE' with your domain name
8. Execute `docker compose up -d`

VSCode should now be running. You can access the site by going to it via https (and http should redirect you to https).

To keep your certs updated, just do a `docker compose restart certbot` every three months. Or a `docker compose down` followed by a `docker compose up -d`.

You can add other programs (and VSCode extensions) to be pre-installed by editing ./code/Dockerfile, and you can setup further persistence by adding/changing the volumes assigned to the vscode service in the docker-compose.yml file.
