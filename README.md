


# Proyecto Segunda Evaluación

  

<img src="https://raw.github.com/alejandroasc96/documentacion2Proyecto/master/imgDoc2Eva/presentacion.jpg" width="500">

  

Alejandro Santana Carreño
Bryan Jaramillo Baldeón

## Descripción

En este proyecto se va a trata la necesidad de crear un sistema genérico que permita el envío de notificaciones a todas las aplicaciones que tiene InventiaPlus actualmente en funcionamiento. Dicho sistema debe permitir la administración de administradores, aplicaciones y notificaciones. Para el envío de la notificación lo que hará nuestro proyecto es comunicarse mediante nuestra API con la API de firebase para que sea esta última quien gestione el envío de la notificación  a los diferentes dispositivos donde se encuentra una aplicación registrada.


<img src="https://raw.github.com/alejandroasc96/documentacion2Proyecto/master/imgDoc2Eva/ideaGenerica.png" width="500">  


Este sería una representación simplificada de nuestro sistema donde se puede observar lo explicado. Una vez realizado nuestro boceto procedemos a desglosar todas las acciones que va a realizar nuestro usuario con el sistema con la ayuda de un **diagrama** de **caso de uso**.

<img src="https://raw.github.com/alejandroasc96/documentacion2Proyecto/master/imgDoc2Eva/DiagramaCasoUso.png" width="500">  

Gracias a este diagrama observamos que el administrador root una vez que inicia sesión puede gestionar la notificaciones , realizar un envío de notificación y última instancia puede generar nuevos administradores los cuales pueden realizar las mismas tareas menos gestionar otros usuarios. En última instancia se observa que el usuario simplemente podrá ver la notificación en su dispositivo.

## Pila Tecnológica

  

### Bases de Datos
<img src="https://raw.github.com/alejandroasc96/documentacion2Proyecto/master/imgDoc2Eva/imgBasesDatos.png" width="500"> 
### API

 <img src="https://raw.github.com/alejandroasc96/documentacion2Proyecto/master/imgDoc2Eva/imgAPI.png" width="500"> 
### Vista

<img src="https://raw.github.com/alejandroasc96/documentacion2Proyecto/master/imgDoc2Eva/imgVista.png" width="500"> 
  

## Proyecto

  

### Diseño base de datos

Visto el concepto de la aplicación pasamos el diseño de la misma. Primero transformaremos nuestro diagrama de caso de uso a un **diagrama de clase**.

<img src="https://raw.github.com/alejandroasc96/documentacion2Proyecto/master/imgDoc2Eva/diagramaClases.png" width="500">

En dicho diagrama observamos que poseemos una clase  llamada **Admin** donde se encuentran los dos tipos de administradores que hay en nuestro sistema (administrador root, administrador ) y los cuales se diferencian mediante el campo discriminator. De esta última podemos destacar que existe una relación de muchos a muchos con la clase Aplications. En otra instancia vemos que poseemos la clase **User** la cual posee una relación de muchos a muchos con la clase **Aplications** . De esta relación surge una nueva clase llamada **userAplication** la cual aparte de poseer las claves foráneas que hacen referencia a las clases también guarda el **deviceToken** campo que usaremos para el funcionamiento de nuestra API con Firebase, y **so** campo que hace referencia al sistema operativo del dispositivo.

  

Una vez obtenido el el diagrama de clases pasamos a trabajar con el **diagrama de Entidad/Relación** que nos dará un diseño con el que entenderemos mejor el diseño de nuestra base de datos.

<img src="https://raw.github.com/alejandroasc96/documentacion2Proyecto/master/imgDoc2Eva/diagramaEntidadRelacion.png" width="500">
Gracias a este diagrama nos damos cuenta del diseño que va a tener nuestra base de datos. Además nos permite ver aspectos tales como; cómo se van a tratar los diferentes campos, así mismo, vemos  se van a diferenciar el tipo de sistema operativo en la entidad userAplication mediante la variante enum, la nueva entidad que se crea de la relación de muchos a muchos entre Admin y Aplication etc.

  
  
  
  

### Creando la base de datos

Una vez documentado la estructura de nuestra base de datos procedemos a crearla. Para ello haremos uso de la herramienta phpMyAdmin donde crearemos nuestra base de datos en MySql.

  

La estructura de nuestro árbol sería tal que así:

<img src="https://raw.github.com/alejandroasc96/documentacion2Proyecto/master/imgDoc2Eva/arbolBaseDatos.png" width="500">

Luego pasaremos a las vistas de la estructuras de nuestras tablas

  

__Vista user__

![](https://lh4.googleusercontent.com/m7FMvE9SQ96uyP35-WTaMXMalUnVFVjbhYEd15LOhJ6lGCKodLUZstPxLE5JbDoo-haYEZKdDyduh3MbAUiIHnJi4h5-rCJe-tDWap4HlJcvIPspIJDjkqcGPz4_fppxy1UqJi6b)

  

__Vista application__

![](https://lh4.googleusercontent.com/Huj2HVjdRjeHhlshCvlpgryI8rtKzxMsVRQBrtbNyLoze0tuOAmWN_jTqx5_h8XYP-jtJK3GiOW2vS1i03a46yyuf5-8uOpfvxkrAhRgqYFvCWDKXD8Q6x3ES0FzT3tfzrPV7hpv)

  

__Vista userAplication__

![](https://lh6.googleusercontent.com/T383V7CwBrsq7-75g9KqlsHXAXctuwANerixA_ythLvFp0eX1Q_sKu044Hu54X4w_fTrZgwT4d7DzydOKYuT3WNakZO5JgkQaRJLZXAvXMe-G0WKY8TZQIMbY9KFWkbdKfR40_Ad)

__Vista Admin__

![](https://lh4.googleusercontent.com/1-KOJg4d6xMnCqNUUxDC4pDR1ZtlY3SnfzK-f9RBY-Hq1sSbEyA8rzKim4rw2y3Dgll8pz_cBj_lsgn5dsdsxGm9p0YwFN0gg-WjCVwb0BjRGJwfnT7k3G4XeZvW-fxrChz_MbEP)

  

__Vista adminAplicaton__

![](https://lh4.googleusercontent.com/gyg2sEvhkOl1d8WA2Q6RpaOqkBylrWfCQks40nAY-jDzwkuzwgo2Gtz2J67qzCeC6CiCwKuGTDQ0ml1NNLV6oLYBJH9ezm-3DKc-DmT2b02QMYojoCPVzuB718xotwOZ20L1l2cb)

  
  
  

__Vista de las relaciones__

![](https://lh6.googleusercontent.com/-dEZEbXnhABrpstDg7sIgRaV0GU1WsSoccpdcXU9zuiXVgY2zCowApMgiVLCp65D-iJTxygM-D0mjb-x9tM4IuIt_VUfNDgL6---7gH2ULI_ZIFewj9vn-oa0bVBAkKKRle0Jbot)



  
### Mockups y Historia de Usuario

#### Requisitos del Sistema
 1. Creación de una notificación
 2. CRUD Empleados (administradores)
 3. CRUD Usuario
 4. CRUD Aplicaciones
 5. Autenticación para los administradores

#### Recorrido del sistema  

Como en todo sistema que se precie, se diseñan rutas para los usuarios. En este apartado del documento se da a conocer el recorrido establecido con ayuda de los mockups que nos dan una idea de la estructura que vamos a llevar a cabo para nuestro cliente web.

  

#### Caso de Administrador root

#### Primer paso : Login

![](https://lh5.googleusercontent.com/MAY1zLX7-Xu-t-ZxRc794osYdfNsQbfo2KfKcHLy2dRdd3MjIhpQUMcHrvoyK4MaSvomuZpfyuUhyWMlhAbq7wCREMXRmmzFpkUQtVmgnb78aDYLZMzxlO3G0mR6t_QIn7HeewsZ)

  

Esta es la vista de login a la que acceden solo los administradores para gestionar ciertas acciones de nuestro sistema por lo tanto tendrán que acreditarse mediante un login con el uso de su e-mail y contraseñas registradas en el sistema.

  
  

#### Segundo paso : Panel Home
**![](https://lh4.googleusercontent.com/TDXH4PuVFMGu_39HVe-m-TPXNb-Sr1eG9zq4M_ucTTGjVzDcAjB8Vbcjz4CzfKsNQKmFB9STbLNbyLJWUBvAQeYol5VJNdj8j-oydEtvwAOWQsJKpLVOT4WTVNm_phj6In3tA9Z-)**

Una vez hecho el login el administrador accede al panel inicial donde podrá elegir las acciones que quiera ejecutar.

#### Panel de Notificación
**![](https://lh3.googleusercontent.com/MVXLzzmoNZ9UhfEpwyt0K-ykyWabTC1XtpPBAiPP-U51YfnUCOSS2n5OeMyxDTj2rCU3GfzYBi4pVsMovE1TEC_xGUbeFy-vbt34HcuCdEE-Wba3KXBVoRfuk1QQeOuYteT8I60I)**
En el caso de querer crear una notificación el administrados al acceder al panel de notificación, se encontrará con un formulario a rellenar y una vez completado podrá efectuar el envío de la notificación.

#### Panel aplicaciones
**![](https://lh5.googleusercontent.com/Neb3FQ9_LMzIGsHhYIkVT6gc_1hR-q2xj-VmRWoKnwjh6454LotpxKqXw_Uc_jBipiB4F8dt4Gfjdhfj3Ub7nNB8QtGzNsx2zy0fpSBVuVCiUVJnMS2pnuXfp07JhIcEz2pBtQQx)**
En el caso de entrar en el apartado de aplicaciones el administrador se encontrará con un panel donde le aparecerán todas las aplicaciones registradas las cuales podrá filtrar según sistema operativo o temática.

#### Panel de Empleados
**![](https://lh5.googleusercontent.com/wwUhwUfeQ-YbJI5CjJQq1EXJtbniFl1rZHRBoSpLu6eFBdd7KOQ8TD0yO6QSiHuSHvyQjgMcKdxiQaUPmc-5xxeFgY5mJdEHdm_60hUpUrEszOrmsRDsT3Qe12LRu0fvxrtAUAGJ)**
En el apartado de empleados el administrador root podrá gestionar todos los empleados que tiene registrados. Así mismo tendrá las opciones de crear nuevos usuarios eliminarlos etc.
#### Panel de Users

**![](https://lh5.googleusercontent.com/w6Rv5VnaPRGS8M_PiG9iWaHafPLSKxd8ehNFxKrUAZ0y37jaQAflXC-QEge3swmfr5klPajjlALZPYywuuw6-6xbyxDlgf69GC54oTYmXSKsjrDI7Vbyefnf1tiRqd6NihYiEoby)**
Luego el administrador puede también un listado de los usuarios que hay dentro de sus aplicaciones y realizar un CRUD manualmente si así lo desea.
## Relaciones dentro de NodeJs usando Sequelize

![](https://lh3.googleusercontent.com/bDtA-fF-LU_8tZb4wlE-HvmX2yZ09hzVbLKUPWgoEy8bl14pTCpmpFyGVynFzJg3aRjcN9V55xxTej7iJUN2aeDDRGZW7HNCqY6Lyze_6iqxwDX7xm79fHgI4DJ2UZ2idO0Vz1HI)

## Descripción del código de la API.


En cuanto al documento index.js :

![](https://lh3.googleusercontent.com/DG2ne3NtGPvEXWdquhA78bk9jIQ0_o5MDhXVmSSQOuBhTdX-iNNNSYi54LbI6-_gzYWjoOMBDPB5oNbdqFBe6vnVN0TpWjXgbQrAYguq4ZdzlXko_sQcoJWrZ8rQYNF00T3hs8UZ)
En este caso utilizamos consign para cargar los archivos necesarios para poder arrancar el servidor con todo lo que necesite.

El primer archivo en cargarse es config.js:

![](https://lh6.googleusercontent.com/ZHyPgxtmeNHVXvQt5Sm_r0gvoyPcank9Yn0-GFMDY1FIuV1rV8S5gy5MxwTpye0iMdNeBvDThJkX9bfYHmkqUqnIe7sErLE9ROoLUdtb9M9b5VtVEPEHUcmeKbEaAIXWrmhOMTic)
En este caso definimos la configuración necesaria para que sequelize pueda conectarse a la base de datos.

En segundo lugar cargamos el archivo db.js:

![](https://lh5.googleusercontent.com/ajUHglti82mbO71MmUgsXD59d41SU9ZEnNT63kH2lrnLKsFK9REu00shpb3nqFkfb0mUbo_f3wF0ZTtmHElmwwYwC3xJ7uSQ0bAW4HA_FfrHF3PzcOdl7t-0B3bXgvc_SBScUjwf)
Aquí es donde realizamos la conección a la base de datos utilizando sequelize. En la línea 8 se se crea una instancia de sequelize con la configuración importada, la propia librería de Sequelize e inicializo un json que contendrá los modelos.

Más adelante en la línea 21 recorro los archivos de todos los modelos y los asocio con sequelize introduciendolos en el json models. Tras cargar todos los modelos ejecuto los métodos que establecerán las asociaciones entre los modelos(línea 28).

Este es un ejemplo de mapeo de la tabla ‘aplications’ con Sequelize.

![](https://lh4.googleusercontent.com/W7dUKC_PwVAwkZfq05JaTR0ezeN_drfK1mlCpGRdBXZRKISJG4O4jyMWLFj9Snpg85PNwnxytUtK-TnxD4cPYKdwmfCYhUfuWX8JT_Aa05_S9VNm5bEk6hT7kxdMRSuqz9L02XUr)

De esta manera en la línea 4 especificamos el nombre de la tabla dentro de la base de datos a la que hará referencia el modelo. Más adelante, defino las columnas de la tabla, especificando sus características como su tipo de dato (líneas 7,11 y 15) o validaciones necesarias (líneas 13 y 18).

Por último están las asociaciones, en esta caso las aplicaciones se relacionarán con administradores y los usuarios de las aplicaciones a través de sus tablas intermedias ya que se trata de una relación de muchos a muchos usando la clave extranjera ‘aplicationID’.

El siguiente archivo que se va a cargar serán los middlewere:

![](https://lh5.googleusercontent.com/lIu9obwJTOwZCia3CSxDL8ccghdhFiCCV2UaMQpNn0nGU41CLCCTW5qd1JQdS8B65X7MXexxYzwvNHorrojYDaLHZCddtFfVwuYWgOwSuQS0YvWudDnxcN7ZzmHM1Y_Ix0qtn0rk)

Luego vienen las rutas, como ejemplo usaremos una ruta de las aplicaciones.

![](https://lh6.googleusercontent.com/SwJuxPD7JlC6NYzsU6sdM0YuTbdRSCoU6Vkec6lZzkso6K9wRlrwanzlKTNSS-Zd3TeJAJIvR9sWyD5kQNB68mFBLqegywLonXBchtFBoTDtTNDijn_yQz07kL97_8K02nlbS0j2)

En este caso importo en la variable Apps el modelo de aplicaciones, en la línea 5 defino la ruta con la que se hará la petición al servidor y más adelante ejecuto el método del modelo de sequelize para realizar la búsqueda dentro de la base de datos.

Este es un ejemplo donde, además de mostrar las aplicaciones de la base de datos, se muestran los usuarios de esa aplicación:

![](https://lh6.googleusercontent.com/QgWaIaSY55bG8Ve9MZxB6AEARjVUK4jE-m_f-Co7JCyzbmjjdDBrnNR3S0nD0MP1tQi2WTDevdd6uNKx9KAvXQotJN7-zyO0Q6E3M3G9O1HkLhNwHuPs1W5wTS7hGBANAs_ISHOl)
En la línea 17 se incluye el modelo de usuarios para que se muestren también.

Por último se arranca el servidor.
![](https://lh4.googleusercontent.com/nAucfQ_kZMxlJ89qRxdAupSJquRcgoBlXaWXW93WOcUtIKmkZqw4sQveLSJ1O1HivFCOcv6m1D17qO7OPU8nxhIa0jCE4RKIAyacUJs2_2RnMTyBCmIpd6fMq2EfT0GzcdDH6-50)

## Describiendo la implementación de la API REST.
En el siguiente enlace se muestran las instrucciones de todas las rutas de todas las tablas: https://documenter.getpostman.com/view/6744581/S11GTLv6

Como ejemplo utilizare las rutas del modelo usuarios:

![](https://lh6.googleusercontent.com/xihAkOY1LLD4Z_09wfEqFBfAh-i87vKhPWrfKalIW9Gj42xfBDM7PAzOmvJHMfuxSQkP8b4ObC4Kjgc8SljQdH7proaSwwVQQPNJs5fPx4JiKjkIttrUcm4ZRI82Qmit28rT0KXV)
Esta ruta devolverá todos los usuarios dentro de la base de datos.

![](https://lh6.googleusercontent.com/-P05FBeW9v_iYlSRv-kOFqBE_tMg6w8IWRH8YLfJO3YKNLMM-aUrv4k0DWw_vAmQTi1wJWwppMmxacD-SsedOAwMlPDMVwjqnNv2RQrZfDJwJKStdfLwIDeOgyXzRs3gB-VSAfqu)
Esta ruta devuelve un solo usuario usando su id, el pasado por parametro.

![](https://lh6.googleusercontent.com/EYGP0kzB7zHK3Bm6S0dg73e4ihsV4rDWo5aEVnYHiPBAj9sT6wkE9wsgyP_fPJY28Sad77wicWVM-4M0pqjCsr-JhMHohs_9mCmufakVdMM042lL5iPvgSL-r887Or4Gk96mVnA7)
Este es el post que debe definir un json con los parámetros necesarios y pasarlos usando un body.

![](https://lh4.googleusercontent.com/xoALpvr0A05Q2aa5wCA1dAUTXqjShVe1IMjKC223Jn4GPqQ4Dsm4wImfKAcHHnTwm2HIwCNK8rhpSfXobIx-BNNPv5okMtE5g-09Tqgu1_wBt6lL3Yfcy9uqTlSEE5gTjIZs_LeJ)

Este es el put, similar al post anteriormente visto, solo que en este caso hay ue indicarle la id del usuario que se quiere actualizar por parámetro en la ruta.

![](https://lh6.googleusercontent.com/HGFS7kASZ4A4CZBOXogkVSx7zn6IS1Zw6_2jNPNffgA3Ct9GBOuljHHTyhuf-QwxDPz9IGLTmsoaDO4xz_eOsJ7HKLvZd6iXssnUi5yxJCbWkb7YXXJ98u7kz1FUqaehT2hFOCWr)
Por último esta el delete, al que se le debe especificar la id del usuario que se deea borrar pasandola por parametro.

# Manual de Usuario
## Descripción
La finalidad de este apartado es definir de cara al usuario como trabajar con la aplicación web.
## Paso 1 : Login
Dado que solo podrán acceder a la página web los administradores que estén dados de alta en nuestro sistema el usuario deberá hacer el login adjuntando su e-mail y contraseña dados de alta.
**![](https://lh5.googleusercontent.com/fjjD4Tyd1bmwr-DUE292dleSC1ajR1rE5yANEDWLfI27hzyJQh0oMzqOuUcM1XQgkFdGzMYym1hzodNOY1vLNmHx-wRMIxnc-d_fkqh5nAVLKUX588Ji3EFEsZx_howgysB5ioaB)**
Una vez introducido los datos el usuario deberá presionar sobre el botón de Login y será el propio sistema el encargado en primera estancia que los datos se ajustan a los parámetros establecidos y luego a realizar la autentificación.
## Paso 2 : Panel Home
Una vez hecho el login el usuario se encontrará con un panel donde tiene disponible diferente tipos de acciones a realizar.
**![](https://lh5.googleusercontent.com/jG7XS5HL6e3x63VTtIIBMizW4Q-8WQfhlDu97hpSwSuUtxlbpkfgZWhQyoHGIoyR7hoAyzAqwj6bxP_UJ9wnT2GzSNWrkwSlPofgL7OWKRqEzURVzfuki9cx5QSr3LlzfjFC7xVw)**
## Paso 3 : Creando Notificación
Para crear una notificación el usuario deberá seleccionar dentro de panel azul __*View Details*__ , dicho botón le llevará al formulario de la notificación el cuál deberá rellenar para realizar el envío de la notificación.
**![](https://lh4.googleusercontent.com/AlvxHhONYA0T5rBGClqEorhDwuRAGYN_1i5pKPr4VpcK_tvHv59vUxsjCUSRNlxKwVjQm8FemZKEt2gIryTFH-4_wqYpi1tIaKQ7ozloFI8irUfeOk3Hm4LtWML5mY1ftWEB0ECH)**
## Paso 4 : Accediendo al panel Usuarios
Para acceder al panel de  usuarios el administrador  deberá seleccionar dentro de panel Amarillo __*View Details*__ , dicho botón le permitirá  ver el listado de usuarios.

**![](https://lh4.googleusercontent.com/IBoJOW1rB-quuu8AcQ1ILPWHv21bS_Q52cYP6fMeNZIppvZUsGBN6v0M3LVcI6F73SHpXSphRY6Xi8FEmQdVTj4Phs-prWvkGijPpva30kQ185WH-Ka_joU3ndOWmfN3eUkvE8Gg)**
## Paso 5 : Administrando Clients
Para acceder al panel de  clients el administrador  deberá seleccionar dentro de panel Verde __*View Details*__ , dicho botón le permitirá  ver el Panel de los clientes donde aparece el listado de los clientes registrado y las diferentes opciones para administrarlos (realizar un crud).
**![](https://lh4.googleusercontent.com/OqnhOh-Bz-n83OVLJ-zwwWOD2YEqTCXVHTnjHc6HgGF0DmrYB_UDzSoc4QhPwhCIy7nCbyQS3BmHr20jr___Tx2NqeuZ7iTuSYVhvoqWQU-6seyaiSS72IkTPYQoxIawBbbkFVWA)**
## Paso 6 : Administrando Aplicaciones
Para acceder al panel de  aplications el administrador  deberá seleccionar dentro de panel Rojo __*View Details*__ , dicho botón le permitirá  ver el Panel de las aplicaciones donde aparece el listado de las aplicaciones registradas y las diferentes opciones para administrarlas (realizar un crud).
**![](https://lh6.googleusercontent.com/qcFKnFRNqVZgAaYbP_MPt0fNeVKM-oMUW_Qkuve92BHj-_cemsLYlqI_mt5sXaNWuMcxm7ndbHs9AEmyG7TepZIgizsPvqrf-S9qButmg5_T8rw19Z5RQWp6lbnW6LtyxcnGr5i1)**
## Paso 7 : Cerrar sesión
Para salir de la sesión desde cualquier vista desde el navegador al pulsar sobre el icono de usuario nos dará la opción de Logout, al pulsar dicha opción de nos abrirá una ventana modal que nos preguntará si realmente queremos salir, si pulsamos salir; cerraremos dicha sesión.
**![](https://lh6.googleusercontent.com/Ps58SQY_V2qbk_Gz2_guCIe7GxsuHUeheJ3-SOmP7pBxFbaTMVtKaiPQOX_ojOUfJCygnND-qhub4SF_ZDAgGv-lksipkw1iXa3rkVtS9hio8LsR7BdUvB3H8-REi3cd_Zx-Juoc)**
**![](https://lh3.googleusercontent.com/S4pY1urGfLu-QRFt-MCLRYPYb9yUMx9_Fjg4XD1M18X4F1VufHlkRO2929ydtOpW8MhTGf_KFZa60QzHnyy3av8L8kxytIznTcref1VWLcBwasy-2KkXmOekLJ0JZKbgh0AD8jmb)**

# Describiendo el código de la  App Web.

## FrontEnd
### Comparativa de Aplicaciones Web vs  Aplicaciones Nativas
#### *Aplicaciones Web*
Las  **aplicaciones web** son aplicaciones a las que  **se accede siempre desde un navegador**, ya sea desde un dispositivo móvil o desde un ordenador. Sólo cambia la visualización de la aplicación en función del dispositivo.

Estas aplicaciones están desarrolladas con tecnología web. Y aunque hay combinaciones muy distintas, en este caso hemos realizado el desarrollo con  **HTML, CSS y JavaScript**  además de un lenguaje de servidor que nos proporcionará acceso a base de datos, seguridad,… entre otras muchas cosas.

#### *Aplicaciones Nativas*
Las aplicaciones nativas son las aplicaciones móviles que se desarrollan **específicamente para cada sistema operativo**. Este es el desarrollo tradicional de aplicaciones móviles. En el cual es necesario conocer el lenguaje y la mecánica de desarrollo para cada uno de los sistemas operativos.

Comúnmente se desarrolla para Android y para iOs.
### *Conclusión*
#### Web
Ventajas: 
 - Sólo un desarrollo
 - No consumen espacio en el dispositivo
 - Mantenimiento Bajo
 - Minimiza el riesgo
 - Base de datos en el mismo servidor
 Desventajas:
 
 - No tiene acceso directo desde el dispositivo
 - Requieren siempre de internet
 - Consumen más datos móviles
 - No hay notificaciones PUSH
 
#### Nativo
 Ventajas:
 - Posee acceso dorecto desde el dispositivo
 - Optimizan el rendimiento del móvil
 - Posee Notificaciones PUSH
 - Accesible Offline*
 Desventajas:
 - Desarrollos independientes para cada plataforma (Gran Coste Económico)
 - Mantenimiento Alto
 - Consumen espacio en el dispositivo
 - Problemas con la versión de los sistemas operativos

## BackEnd
### Node JS vs Java/ Spring

  

#### Node Js

  

Node.js es un entorno en tiempo de ejecución múltiplataforma, de código abierto, para la capa del servidor (pero no limitándose a ello). Fue creado con el enfoque de ser útil en la creación de programas de red altamente escalables, como por ejemplo, servidores web.![](https://lh5.googleusercontent.com/JxksZTXcs_7ufjlWHF7faYYDZLoZHNUVbsUKOssotgTv99-jjb80qutU24-Eeo9vYAxBbzBgnfrGnHAlSVMdQL08Mgj40R1YES4hdsRXAwlqAulNbxWn10-qpcpn9r6zh2r3N7go)

  
  
  
  
  

El lenguaje de este entorno es javaScript que está presente en algunos elementos de prácticamente todos los sitios web-, por lo que el proceso de aprendizaje será veloz. Resulta especialmente útil para webs dinámicas que soportan grandes cantidades de tráfico en tiempo real, convirtiéndose en el lenguaje del futuro para las apps que se vienen.

  

### Java / Spring

Spring es un framework para el desarrollo de aplicaciones y contenedor de inversión de control, de código abierto para la plataforma Java. el lenguaje que emplea no es otro que Java por lo que le confiere gran solidez dada la cantidad de años que lleva en el rubro lo dotan de controladores, depuradores y otras herramientas que integran el lenguaje para cubrir todas las patas de la tarea que desempeña un programador. Su antigüedad es sinónimo de solidez aunque la complejización de sus recursos repercute sobre sus funciones: es cada vez más difícil aprender a implementarlo.

  

### Conclusión

Los dos son viables en las áreas de ingeniería, aunque cada uno posee sus particularidades que lo hacen más propicio para una u otra situación. Java es más apropiado si estás construyendo un sistema en tiempo real porque actúa más rápido, pero ten en cuenta que su abanico de posibilidades implica dificultades a la hora de interiorizarse con su funcionamiento. Es estático – por tanto menos factible en webs dinámicas- y la complejidad de su sintaxis requiere horas de estudio.

  

Por otra parte, Node.js resuelve problemas de sincronización mucho más rápido porque trabaja sin hilos, es decir que no se vale de subprocesos para ejecutar una tarea sino que directamente apela a una única línea de trabajo: prioriza las tareas y las pone en cola. Perfecto para principiantes, sitios web dinámicos de empresas tecnológicas o de comunicación o aquellas que necesiten soportar miles de usuarios navegando al mismo tiempo.

# Línea de Tiempo
**![](https://lh5.googleusercontent.com/9nieicoxkfT3dO0iFLTDNrZ5rCyPZlTiFFeJ1i3l_HlfjTDVCIyory4Hy1bW6uVnBnGMkLltrmWRde696tvECDe3fFdKUppTEKP6MC2Cn1g2RV0E6njkQYxlSNc7sSF8ij5PUSu5)**
**![](https://lh5.googleusercontent.com/LzZcd3M7lWG8Mh2oBe9ODO_LKdWcnikxXU2T3syZrCt4_mWSmRm76hJsMxkT-mPpFZZkhiSB0hAff27HhED8ysV54VOi9qjWKxrzkRgq1R1ahPFsFwvc4chsv1ZYdsoqeLA9jUOT)**
**![](https://lh5.googleusercontent.com/F5qgN7kjSghN5RZD78Ailurj-gaF7zM4RZTyVo6jNZpq3_5zBJySfo3psC8xMFWlr3UHm1Qsj8EoYqWJEeVLsH_kgeOCqmjD6m13CPLTtqwVeCRl9nWwCyDmzdl3taH5m8TDq6Bj)**
**![](https://lh6.googleusercontent.com/_wptWB128UmP0qjhSqz5MRrgVYSGtHdCJsScYjmngzkIMO2D-RKJnLOB7zjNg_hShucuomY16zLfFC-YhQdLZ-DPmXzQsgl1HoBm-mNMLx_NnnK6j21SrKCAEN-8lu--Yv-A_F9R)**