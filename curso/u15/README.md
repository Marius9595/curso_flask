	# Plantillas con jinja2

[Jinja2](http://jinja.pocoo.org) es un motor de plantilla desarrollado en Python. Flask utiliza el sistema de plantillas de jinja2 para generar documentos HTML válidos de una manera muy sencilla y eficiente.

Por dependencias al instalar Flask instalamos jinja2. en esta unidad vamos a estudiar los elementos principales de jinja2, para más información accede la [documentación](http://jinja.pocoo.org/docs).

## Una plantilla simple

Veamos un ejemplo para entender como funcion jinja2:

	from jinja2 import Template

	temp1="Hola {{nombre}}"
	print(Template(temp1).render(nombre="Pepe"))

La salida es `Hola Pepe`. La plantilla se compone de una variable `{{nombre}}` que es sustituida por el valor de la variable `ǹombre` al renderizar o generar la plantilla.

## Elementos de una plantilla

Una plantilla puede esta formada por texto, y algunos de los siguientes elementos:

* Variables, se indican con {{ ... }}
* Instrucciones, se indican com {% ... %}
* Comentarios, se indican con {# ... #}

## Variables en las plantillas

Las varibles en la plantillas se sustituyen por los valores que se pasan a la plantilla al renderizarlas. Si enviamos una lista o un diccionario puedo acceder los valores de dos maneras:

	{{ foo.bar }}
	{{ foo['bar'] }}

Veamos algunos ejemplos:

	temp2='<a href="{{ url }}"> {{ enlace }}</a>'
	print(Template(temp2).render(url="http://www.flask.com",enlace="Flask"))	

	temp3='<a href="{{ datos[0] }}"> {{ datos[1] }}</a>'
	print(Template(temp3).render(datos=["http://www.flask.com","Flask"]))	

	temp4='<a href="{{ datos.url }}"> {{ datos.enlace }}</a>'
	print(Template(temp4).render(datos={"url":"http://www.flask.com","enlace":"Flask"}))

El resultado de las tres plantillas es:

	<a href="http://www.flask.com"> Flask</a>

## Filtros de variables

Un filtro me permite modificar una variable. Son ditintas funciones que me modifican o calculan valores a partir de las variables, se indican separadas de las variables por `|` y si tienen parámetros se indican entre parántesis. Veamos algunos ejemplos:

	temp5='Hola {{nombre|striptags|title}}'
	print(Template(temp5).render(nombre="   pepe  "))	

	temp6="los datos son {{ lista|join(', ') }}"
	print(Template(temp6).render(lista=["amarillo","verde","rojo"]))	

	temp6="El ultimo elemento tiene {{ lista|last|length}} caracteres"
	print(Template(temp6).render(lista=["amarillo","verde","rojo"]))

Para ver todos los filtros aceede a la [lista de filtros](http://jinja.pocoo.org/docs/2.9/templates/#builtin-filters) en la documentación.
