# **Proyecto Loriot** 

|<a name="_page0_x94.00_y112.00"></a>**TFG ASIR II** 

Junio 19,2024 <a name="_page0_x295.00_y370.00"></a>— 

Administración de Sistemas Informáticos en Red 

<a name="_page0_x295.00_y448.00"></a>— 

**Lautaro Lorca Ciclo : Administración de Sistemas Informáticos en Red Memoria del proyecto de ASIR**

**IES La Senia. Curso 2023/24. Grupo 1. 19/06/2024 Javier García**

**Proyecto Loriot** 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.003.jpeg)

**Proyecto Loriot** 

<a name="_page2_x33.00_y64.00"></a> #ÍNDICE 
# ÍNDICE

- [TFG ASIR II](#_page0_x94.00_y112.00) ............................................................................................... 1
- [Proyecto Loriot](#_page0_x153.00_y293.00) ..................................................................................... 1
- — ............................................................................................................................................................. 1
- — ............................................................................................................................................................. 1
- [ÍNDICE](#_page2_x33.00_y64.00) ...................................................................................................... 3
- [INTRODUCCIÓN](#_page4_x33.00_y65.00) .......................................................................................... 5
- [Componentes del Proyecto](#_page6_x33.00_y36.00) .......................................................................... 7
  - [Azure Cloud:](#_page6_x33.00_y77.00) ............................................................................................ 7
  - [Jenkins VM:](#_page6_x33.00_y217.00) ............................................................................................ 7
  - [Terraform:](#_page7_x33.00_y380.00) ............................................................................................. 8
  - [Ansible:](#_page7_x693.00) ............................................................................................................. 8
  - [Prometheus y Grafana:](#_page8_x214.00) ......................................................................................... 9
  - [Balanceador de Carga:](#_page9_x36.00) .......................................................................................... 10
  - [Mongodb ReplicaSet:](#_page9_x182.00) ......................................................................................... 10
  - [Mongodb Replica Set Azure Locations:](#_page9_x479.00) ............................................................ 10
  - [Diagrama de flujo del proyecto:](#_page10_x374.00) ....................................................................... 11
- [JUSTIFICACIÓN](#_page11_x669.00) ................................................................................................. 12
- [OBJETIVOS DEL PROYECTO](#_page13_x33.00_y36.00) ................................................................... 14
  1. [Automatización de Infraestructura:](#_page13_x139.00) ................................................................. 14
  2. [Alta Disponibilidad:](#_page13_x203.00) .......................................................................................... 14
  3. [Despliegue Redundante:](#_page13_x268.00) ................................................................................... 14
  4. [Eficiencia Operativa:](#_page13_x333.00) ......................................................................................... 14
  5. [Monitorización Avanzada:](#_page13_x382.00) ................................................................................ 14
  6. [Escalabilidad:](#_page13_x446.00) ................................................................................................... 14
  7. [Seguridad:](#_page13_x495.00) ......................................................................................................... 14
- [PLANIFICACIÓN/EXPLICACIÓN](#_page14_x33.00_y36.00) ............................................................ 15
  - [Creación del directorio de Terraform:](#_page15_x33.00_y321.00) ................................................. 16
- [Resource Groups:](#_page17_x375.00) ............................................................................................... 18
  1. [1-LLA-TFG](#_page17_x408.00) ....................................................................................................... 18
  2. [2-LLA-TFG](#_page18_x36.00) ........................................................................................................ 19
  3. [3-LLA-TFG](#_page18_x367.00) ...................................................................................................... 19
- [Desarrollo de los playbooks de Ansible:](#_page19_x208.00) ............................................................ 20
- [Configuración del Load Balancer:](#_page19_x489.00) ..................................................................... 20
- [Monitoreo con Prometheus y Grafana:](#_page19_x569.00) ............................................................ 20
- [CONCLUSIONES](#_page21_x36.00) .................................................................................................. 22


**Proyecto Loriot** 

**Proyecto Loriot** 

<a name="_page4_x33.00_y65.00"></a>**INTRODUCCIÓN** 

Hoy en día, en un entorno tecnológico donde la agilidad, eficiencia y escalabilidad son esenciales para el éxito de cualquier empresa u organización, el despliegue de infraestructura en la nube se ha convertido en una necesidad más que una opción. 

Este proyecto tiene como objetivo diseñar e implementar una infraestructura en la nube utilizando herramientas de automatización y monitoreo para llevar la eficiencia, escalabilidad y disponibilidad de los servicios al siguiente nivel. Utilizaremos una combinación de varias  tecnologías de automatización de alto nivel, como Jenkins, Terraform, Ansible, Prometheus y Grafana, todas alojadas en la plataforma de Microsoft Azure teniendo como finalidad desplegar un servidor de bases de datos Mongodb Replica SET. 

Estas herramientas facilitarán nuestro trabajo diario al crear un entorno de automatización donde el despliegue de la infraestructura y su monitoreo se realizan con solo unos pocos clics. El objetivo principal es diseñar e implementar una infraestructura automatizada y escalable en la nube utilizando Terraform y Ansible. Esto permitirá crear, configurar y gestionar un clúster de MongoDB de manera eficiente y reproducible. La automatización reducirá demasiado el tiempo necesario para realizar el despliegue y la configuración de servicios, reduciendo los posibles errores humanos y garantizando la consistencia en entornos Linux más especificamente esta diseñado para Sistemas Operativos Ubuntus. 

Para garantizar la alta disponibilidad y la tolerancia a fallos, el clúster de MongoDB se configuraró como un replica set. Un replica set en MongoDB es un grupo de instancias de mongod que mantienen los mismos datos, proporcionando redundancia y aumentando la disponibilidad de los datos. En caso de que el servidor primario falle, uno de los servidores secundarios se promoverá automáticamente a primario, asegurando así la continuidad del servicio sin intervención manual. 

Además, para asegurar la disponibilidad del servicio web, se desplegarán dos máquinas virtuales adicionales en diferentes ubicaciones de Azure. Esto permitirá que, en caso de que una de las ubicaciones falle, el servicio continúe operativo desde la otra ubicación. Un balanceador de carga distribuirá las peticiones entrantes entre los dos servidores, garantizando una distribución eficiente del tráfico y aumentando la resiliencia del sistema. 

En resumen, este proyecto tiene como fin crear una infraestructura en la nube completamente automatizada y escalable. Utilizando Terraform para la provisión de la infraestructura y Ansible para la configuración de los servicios, se implementará un clúster de MongoDB con replica set y servidores web distribuidos en diferentes 

**Proyecto Loriot** 

ubicaciones. Esto garantizará la alta disponibilidad y la resiliencia del sistema, proporcionando un servicio confiable y eficiente. 

**Proyecto Loriot** 

<a name="_page6_x33.00_y36.00"></a>**Componentes del Proyecto** 

<a name="_page6_x33.00_y77.00"></a>**Azure Cloud:** 

- Utilizaremos la plataforma de Microsoft Azure para alojar nuestra infraestructura en la nube. Azure proporcionará los recursos necesarios, como máquinas virtuales, redes, y almacenamiento, para desplegar y operar nuestro sistema. 

<a name="_page6_x33.00_y217.00"></a>**Jenkins VM:** 

- ¿Qué es Jenkins? Es un servidor open source para la integración contigua. Se usa para probar y compilar proyectos de software de forma continua. Con Jenkins se facilita la incorporación de cambios en un desarrollo y la entrega de nuevas versiones. 
- Servirá como la herramienta de automatización de pipelines de CI/CD. Jenkins gestionará los procesos de integración y despliegue continuo, asegurando que los cambios en el código y la infraestructura se implementen de manera eficiente y sin errores. 

  Usaremos un pipline de tipo “Pipeline Script from SCM”, lo que hará sera bajar un repositorio desde Gitlab donde tendra su Pipline y todo lo necesario para la ejecución de Terraform y Ansible. 

**Proyecto Loriot** 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.004.jpeg)

<a name="_page7_x33.00_y380.00"></a>**Terraform:** 

- Terraform es una poderosa herramienta de infraestructura como código que permite a los equipos de TI y desarrolladores automatizar la creación y gestión de infraestructuras completas. Con Terraform, se puede definir, provisionar y actualizar recursos en la nube y en servidores locales usando código, lo que facilita la gestión de infraestructuras en múltiples nubes públicas y privadas. Esto asegura configuraciones consistentes, reproducibles y eficientes, ahorrando tiempo y reduciendo errores humanos. 
- Servirá como la herramienta de automatización de pipelines de CI/CD. Jenkins gestionará los procesos de integración y despliegue continuo, asegurando que los cambios en el código y la infraestructura se implementen de manera eficiente y sin errores. 

<a name="_page7_x33.00_y693.00"></a>**Ansible:** 

**Proyecto Loriot** 

- Ansible es una herramienta que automatiza la configuración y administración de sistemas informáticos. Permite definir y aplicar configuraciones en servidores y dispositivos de red de manera eficiente, simplificando tareas repetitivas y mejorando la consistencia y seguridad de los entornos de TI. 
- Empleado para la configuración automática de sistemas. A través de playbooks de Ansible, se instalarán y configurarán los servicios de bases de datos  en las máquinas virtuales, garantizando la consistencia y rapidez en la configuración de entornos. 

<a name="_page8_x33.00_y214.00"></a>**Prometheus y Grafana:** 

- Prometheus y Grafana son dos herramientas que se complementan para monitorizar y visualizar sistemas y aplicaciones: 
- **Prometheus** es un sistema de monitorización y alerta de código abierto diseñado para recopilar métricas de sistemas y servicios. Utiliza un modelo de datos basado en series temporales y permite consultar y visualizar estas métricas. 
- **Grafana** es una plataforma de visualización de métricas y análisis de datos de código abierto. Se integra con diversas fuentes de datos, incluido Prometheus, y permite crear cuadros de mando y gráficos interactivos para visualizar y analizar datos de métricas. 

**Cómo funcionan juntos:** 

- **Prometheus** recopila métricas de diferentes sistemas y servicios utilizando su propio servidor web y un modelo de almacenamiento de series temporales. 
- **Grafana** se conecta a Prometheus como fuente de datos para consultar y visualizar estas métricas en cuadros de mando personalizados. 
- Los usuarios pueden configurar alertas en Prometheus y visualizar estas alertas en Grafana, lo que proporciona una integración completa para monitorear y analizar el rendimiento de sistemas y aplicaciones. 

Esta combinación permite a los equipos de operaciones y desarrollo supervisar el rendimiento de sus sistemas en tiempo real y analizar tendencias históricas para mejorar la eficiencia y la confiabilidad de sus aplicaciones. 

- Estas herramientas se utilizarán para el monitoreo y la visualización de métricas. Prometheus recolectará datos de rendimiento y estado de los servicios, mientras que Grafana proporcionará paneles interactivos para visualizar estas métricas y facilitar el monitoreo en tiempo real. 

**Proyecto Loriot** 

<a name="_page9_x33.00_y36.00"></a>**Balanceador de Carga:** 

- El balanceador de carga se encargará de distribuir las peticiones de los clientes entre los servidores del MongoDB Replica Set. Al configurar un solo dominio o dirección IP para el balanceador de carga, éste redirigirá automáticamente las peticiones entrantes hacia los servidores disponibles en el Replica Set. Esto asegura que los clientes puedan acceder al servicio de base de datos de manera continua y sin interrupciones, incluso si uno de los servidores del Replica Set falla o está en mantenimiento. 

<a name="_page9_x33.00_y182.00"></a>**Mongodb ReplicaSet:** 

- Un MongoDB Replica Set es un grupo de servidores MongoDB que mantienen copias idénticas de los mismos datos para proporcionar alta disponibilidad y tolerancia a fallos. Consiste en un nodo primario que acepta operaciones de escritura y replica datos a nodos secundarios, que pueden ser configurados para permitir lecturas. En caso de fallo del nodo primario, un secundario se promueve automáticamente a primario, garantizando la continuidad del servicio. 
- Se desplegará un clúster de MongoDB configurado como replica set para garantizar la alta disponibilidad y tolerancia a fallos. Un replica set en MongoDB es un conjunto de instancias de bases de datos que mantienen los mismos datos, asegurando redundancia y continuidad del servicio en caso de fallos. 

<a name="_page9_x33.00_y479.00"></a>**Mongodb Replica Set Azure Locations:** 

**Proyecto Loriot** 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.005.jpeg)

<a name="_page10_x33.00_y374.00"></a>**Diagrama de flujo del proyecto:** 

**Proyecto Loriot** 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.006.jpeg)

<a name="_page11_x33.00_y669.00"></a>**JUSTIFICACIÓN**  

Este proyecto surgió gracias a mis prácticas realizadas en Loriot. Cuando ingresé a la empresa y comencé a trabajar, aprendí y me interioricé día a día en su funcionamiento. Me di cuenta de que el nivel de automatización de la empresa era fenomenal. Siempre 

**Proyecto Loriot** 

que hablaba con algún superior, veía que su enfoque estaba centrado en la escalabilidad, ya que la empresa está creciendo exponencialmente y saben que no pueden realizar todo el trabajo ellos manualmente. 

Por ejemplo, al ingresar un nuevo cliente, se crearía su entorno en alguna nube, creando las máquinas virtuales, desplegando su servicio y configurándolo a gusto del cliente. Este proceso llevaría demasiado tiempo si se hiciera manualmente. Por eso, utilizan tecnologías para desarrollar la automatización del despliegue, actualizaciónes, etc. Con herramientas como Terraform, solo se necesita ejecutar un comando, como "terraform apply", para tener toda la infraestructura física creada en la nube. Luego, con Ansible, ejecutando un "ansible-playbook", pueden desplegar todo su servicio. 

Un trabajo que antes tomaba muchas horas ahora se puede realizar con unos pocos comandos. Esta experiencia cambió mi mentalidad y me hizo pensar en función de la automatización y la escalabilidad. Así surgió la idea de este proyecto, donde utilizaremos estas tecnologías para desplegar un clúster de base de datos basado en un MongoDB replica set. 

**Proyecto Loriot** 

<a name="_page13_x33.00_y36.00"></a>**OBJETIVOS DEL PROYECTO** 

El proyecto tiene como objetivos principales: 

1. **Automatización<a name="_page13_x33.00_y139.00"></a> de Infraestructura:** Implementar un entorno de infraestructura automatizado en la nube utilizando Terraform y Ansible. Esto permitirá provisionar y configurar rápidamente los recursos necesarios para el despliegue de servicios. 
1. **Alta<a name="_page13_x33.00_y203.00"></a> Disponibilidad:** Configurar un clúster de MongoDB como replica set para garantizar la alta disponibilidad de los datos. Un replica set proporciona redundancia, permitiendo la promoción automática de servidores secundarios a primarios en caso de fallo. 
1. **Despliegue<a name="_page13_x33.00_y268.00"></a> Redundante:** Desplegar dos máquinas virtuales con servidores web en diferentes ubicaciones de Azure para asegurar la continuidad del servicio en caso de fallo de una ubicación. Un balanceador de carga distribuirá el tráfico entre ambos servidores. 
1. **Eficiencia<a name="_page13_x33.00_y333.00"></a> Operativa:** Reducir el tiempo y los errores asociados con el despliegue y la gestión de infraestructura y servicios mediante la automatización completa con herramientas como Terraform y Ansible. 
1. **Monitorización<a name="_page13_x33.00_y382.00"></a> Avanzada:** Implementar Prometheus y Grafana para la monitorización avanzada de la infraestructura y los servicios desplegados. Esto permitirá una visualización detallada del rendimiento y la salud del sistema en tiempo real. 
1. **Escalabilidad:<a name="_page13_x33.00_y446.00"></a>** Diseñar la infraestructura de manera que sea escalable, permitiendo el crecimiento y la expansión según las necesidades futuras de la empresa. 
1. **Seguridad:<a name="_page13_x33.00_y495.00"></a>** Implementar prácticas de seguridad recomendadas para proteger los datos y la infraestructura frente a amenazas y vulnerabilidades. 

Estos objetivos se orientan hacia la mejora de la eficiencia operativa, la disponibilidad y la escalabilidad de los servicios, asegurando un entorno de nube robusto y confiable para la organización. 

**Proyecto Loriot** 

<a name="_page14_x33.00_y36.00"></a>**PLANIFICACIÓN/EXPLICACIÓN** 

La planificación y avance de este proyecto se basaron en un aprendizaje y práctica constantes. Comencé realizando un curso de Terraform en udemy gracias a que la empresa tiene una cuenta de udemy donde puedo realizar estos cursos, gracias a esto pude realizar cursos y especializarme un poco más tanto en Mongodb como en Terraform y principalmente en Ansible que lo ocupo a díario para mí trabajo dentro de la emresa. 

Para lograr relacionarme con Terraform + Azure el proceso fue crear y destruir entornos para ir encontrando fallos y entendiendo como se relacionaba cada componente de Azure entre si. 

Como en la empresa trabajo constantemente con Ansible y sobre los servidores de MongoDB, no tuve que realizar tanta tarea adicional como con Terraform, pero sí hice pruebas particulares de cada componente del proyecto, independientemente unos de otros. 

Hice despliegues en local de cada componente/tecnología que iba a utilizar para entender a fondo como es su infraestructura internay comportamiento. 

1. Una vez comprendido el funcionamiento de cada componente (Terraform/Azure, Ansible, Replica Set de MongoDB, y Azure Load Balancer), inicié el proyecto desde cero, comenzando a crear y relacionar cada componente para formar el proyecto completo. 
1. Jenkins VM : El primer paso fue desplegar un servidor de Jenkins en una una VM de azure para realizar el proceso de automatización con piplines de Jenkins. Todo el proceso será gestionado desde esta máquina. 

**Proyecto Loriot** 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.007.jpeg)

2. **Creación<a name="_page15_x33.00_y321.00"></a> del directorio de Terraform:** Primero, creamos el directorio de Terraform donde comenzaremos con la creación de tres grupos de recursos (resource groups) en diferentes ubicaciones de Azure para asegurarnos de que, en caso de que un servidor de Azure falle, nuestro Replica Set seguirá funcionando.  Aquí no solo crearemos las maquinas virtuales sino que crearemos toda una configuración de seguridad y red para tener las VMs controladas y con una ip pública. 

   ![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.008.png)

   Con toda la estructura creada para poder ejecutar terraform y crear la infraestructura en la nube debemos ejecutar 3 comandos: 

**Proyecto Loriot** 

- terraform init : Se encarga de inicializar un directorio de trabajo con archivos de configuración de Terraform, establece todos los componentes necesarios para que Terraform pueda gestionar y desplegar la infraestructura correctamente. 
- terraform plan: Permite visualizar las acciones que Terraform realizará para alcanzar el estado deseado de la infraestructura, descrito en los archivos de configuración.Aquí podemos ver que al ejecutarlo tenemos 10 planes para ejecutar. 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.009.png)

- terraform apply: Después de generar y revisar el plan de ejecución con terraform plan, terraform apply aplica efectivamente esos cambios, creando, modificando o destruyendo recursos en el proveedor de infraestructura (como Azure). 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.010.png)

Ahora si vamso a nuestro portal de azure podremos ver la infraestructura creada, aqúi veremos los 3 grupos en diferentes regiones: 

**Proyecto Loriot** 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.011.jpeg)

Ahora si entramos dentro de cada grupo podremos ver todo lo que creamos a traves de Terraform como la VM,IP,SSH,etc. 

<a name="_page17_x33.00_y375.00"></a>Resource Groups: 

<a name="_page17_x33.00_y408.00"></a>**1-LLA-TFG**

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.012.jpeg)

**Proyecto Loriot** 

<a name="_page18_x33.00_y36.00"></a>**2-LLA-TFG** 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.013.jpeg)

<a name="_page18_x33.00_y367.00"></a>**3-LLA-TFG** 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.014.jpeg)

Y podemos comprobar el acceso a las 3 vms que lo tenes permitido por clave ssh desde el inventory: 

**Proyecto Loriot** 

![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.015.jpeg)

3. **Desarrollo<a name="_page19_x33.00_y208.00"></a> de los playbooks de Ansible:** Una vez configuradas las máquinas, comenzamos con el desarrollo de los playbooks de Ansible.  

   Estos playbooks se encargan de la instalación del Replica Set de MongoDB y también incluyen scripts para actualizar MongoDB según salgan nuevas versiones. 

   La estructura de ansible se basa en 2 directorios (ansible,inventory), en ansible solo se encontraran los playbooks que son los encargados de ejecutar cualquier tarea y luego el inventory que es donde estan todas las especificaciones de los host/servidores aquí se encontrarán todas las variables particulares de cada host, el nombre, la conexión y todo lo necesario de cada host. 

   ![](Aspose.Words.0d40ce37-0fd2-42fe-8062-c6b1da16bf86.016.png)

4. **Configuración<a name="_page19_x33.00_y489.00"></a> del Load Balancer:** Configuramos el balanceador de carga (Load Balancer) con nginx para que maneje el tráfico hacia los servidores y distribuya las peticiones de manera eficiente, asegurando que las consultas (queries) se dirijan correctamente a los servidores disponibles. 
4. **Monitoreo<a name="_page19_x33.00_y569.00"></a> con Prometheus y Grafana:** Configuramos Prometheus y Grafana en la máquina de Jenkins para monitorear los servidores. Esto nos permitirá tener una visión clara y en tiempo real del estado y rendimiento de nuestros servicios, facilitando la detección y resolución de posibles problemas. Crearemos nuestros propios dashbords y templeates para lograr tener una monotorización buena de nuestro cluster. 

En resumen, la planificación del proyecto implica una serie de pasos bien definidos para asegurar la automatización y escalabilidad de la infraestructura en la nube, garantizando alta disponibilidad y eficiencia operativa. Cada componente ha sido cuidadosamente integrado y probado para cumplir con los objetivos del proyecto y proporcionar un entorno robusto y fiable.  

**Proyecto Loriot** 

**Proyecto Loriot** 

<a name="_page21_x33.00_y36.00"></a>**CONCLUSIONES** 

Personalmente, al reflexionar sobre este proyecto y mi experiencia en Loriot durante estos meses, así como mis dos años cursando el grado superior de ASIR, puedo decir que el nivel de aprendizaje y desarrollo personal que he alcanzado ha sido sorprendente. Trabajar en Loriot y sumergirme en el mundo laboral ha abierto un amplio abanico de oportunidades de aprendizaje. 

Ingresé al ciclo superior sin ningún conocimiento previo en el ámbito informático, y hoy estoy desarrollando proyectos como este. Esto es algo que no habría imaginado al comenzar el curso. Los dos años de estudio y la experiencia en Loriot me han dado las herramientas y el conocimiento necesario para desarrollar proyectos complejos como este, utilizando tecnologías de vanguardia y prácticas de automatización. 

En cuanto a las conclusiones específicas del proyecto, creo que realmente ha cambiado mi enfoque frente a cualquier situación en la vida. Ahora entiendo la importancia de pensar en soluciones que no solo resuelvan problemas momentaneos, sino que también estén diseñadas para ser escalables y sostenibles a largo plazo. Esto es fundamental tanto en el entorno empresarial como en la vida personal. 

Este proyecto se centra en la automatización no solo por el hecho de automatizar acciones o procesos, sino porque entiendo que es crucial para el crecimiento de una empresa, la eficiencia en el tiempo de los empleados y para realizar un trabajo que no solo esté bien hecho, sino que también ahorre recursos críticos para el funcionamiento diario de una empresa. 

En resumen, este proyecto no solo me ha permitido aplicar mis habilidades técnicas y conocimientos adquiridos, sino que también me ha enseñado lecciones valiosas sobre la importancia de la automatización, la planificación a largo plazo y el crecimiento personal y profesional. 

**Proyecto Loriot** 

**REFERENCIAS** 

Documentación utilizada: 

Ansible -[ https://www.ansible.com/ ](https://www.ansible.com/)

Terraform -[ https://www.terraform.io/ ](https://www.terraform.io/)

Mongodb -[ https://www.mongodb.com/docs/ ](https://www.mongodb.com/docs/)

Microsoft Azure -[ https://learn.microsoft.com/en-us/azure/?product=popular ](https://learn.microsoft.com/en-us/azure/?product=popular)

Terraform + Azure -[ https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs ](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)

Udemy -[ https://www.udemy.com/?utm_source=aff- campaign&utm_medium=udemyads&LSNPUBID=OzpaRYwFVr0&ranMID=47901&ranEAID=Ozpa RYwFVr0&ranSiteID=OzpaRYwFVr0-q3b9xb70wzWMkSNenjyMcg ](https://www.udemy.com/?utm_source=aff-campaign&utm_medium=udemyads&LSNPUBID=OzpaRYwFVr0&ranMID=47901&ranEAID=OzpaRYwFVr0&ranSiteID=OzpaRYwFVr0-q3b9xb70wzWMkSNenjyMcg)

Load Balancer -[ https://azure.microsoft.com/es-es/products/load-balancer/ ](https://azure.microsoft.com/es-es/products/load-balancer/)Jenkins -[ https://www.jenkins.io/doc/ ](https://www.jenkins.io/doc/)

Gitlab -[ https://docs.gitlab.com/ ](https://docs.gitlab.com/)

Genially - https://app.genially.com/teams/6668a2418fecf10013d0066a/spaces/6668a2418fecf10013d00687/d ashboar 
22  **Lautaro Lorca**
