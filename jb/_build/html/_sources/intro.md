# Libro DWEC

Dentro del ciclo de DAW, el segundo curso tiene 3 módulos íntimamente relacionados y que, todos juntos, sirven para hacer una web completamente. Tenemos un módulo para programar el servidor (backend): `DWES`, un para el cliente (frontend): `DWEC` y uno para la interfaz de usuario: `DIW`. El módulo DWEC, por tanto, debe suponer que hay un servidor funcionando correctamente, así como el módulo de DWES supone que alguien ará el frontend. Además, en DWEC no nos vamos a preocupar demasiado de la parte estética, aunque es inevitable construir HTML y reaccionar a las acciones del usuario. Por tanto, este módulo se centra en cómo recoger datos del servidor, mostrarlos y hacer algo con ellos. Puesto que este módulo es casi todo `Javascript`, la manera de tratarlo más intensamente y en todos los aspectos del frontend es hacer una `SPA` (ya veremos qué es eso). Es importante recalcar que vamos a ver un subconjunto muy pequeño de todas las maneras distintas que hay para enfocar un proyecto de frontend y que no tiene porqué ser el mejor en todos los casos. El alumnado de estos ciclos debe añadir a su rutina personal alguna manera de estar al dia de las novedades del desarrollo web. Por ejemplo, seguir a la MDN en redes, /r/javascript en Reddit, Canales de Youtube, Hacker News, la W3C...

Podemos separar el curso en dos grandes bloques con los siguientes temas:

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
* Frameworks
  * Typescript
  * Angular
  * Componentes, rutas, servicios...
  * Formularios

Puesto que todo está mejor documentado en las webs oficiales de cada tecnología, en MDN o W3CSchool y demás, no es necesario ser exhaustivo en cada sección. Nos detendremos en las partes más interesantes y representativas del frontend con ejemplos prácticos y intentando siempre aplicar las mejores prácticas.

> Actualmente hay poca gente que programe directamente en Javascript "Vanilla". En un módulo para formación profesional nos podemos preguntar si no sería mejor enseñar directamente un framework. I también si no sería mejor enseñar el framework "de moda". Los motivos para el hecho de explicar los fundamentos en Javascript sin frameworks o muchas bibliotecas y de seguir con Angular han sido reflexionados con otros profesores y alumnos. Por un lado está el hecho de que hay que conocer la base y no depender de una librería en concreto. Pero es que el uso de frameworks, aún siendo masivo, también tiene su controversia. Conocer los fundamentos y las buenas prácticas es mejor que saber programar rápidamente algo comercial. En cuanto al framework, Angular es usado masivamente por gente que no publicita su trabajo en redes sociales. La mayoría de empresas de la zona lo utilizan. Además, es un framework totalmente actualizado a las metodologías modernas, que fuerza a tener una disciplina y conocer arquitecturas, patrones de diseño y buenas prácticas.
