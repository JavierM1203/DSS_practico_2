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



## Vulnerabilidad 2

## Vulnerabilidad 3

## Vulnerabilidad 4

## Vulnerabilidad 5

## Vulnerabilidad 6

## Vulnerabilidad 7

## Vulnerabilidad 8
