# Desarrollo de Software Seguro - Práctico 2

A continuación, se muestran 8 vulnerabilidades presentes en el software proporcionado de Altoro. Para cada vulnerabilidad, se muestra una prueba de concepto de cómo explotarla y una solución para mitigarla.

## Vulnerabilidad 1 – Cross Site Scripting

Existe un cross site scripting (XSS) en el parámetro query de la url search.jsp, lo que permite manipular los datos que se introducen desde la petición web para inyectar scripts maliciosos.

![image1](images/image1.png)

Esto se debe a que los datos de entrada en el parámetro de entrada no son neutralizados antes de ser utilizados. Para mitigar este problema, se puede usar el método ServletUtil.sanitizeHtmlWithRegex() sobre los datos de entrada antes de utilizarlos para realizar operaciones de búsqueda.

![image2](images/image2.png)

![image3](images/image3.png)

Luego de realizar los ajustes en el código, no se ejecuta el script ingresado desde la url.

![image4](images/image4.png)



## Vulnerabilidad 2  – SQL Injection
Se puede realizar una inyección SQL en la funcionalidad de login, lo que permite acceder al sistema sin conocer la contraseña.

Se puede observar que independientemente de la contraseña que se ingrese se logra acceder al sistema:

![admin login](images/adminlogin.png)

![admin2](images/admin2.png)

![Ingreso exitoso](images/Ingresoexitoso.png)

Este código es vulnerable a SQL Injection porque concatena directamente las entradas del usuario (user y password) en la consulta SQL sin ninguna sanitización. 
Al no estar sanitizadas, cuando se le ingresa: admin' -- en el campo de usuario y cualquier valor en el campo de contraseña, pasa la validación porque ambos campos contienen algún valor y la consulta SQL que se genera se convierte en:

**SELECT COUNT(*) FROM PEOPLE WHERE USER_ID = 'admin'** --'AND PASSWORD = '...'

Los guiones -- que se encuentran luego del 'admin', comentan el resto de la consulta, evadiendo el control de la password y permitiendo el acceso.

Para mitigar esta vulnerabilidad, se debes utilizar sentencias preparadas (Prepared Statements), que aseguran que las entradas del usuario no se interpreten como parte del código SQL.

![codigo arreglado](images/codigoarreglado.png)

![no ingresa debido al control](images/noingresadebidoalcontrol.png)

Se puede observar que luego del ajuste, cuando se intenta ingresar con el uso de la inyeccion, se visualiza un error, es decir, se controla exitosamente los datos ingresados.



## Vulnerabilidad 3 – Improper Input Validation 

Se encontro que existe una vulnerabilidad de Improper Input Validation, al visualizar las historias.
Se ingreso como el usuario "jsmith", el cual tenia 3 opciones para seleccionar: 800003, 800002 o 4539082039396288, para visualizar la historia.

![presionarGo](images/presionarGo.png)

Se encontro que luego de ingresar, en la url se veia el numero del mismo, y cambiandolo se lograba acceder a la historia de otro usuario, lo cual no deberia tener permitido visualizar.

![entrarAMiHistoria](images/entrarAMiHistoria.png)


![entreAOtraHistoria](images/entreAOtraHistoria.png)


## Vulnerabilidad 4  – OS Command Injection

Se puede realizar una inyección de comando en el parámetro content de la página index.jsp.
![inyeccioncomando](images/inyeccioncomando.png)

## Vulnerabilidad 5

## Vulnerabilidad 6 – Use of Hard-coded Credentials 

En la interfaz de administración (/AltoroJ/admin/login.jsp) se utiliza una clave codificada directamente en el código fuente.
Esto implica una vulnerabilidad porque un atacante puede revisar el codigo fuente por ejemplo a traves de las herramientas de desarrollo (f12).

![contrasenaVista](images/contrasenaVista.png)

Para mitigar dicho comportamiento:

Se retiro la misma de ese archivo y se la guardo en el archivo app.properties.
![app.properties](images/app.properties.png)

Luego desde el login.jsp, se podria acceder a la contraseña cargando el archivo de app.properties.

![contrasena](images/contrasenaP.png)




## Vulnerabilidad 7

## Vulnerabilidad 8
