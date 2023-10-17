# contenedorDNS

services: → Formará un bloque (x nombre), cada uno con dicha configuración.

  bind9: → nombre del servicio

    image: internetsystemsconsortium/bind9:9.18 → nombre de la imagen y version

    container_name: asir_bind9 → nombre del contenedor

    restart: always → Para que el servicio se reinicie siempre una vez se detenga

    ports: →Especifica la asignación de puertos entre el sistema host y el contenedor. En este caso, estás mapeando el puerto 53 del sistema host al puerto 53 del contenedor, lo que permite que el contenedor de BIND9 atienda las solicitudes DNS en el puerto 53 del host.
          - "53:53"

    volumes: → Donde almacenas los datos
          - ./conf:/etc/bind
          - ./lib:/var/lib/bind

    environment: Zona donde se hará el servicio
          - TZ=Europe/París

“Volumes”: Permiten almacenar datos fuera de un contenedor, lo que significa que los datos sobreviven incluso si se elimina o se recrea el contenedor.

# Probar cosas

Para meterse dentro del contenedor , lo buscamos y hacemos clic derecho donde le daremos a "Attach shell" o escribimos "docker exec -it asir_bin9 bash"

$apt update
$apt install -y dnsutils
