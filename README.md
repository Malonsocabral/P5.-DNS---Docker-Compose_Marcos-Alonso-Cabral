# P5.-DNS---Docker-Compose_Marcos-Alonso-Cabral
## 1. Configura un contenedor coa imaxe oficial de bind9 usando docker-compose.
>[!NOTE]
>Para poder crear este yml e configurar todo nos iformamos na paxina oficial e vamos ao propio link da imaxe: https://hub.docker.com/r/internetsystemsconsortium/bind9

Para configurar un contenedor primeiro debemos crear un ficheiro que chamarase `docker-compose.yml` que sera o arquivo no que estableceremos todos os parametros asi como os volumes seguindo a configuracion que nos explican na propia paxina oficial de dockerhub de bind9. O codigo do mey .yml 
é o seguinte:
```yaml
version: '3'

services:
  bind9:
    image: internetsystemsconsortium/bind9:9.18
    container_name: bind9
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "127.0.0.1:953:953/tcp"
    volumes:
      - bind_config:/etc/bind
      - bind_cache:/var/cache/bind
      - bind_lib:/var/lib/bind
    environment:
      - TZ=Europe/Madrid
    restart: unless-stopped

volumes:
  bind_config:
  bind_cache:
  bind_lib:
```
  
  E posteriormente podemos facer un `docker-compose up -d` para poder lanzar este entorno multicontenedor que so ten un contenedor.

## 2. Usa os volumes como se explica no setup da imaxe
>[!NOTE]
>Para explicar como funciona, vamos ao propio link da imaxe: https://hub.docker.com/r/internetsystemsconsortium/bind9

Como se pode ver no anterior yml e no que deixarei no repositorio, eu utilicei os tres volumes como na guia da propia imaxe.
Unha breve explicacion pode ser :   

`bind_config:/etc/bind`: Garda configuraciones de BIND, como archivos de zona e políticas DNS.  

`bind_cache:/var/cache/bind`: Almacena na caché DNS, mellorando o rendimiento ao conservar datos entre reinicios.  

`bind_lib:/var/lib/bind`: Garda datos dinámicos de DNS, como rexistros actualizables por clientes autorizados.  

## 3. Unha comprobado que o contenedor funciona, sube a GitHub o ficheiro nun repo.
Como xa comprobamos que todo funciona correctamente, facemos o commit no meu caso dende visual estudio. O `git add .` para engadir o .yml logo o commit e o `git push` como sempre.