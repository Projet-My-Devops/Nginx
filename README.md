# Nginx

L'image "Nginx" va être utilisé comme reverse-proxy.

## Comment générer un certificat auto-signé ?
1. Générer un certificat
    - openssl req -newkey rsa:2048 -nodes -keyout /docker/nginx/certs/key.pem -x 509 -days 365 -out /docker/nginx/certs/certificate.pem
2. Remplir les différents champs demandés
    - Vous n'êtes pas obliger de remplir les champs

## Comment ajouter un site dans Nginx ?
3. Se rendre dans le dossier "conf.d"
    - cd /docker/nginx/config/conf.d
4. Créer un fichier portant le nom de l'application
    - nano gitlab.conf
5. Reprendre la même structure que les autres fichiers: 
        ```

        server {
            listen	80;
            server_name	example.mydevops.com;

            return 301 https://$server_name$request_uri;

            location / {
                proxy_pass http://IP;
            }
        }

        server {
            listen	443 ssl;
            server_name	example.mydevops.com;

            location / {
                proxy_pass http://IP;
            }
        }
        ```
6. Modifier le champs "server_name" et "proxy_pass"
    - Dans le champ "server_name", remplacer le mot 'example'
    - Dans le champ "proxy_pass" mettre l'adresse IP du serveur + le port s'il y en a un particulier