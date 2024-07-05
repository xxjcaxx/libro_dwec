# Libro DWEC

📃 Versión web: https://xxjcaxx.github.io/libro_dwec/intro.html 

Este libro está hecho con Jupyter Books. Se puede obtener una copia en PDF, acceso a una versión Web y, en caso de tener Jupyter con Deno, se puede ejecutar el código de algunos ejemplos.

Este libro pretende ser la base de un curso de Desarrollo Web en Entorno Cliente del ciclo superior DAW. Puesto que cada profesor puede elegir la metodología y gran parte de los contenidos, es necesario advertir que este libro puede no ser un buen candidato a sustituir a los libros de las editoriales, mucho más genéricos. No obstante, se intenta dar un enfoque de programación moderna del frontend. No nos detendremos tampoco en la adecuación de estos contenidos a los currículos oficiales.

Todo el libro está enfocado al desarrollo de dos proyectos individuales o grupales. El primer proyecto, que puede ser realizado a lo largo del primer trimestre y el segundo durante el segundo trimestre. El primer proyecto es en Javascript Vanilla y el segundo en Angular. Durante la primera parte iremos introduciendo conceptos y tecnologías necesarios para entender la potencia de un framework como React, Vue o, en este caso, Angular.

La forma más sencilla de editar este libro es con Jupyter Notebook:

1. Instala `Jupyter` y luego `Deno` como intérprete: 

https://docs.deno.com/runtime/manual/tools/jupyter :

    curl -fsSL https://deno.land/install.sh | sh
    deno jupyter --unstable
    deno jupyter --install
    
Con todo esto instalado, en Visual Studio también se puede instalar la extensión de Jupyter y seleccionar Deno como Kernel. 

2. Clona este repositorio y edita con `Jupyter Notebook` o Visual Studio, por ejemplo, los .ipynb

3. Si lo que se quiere es transformarlo en web, se instala:

    sudo pip install -U jupyter-book

Y luego se puede construir con:
    jupyter-book build libroDwec/

Pero hay una versión ya construida en este repositorio que se actualiza casi siempre que se cambia algo en el libro.

4. Para publicar este libro he usado `Github Pages`. La manera de hacerlo funcionar es hacer un `Github Action` que podemos consultar en la rama `master` de este repositorio. El manual del action está aqui: https://github.com/marketplace/actions/github-pages-overwriter . A continuación he tenido que poner un archivo `.nojekyll` para que Github no transforme nada de la web y acepte subdirectorios que comienzan por '_'. De esta manera, cada vez que subo el libro, se despliega la versión HTML estática a: https://xxjcaxx.github.io/libro_dwec/intro.html 