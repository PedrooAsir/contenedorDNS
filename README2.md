# DNS -> Servidor - Cliente

Cogemos de la práctica anterior el archivo docker-compose.yml donde en esta práctica añadiremos un servicio mas (cliente) para que actúe con el contenedor de servidor.

Para configurar el cliente, es casi el mismo código pero cambian o se añaden algunas cosas, por ejemplo el "DNS", donde tendremos que poner la puerta de enlace  del Servidor que en este caso es la 172.28.5.1. Continuamente, le asignamos cualquier numero de equipo a la IP del cliente (172.28.5.2).


Una vez configurado el cliente - servidor, empezamos LANZANDO los contenedores con:

$ docker compose up -d

Una vez encendidos, accedemos a sus terminales con clic derecho en el contenedor y "Attach Shell" u otra manera que es con:

# Servidor

"$ docker exec -it [nombre del servidor] bash" 

# cliente

"$ docker exec -it [nombre del cliente] sh" 


Para poder usar los comandos de red haríamos:

# Servidor

$ apt update
$ apt install -y dnsutils
$ apt-get install -y iputils-ping

# Cliente

$ apk add --no-cache bind-tools (Para Dig y Ping).
========================================================================
$TTL 38400	; 10 hours 40 minutes
@		IN SOA	ns.asircastelao.int. some.email.address. (
				10000002   ; serial
				10800      ; refresh (3 hours)
				3600       ; retry (1 hour)
				604800     ; expire (1 week)
				38400      ; minimum (10 hours 40 minutes)
				)
@		IN NS	ns.asircastelao.int.
ns		IN A		172.28.5.1
test	IN A		172.28.5.4
www		IN A  		172.28.5.7
sinco	IN A 		172.28.5.9
alias	IN CNAME	test
texto	IN TXT		mensaje

-------------------------------------------------------------------------

Vamos a fijarnos en la imagen de arriba que es la Db de asircastelao.int. Por ejemplo, si queremos resolver los nombres en una base de datos como por ejemplo esta , entramos a la Terminal del Cliente. Contínuamente, haremos un Dig [Ip del servidor / DNS del cliente, es lo mismo] [algun nombre del dominio + nombre base de datos] --> Dig @172.28.5.1 sinco.asircastelao.int , nos devolvería (resolvería) la IP que sería 172.28.5.9.

Esta IP podemos ver en la Base de Datos que pertenece al nombre de dominio "sinco".

