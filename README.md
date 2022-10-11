# Nginx

L'image "Nginx" va être utilisé comme reverse-proxy.

## Comment générer un certificat auto-signé ?
1. Aller dans le dossier des certificats
    - cd /docker/nginx/certs
2. Générer un certificat
    - openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
3. Remplir les différents champs demandés
    - Vous n'êtes pas obliger de remplir les champs

## Comment ajouter un site dans Nginx ?
4. Se rendre dans le dossier "conf.d"
    - cd /docker/nginx/config/conf.d
5. Créer un fichier portant le nom de l'application
    - nano gitlab.conf
6. Reprendre la même structure que les autres fichiers: 
        ```

        server {
            listen	80;
            server_name	example.mydevops.intra;

            return 301 https://$server_name$request_uri;

            location / {
                proxy_pass http://IP;
            }
        }

        server {
            listen	443 ssl;
            server_name	example.mydevops.intra;

            location / {
                proxy_pass http://IP;
            }
        }
        ```
7. Modifier le champs "server_name" et "proxy_pass"
    - Dans le champ "server_name", remplacer le mot 'example'
    - Dans le champ "proxy_pass" mettre l'adresse IP du serveur + le port s'il y en a un particulier