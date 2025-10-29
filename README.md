# Desafío DIO: Gestión de Instancias EC2 en AWS 

##  Objetivo del Desafío

Este repositorio tiene como objetivo **consolidar los conocimientos en gestión de instancias EC2 en Amazon Web Services (AWS)**, con un enfoque particular en la **creación y uso de AMIs (Amazon Machine Images) y Snapshots de EBS (Elastic Block Store)**.

Sirve como material de apoyo, anotaciones e *insights* adquiridos durante la práctica, demostrando la comprensión de los conceptos discutidos en el bootcamp de la DIO.

---

##  Conceptos Fundamentales Practicados

Durante el desarrollo de este desafío, se aplicaron y documentaron los siguientes conceptos clave de AWS y la nube:

* **Lanzamiento y Conexión a Instancias EC2:** Creación de una instancia EC2 base (por ejemplo, con Amazon Linux o Ubuntu) y conexión vía SSH.
* **Gestión de Almacenamiento (EBS):** Entendimiento de los volúmenes EBS y su ciclo de vida.
* **Creación de Snapshots de EBS:** Realización de copias de seguridad a nivel de bloque (Snapshots) de los volúmenes EBS de la instancia, como estrategia de **recuperación de desastres (DR)** y **migración**.
* **Creación de AMIs Personalizadas:** Generación de una AMI a partir de la instancia EC2 configurada, lo cual permite:
    * **"Golden Images":** Crear copias exactas y preconfiguradas del servidor para un lanzamiento rápido.
    * **Escalabilidad:** Implementar rápidamente nuevas instancias idénticas para manejar picos de tráfico.
* **Lanzamiento de Instancias a partir de AMI:** Utilización de la AMI personalizada para lanzar nuevas instancias EC2 idénticas a la original.
* **Documentación Técnica:** Uso de Markdown y Git/GitHub para la organización y el *versionamiento* de la documentación.

---

##  Anotaciones e Insights Clave

Aquí se detallan los pasos realizados y las reflexiones obtenidas durante la práctica:

### 1. Preparación de la Instancia Base

* Se lanzó una instancia EC2 (`t2.micro`) con el sistema operativo **[Indicar el SO utilizado, ej: Amazon Linux 2023]**.
* Se realizaron **configuraciones iniciales** (ej: instalación de un servidor web como Apache/Nginx o la creación de un archivo de prueba).
* **Insight:** Antes de crear la AMI o el Snapshot, es crucial asegurarse de que la aplicación esté en un **estado consistente** (a menudo mediante el *quiescing* de la aplicación o el sistema de archivos) para evitar datos corruptos.

### 2. Creación del Snapshot de EBS

* **Paso a paso:** Se navegó a la consola de **Volúmenes EBS**, se identificó el volumen raíz de la instancia y se creó un Snapshot.
* **Caso de Uso:** El Snapshot es ideal para **copias de seguridad de datos** y volúmenes individuales. Un Snapshot puede restaurarse a un **nuevo volumen EBS** en cualquier Zona de Disponibilidad (AZ) de la misma región.
* **Comando/Acción Clave:** `Acciones > Crear Snapshot`.


### 3. Creación de la AMI Personalizada

* **Paso a paso:** Se seleccionó la instancia EC2 base y se eligió la opción para **crear una imagen (AMI)**.
* **Caso de Uso:** La AMI es una **plantilla completa** que incluye la configuración de la instancia (bloque de arranque, permisos, *layout* de disco y los datos del volumen raíz/EBS). Es la forma más rápida de *provisionar* nuevos servidores idénticos.
* **Diferencia clave con Snapshot:** La AMI te permite lanzar una nueva *instancia completa* directamente. El Snapshot solo te permite lanzar un *volumen*. La creación de una AMI automáticamente crea un Snapshot subyacente.


### 4. Verificación y Uso de la AMI

* Se lanzó una **nueva instancia EC2** seleccionando la AMI personalizada en el paso de selección de imagen.
* **Resultado:** La nueva instancia arrancó con todas las configuraciones y archivos que se habían creado en la instancia base, validando el proceso.
* **Aprendizaje:** Este proceso es la base de la **Infraestructura como Código (IaC)** y fundamental para entornos **DevOps** que buscan inmutabilidad.

---
