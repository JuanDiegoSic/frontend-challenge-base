<div align="left">
  <img src="https://img.shields.io/static/v1?message=Gmail&logo=gmail&label=&color=D14836&logoColor=white&labelColor=&style=for-the-badge" height="35" alt="gmail logo"  />
  <img src="https://img.shields.io/static/v1?message=LinkedIn&logo=linkedin&label=&color=0077B5&logoColor=white&labelColor=&style=for-the-badge" height="35" alt="linkedin logo"  />
</div>

# Prueba técnica  - Solucion por Juan Diego Sicachá Cortes

Este repositorio contiene la solucion de los problemas planteados para la prueba técnica de devops

---

## 1. Diseño de Infraestructura
### Enunciado
Diseñar una arquitectura para implementar una aplicación web escalable. La solución incluye:

- **Uso de contenedores:** Docker para empaquetar la aplicación.
- **Orquestación:** Kubernetes para la gestión de contenedores.
- **Base de datos:** Integración con PostgreSQL o MongoDB con alta disponibilidad.
- **Pipeline CI/CD:** Despliegues automáticos.
- **Monitoreo del sistema:** Prometheus y Grafana.

### Solución
![Diseño CI/CD](https://github.com/user-attachments/assets/b144e8b5-e63f-4abd-9e97-09a7aa5f9085)

La propuesta de diseño creada muestra un panorama de CI/CD que evidencia el flujo desde que el programador planea un cambio hasta que el usuario final utiliza el programa desplegado.
- **CI Pipeline:**

1. Planning: Proceso de análisis de nuevas mejoras al programa, solucion de bugs o cambios que afectan el programa 
2. Code: Proceso donde el desarrollador empieza a codificar el feature desde su local, realizando cambios o creando nuevas lineas de código en un repositorio
3. Build: Proceso donde sube sus cambios al repositorio para construir el nuevo proyecto listo para pruebas
4. Unit Test: Proceso donde el desarrollador crea pruebas unitarias en su nuevo código para verificar la calidad del mismo, reduciendo asi el ingreso de bugs y que ayuda a verificar el funcionamiento no solo de sus cambios si no de todo el proyecto
  
- **CD Pipeline:**
    - **Docker:**

      1. Release: Proceso de empaquetado de código para despliegue, cuenta con subproceso de generacion de contenedor a partir de Docker
      2. DockerFile: Archivo que contiene la logica de empaquetado, donde verifica funcionamiento de código, identificando errores
      3. Package proceso de empaquetado usando el dockerfile para cargar en docker todo el código nuevo en un paquete
      4. Version: Proceso donde se realiza un versionamiento del paquete que realiza una identificación, generalmente es un tag autoincremental o con la fecha de empaquetado
      5. Container Registry: proceso donde se almacenan todos los paquetes de los repositorios, estos estan catalogados por microservicios y tag para identificar siempre el paquete mas reciente
      6. Icono de github Action ya que se propone que todo este proceso de docker es posible automatizarlo desde esta herramienta, haciendo que sea transparente para el desarrolLador todo este proceso y dandole como entrega el paquete y su tag
    - **Deploy:** Proceso en el que se realiza despliegue al cluster de imagen creando en docker, este deployment va directamente al cluster y puede usar una serie de comandos con Helm y kubectl para subir todos los recursos necesarios para el funcionamiento del microservicio
    - **Kubernetes:**

      1. Operate - Cluster: Hace referencia al orquestador, donde se ejecuta en tiempo real el programa desplegado y es el recurso principal en donde esta compuesto por microservicios, conexion de base de datos, configuracion de network, comunicacion con peticiones, etc 
      2. Microservice: serie de yaml que componen un microservicio, para su funcionamiento y comunicacion con el gateway y otros recursos, requiere diferentes recursos como: 
                      - Deployment: contiene informacion de los recursos necesarios para el funcionamiento del servicio
                      - HPA: recursos que contiene informacion de replicas, esto permite que el microservicio sea autoincremental debido a que se define cuantos pods pueden estar disponibles segun su demanda
                      - PDB: recurso que garantiza disponibilidad minima
                      - Service: recurso que define reglas de acceso
                      - ConfigMap: Recurso utilizado para almacenar datos de configuracion
    - **Grafana:**  

      1. Monitor: Herramienta que permite revisar el estado del cluster, permitiendo adelantarse a problemas o posibles inconvenientes
      2. Dashboard: Herramienta dentro del monitor que ofrece informacion de los recursos y su estado
      3. Alerts: Herramienta que permite alertar a los involucrados de problemas criticos en el cluster, ya sea de un microservicio o un recurso que no esta funcionando o esta en estado grave
      4. Metrics: Herramienta que permite medir desde el tiempo el funcionamiento de servicios y revision de logs
- **DataBase:**

1. Pvc: es una solicitud de almacenamiento persistente hecha por una aplicación
2. LoadBalancer: servicio que proporciona acceso externo a la base de datos a través de un balanceador de carga.
3. ReplicaSet: asegura que un número específico de Pods (réplicas)

- **Network:**

1. Istio: Herramienta que opera toda la red del cluster, responsable de comunicar todos los recursos y asignar ips para identificarlos
2. Control Plane: Gestiona el estado deseado del clúster y actúa como "cerebro" del sistema
3. Load Balancer: Distribuye el tráfico de red entrante entre varios Pods o nodos de manera eficiente.


---

## 2. Implementación de un Pipeline CI/CD
### Enunciado
Crear un pipeline de CI/CD para una aplicación Node.js basado en el siguiente repositorio: GitHub - sport-enlace-sas/frontend-challenge-base

- Clonar el repositorio desde GitHub.
- Construir y testear la imagen Docker.
- Publicar la imagen en un registry público/privado.
- Desplegar la aplicación automáticamente en un clúster Kubernetes usando
ArgoCD.

### Solución
En este mismo repositorio se realizaron las modificaciones necesarias para el funcionamiento del pipeline y uso de ArgoCD
#### Ejecucion en local

- Ejecucion de comando npm run build:

<img src="https://github.com/user-attachments/assets/4e76eba4-26bf-412b-996c-763d8dfb352f" width="60%"/>

- Archivo DockerFile creado y ejecucion:
  
<img src="https://github.com/user-attachments/assets/d23ceb50-b64e-4c59-b0a5-8c2b2a1a38c0" width="60%"/>

- Pagina de inicio:
  
<img src="https://github.com/user-attachments/assets/db78414c-d815-4419-a823-4bb62a1d6fce" width="60%"/>

- Proyecto montado en cluster local con pods corriendo:
  
<img src="https://github.com/user-attachments/assets/62c04057-9a8a-4f22-9566-aa8de58210c4" width="60%"/>

- Consumo y logs exitosos:
  
<img src="https://github.com/user-attachments/assets/2000bf12-ff91-402f-82b6-52b3c9fb4f2f" width="60%"/>

-Sincronización con ArgosCD:
  
<img src="https://github.com/user-attachments/assets/fdd577d1-2222-4790-9000-48ae1f5779ae" width="60%"/>

#### Archivo de configuración para el pipeline
El siguiente link los llevara a ver el yaml creado para el CI/CD y sincronización con ArgoCD: https://github.com/JuanDiegoSic/frontend-challenge-base/blob/main/.github/workflows/pipeline.yaml

##### Explicación
- **Job build-CICD:** Este Job contiene los steps para montar la imagen a docker hub, cuenta con dos secretos que son el usuario y contraseña de dockerhub para montar el paquete en la cuenta correspondiente
        - Inicia con clonar el repositorio, ejecutar comandos de docker para construir, loguearse y hacer push al código
  
- **deploy-Argo:** Este Job contiene los steps para crear un cluster, instalar ArgosCD y sincronizar el servicio
        - Inicia con clonar el repositorio, instalar minikube para creear un cluster local en la maquina virtual, se instala ArgosCD, una vez creado el cluster , se implementan recursos (Archivos de configuración para ArgoCD) en cluster, se realiza portforward para ingresar a la interfaz de argoCD, se accede a credenciales genericas, se ejecuta comando de sincronizacion

#### Archivos de configuración para ArgoCD.
En la carpeta "k8s" se crearon 4 archivos para el funcionamiento del servicio en el cluster y sincronizacion de ArgosCD
- argo-app.yaml: Manifiesto de configuración utilizado por ArgoCD para definir y gestionar aplicaciones dentro de un clúster de Kubernetes. https://github.com/JuanDiegoSic/frontend-challenge-base/blob/main/k8s/argo-app.yaml
- deployment.yaml: Permiten gestionar el ciclo de vida de las aplicaciones, incluyendo la creación, actualización y escalado de réplicas de Pods. https://github.com/JuanDiegoSic/frontend-challenge-base/blob/main/k8s/deployment.yaml
- rolebinding.yaml: Se utiliza para crear un RoleBinding en Kubernetes, que asigna un Role o ClusterRole a un User. https://github.com/JuanDiegoSic/frontend-challenge-base/blob/main/k8s/rolebinding.yaml
- service.yaml: recurso que expone una aplicación en ejecución en un conjunto de Pods como un servicio de red estable https://github.com/JuanDiegoSic/frontend-challenge-base/blob/main/k8s/service.yaml

---

## 3. Solución de Problemas
### Enunciado
Basado en el siguiente docker compose docker-compose.yaml , corregir el archivo que está mal construído y optimizado

### Solución
EN el siguiente link van a ver el yaml optimizado y arreglado , cuanta con comentarios acerca de cada uno de los cambios: https://github.com/JuanDiegoSic/frontend-challenge-base/blob/main/docker-compose.yaml

- **app:**
  
          app:
            image: nginx:latest
            ports:
              - "8080:80"
            environment:
              NODE_ENV: "production"
            depends_on:
              database:
                condition: service_healthy #Practica para garantizar que esta dependencia se cumpla correctamente cuando el contenedor database aparte de iniciar, pase una comprobacion de estado
              - app_network
            restart: unless-stopped  #Implementacion de reinicio para el contenedor, buena practica por si falla, le permite reiniciars

  Se realizo un ajuste a depends_on para mejorar su funcionamiento, se agrego una funcionalidad nueva en caso de errores

  
- **database:**
  
          database:
            image: postgres:alpine #Opcion de cambio dependiendo de logica de negocio, dado que es una imagen de un servicio externo , para evitar temas de versiones deprecadas en un futuro, se puede usar tag de ultima version "postgres:latest"
            volumes:
              - pg_data:/var/lib/postgresql/data
            environment:
              POSTGRES_USER: ${{ secrets.POSTGRES_USER }}    #CORRECCION: no se dejan datos sensibles a simple vista, se puede aprovechar los secretos de github para guardar esta informacion, y llamarla en código
              POSTGRES_PASSWORD: ${{ secrets.POSTGRES_PASSWORD }}
              POSTGRES_DB: ${{ secrets.POSTGRES_DB }}
            ports:
              - "5432:5432"
            networks:
              - app_network
            restart: unless-stopped  #Implementacion de reinicio para el contenedor, buena practica por si falla, le permite reiniciarse

  Se identifico mejor en la imagen obtenida, se soluciono problema grave con datos sensibles quemados, se agrego una funcionalidad nueva en caso de errores

  - **redis:**
  
          redis:
            image: redis #Verificar version de la imagen que se esta usando y quemarla, para evitar posibles cambios de actualizaciones que afecten el servicio
            container_name: redis #Dado que se trata de un servicio de almacenamiento, es buena opcion estipular un contenedor en caso de reinicio volver a obtener los datos registrados previamente
            command: redis-server --requirepass "${{ secrets.REQUIRE_PASS }}" #Este es un dato sensible que debe guardarse en un secreto, se puede usar secretos de github y llamarlo
            ports:
              - "6379:6379"
            restart: unless-stopped #Implementacion de reinicio para el contenedor, buena practica por si falla, le permite reiniciarse

  Se identifica problema con imagen de redis al no tener version, funcionalidad implementada de container fijo, solucion de error grave de dato sensible quemado,  se agrego una funcionalidad nueva en caso de errores

  - **redis:**
 
            volumes:
            pg_data:
              driver_opts: #Para controlar el espacio de este volumen se puede especificar el tamaño
                size: "20GB"

  Se optimiza el tamaño del volumen a trabajar

  - **networks:**
 
          networks:
            app_network:
              driver: bridge
              ipam: #COntrol de ip, se puede agregar esta opcion para controlar las ips de los recursos que van a utilizar esta network , esto permite generar medidas de seguridad para acceso a ips permitidas
                config:
                  - subnet: 192.168.1.0/12
              driver_opts:
                com.docker.network.bridge.enable_ip_masquerade: "true" #Opcion para habilitar el enmascaramiento de IP

  Se optimiza el rango de ips a utilizar en la reds, se implementa habilitacion de enmascaramiento

