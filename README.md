# Libro DWEC

Este libro está hecho con Jupyter Books. Se puede obtener una copia en PDF, acceso a una versión Web y, en caso de tener Jupyter con Deno, se puede ejecutar el código de los ejemplos. 

Este libro pretende ser la base de un curso de Desarrollo Web en Entorno Cliente del ciclo superior DAW. Puesto que cada profesor puede elegir la metodología y gran parte de los contenidos, es necesario advertir que este libro puede no ser un buen candidato a sustituir a los libros de las editoriales, mucho más genéricos. No obstante, se intenta dar un enfoque de programación moderna del frontend. No nos detendremos tampoco en la adecuación de estos contenidos a los currículos oficiales.

Todo el libro está enfocado al desarrollo de dos proyectos individuales o grupales. El primer proyecto, que puede ser realizado a lo largo del primer trimestre y el segundo durante el segundo trimestre. El primer proyecto es en Javascript Vanilla y el segundo en Angular. Durante la primera parte iremos introduciendo conceptos y tecnologías necesarios para entender la potencia de un framework como React, Vue o, en este caso, Angular. 

De esta manera, podemos separar el curso en dos grandes bloques con los siguientes temas:
* Javascript "Vanilla":
  * Programación Javascript para el frontend
  * Testing
  * Comunicación con el servidor
    * Promesas
    * Fetch
  * Programación moderna en Javascript
    * Vite
    * CI/CD
    * Despliegue
    * Observables y programación reactiva
    * Programación funcional
* Angular    


La forma más sencilla de editar este libro es con Jupyter Notebook. Instala Jupyter y luego Deno como intérprete: 

https://docs.deno.com/runtime/manual/tools/jupyter :

    curl -fsSL https://deno.land/install.sh | sh
    deno jupyter --unstable
    deno jupyter --install
    
Con todo esto instalado, en Visual Studio también se puede instalar la extensión de Jupyter y seleccionar Deno como Kernel. 

Si lo que se quiere es transformarlo en web, se instala:

    sudo pip install -U jupyter-book

Y luego se puede construir con:
    jupyter-book build libroDwec/

Pero hay una versión ya construida en este repositorio que se actualiza casi siempre que se cambia algo en el libro. 