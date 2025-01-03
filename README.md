        # Prueba tecnica  - Solucion por Juan Diego Sicachá Cortes

Este repositorio contiene la solucion de los problemas planteados para la prueba tecnica de devops

---

## 1. Diseño de Infraestructura
### Enunciado
Diseñar una arquitectura para implementar una aplicación web escalable. La solución incluye:

- **Uso de contenedores:** Docker para empaquetar la aplicación.
- **Orquestación:** Kubernetes para la gestión de contenedores.
- **Base de datos:** Integración con PostgreSQL o MongoDB con alta disponibilidad.
- **Pipeline CI/CD:** Despliegues automáticos.
- **Monitoreo del sistema:** Prometheus y Grafana.

### Solucion
![Diseño CI/CD](https://github.com/user-attachments/assets/b144e8b5-e63f-4abd-9e97-09a7aa5f9085)

La propuesta de diseño creada muestra un panorama de CI/CD que evidencia el flujo desde que el programador planea un cambio hasta que el usuario final utiliza el programa desplegado.
- **CI Pipeline:**

      1. Planing: Proceso de analisis de nuevas mejoras al programa, solucion de bugs o cambios que afectan el programa 
      2. Code: Proceso donde el desarrollador empieza a codificar el feature desde su local, realizando cambios o creando nuevas lineas de codigo en un repositorio
      3. Build: Proceso donde sube sus cambios al repositorio para construir el nuevo proyecto listo para pruebas
      4. Unit Test: Proceso donde el desarrolador crea pruebas unitarias en su nuevo codigo para verificar la calidad del mismo, reduciendo asi el ingreso de bugs y que ayuda a verificar el funcionamiento no solo de sus cambios si no de todo el proyecto
  
- **CD Pipeline:**
    - **Doker:**

            1. Release: Proceso de empaquetado de codigo para despliegue, cuenta con subproceso de generacion de contenedor a partir de Docker
            2. DockerFile: Archivo que contiene la logica de empaquetado, donde verfica funcionamiento de codigo, identificando errores
            3. Package proceso de empaquetado usando el dokerfile para cargar en docker todo el codigo nuevo en un paquete
            4. Version: Proceso donde se realiza un versionamiento del paquete que realiza una identificacion, generalmente es un tag autoincremental o con la fecha de empaquetado
            5. Container Registry: proceso donde se almacenan todos los paquetes de los repositorios, estos estan catalogados por microservicios y tag para identificar siempre el paquete mas reciente
        Icono de github Action ya que se propone que todo este proceso de docker es posible automatizarlo desde esta herramienta, haciendo que sea transparente para el desarrolador todo este proceso y dandole como entrega el paquete y su tag
    - **Deploy:** Proceso en el que se realiza despliegue al cluster de imagen creando en docker, este deployment va directamente al cluster y puede usar una serie de comandos con Helm y kubectl para subir todos los recursos necesarios para el funcionamiento del microservicio
    - **Kubernetes:**

            1. Operate - Cluster: Hace referencia al orquestador, donde se ejecuta en tiempo real el programa desplegado y es el recurso principal en donde esta compuesto por microservicios, conexion de base de datos, configuracion de network, comunicacion con peticiones, etc 
            2. Microservice: serie de yalm que componen un microservicio, para su funcionamiento y comunicacion con el gateway y otros recursos, requiere diferentes recursos como: 
                            - Deployment: contiene informacion de los recursos necesarios para el funcionamiento del servicio
                            - HPA: recursos que contiene informacion de replicas, esto permite que el microservicio sea autoincremental debido a que se define cuantos pods pueden estar disponibles segun su demanda
                            - PDB: recurso que garantiza disponibilidad minima
                            - Service: recurso que define reglas de acceso
                            - ConfigMap: Recurso utlizado para almacenar datos de configuracion
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

### Solucion
En este mismo repositorio se realizaron las modificaciones necesarias para el funcionamiento del pipeline y uso de ArgoCD
#### Ejecucion en local

- Ejecucion de comando npm run build:

<img src="https://github.com/user-attachments/assets/4e76eba4-26bf-412b-996c-763d8dfb352f" width="60%"/>

- Archivo DockerFile creado y ejecucion:
  
<img src="https://github.com/user-attachments/assets/d23ceb50-b64e-4c59-b0a5-8c2b2a1a38c0" width="60%"/>

- Pagina de inicio:
  
<img src="https://github.com/user-attachments/assets/db78414c-d815-4419-a823-4bb62a1d6fce" width="60%"/>





  
