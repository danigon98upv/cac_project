# Proyecto CAC.  Servidor web y de cómputo en clúster con alta disponibilidad y distribución de carga

El proyecto consiste en configurar un servidor de Internet basado en clúster. El sistema aceptará peticiones HTTP y las distribuirá entre los nodos servidores del clúster. Adicionalmente, el clúster podrá funcionar como servidor de cómputo, aceptando trabajos secuenciales o paralelos de los usuarios y gestionando su ejecución sobre los nodos del clúster. El modo de funcionamiento se seleccionará en el momento de arranque del clúster.

## Descripción Básica del Clúster

El clúster estará formado por 6 nodos como los mostrados en la imagen. Las funciones asociadas a los nodos son las siguientes:

• master y standby: nodos maestros. Están duplicados para conseguir alta disponibilidad, componiendo un servicio activo-pasivo (master-standby). Forman el front-end del sistema. Hacia el exterior (Internet), ofrecen el servicio web en el puerto 80 de una dirección IP virtual asociada al nodo que en cada momento está activo. Además de las funciones propias del nodo maestro de un clúster, también se ocupará de distribuir la carga, repartiendo las peticiones HTTP recibidas entre los servidores reales del back-end. Inicialmente, el maestro activo es master. Cuando standby detecta la caída de master o del proceso de distribución de carga que allí se ejecuta, toma el relevo.

• server1, server2, server3: servidores web reales. Forman el back-end del sistema. Tienen instalado un servidor apache que atiende las peticiones que les deriva el nodo maestro activo. La comunicación entre el nodo maestro y los servidores se realiza a través de la red interna del clúster.

• NFS: servidor de almacenamiento. Es un servidor NFS. Las páginas web proporcionadas por los servidores reales están almacenadas aquí.
