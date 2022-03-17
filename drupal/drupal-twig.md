# Twig
Twig es un motor de plantillas para php
# Templates en módulo personalizado
Para crear una plantilla de twig debes:
## Estructura
Las plantillas que se cren en un módulo personalizado deben entontrarse en la siguiente carpeta
```
|--- modules/
|    |--- custom/
|        |--- hello/
|             |--- templates/                  
``` 
## Creación de archivo
Por norma los nombres de la plantilla empiezan con el nombre del modulo y separa las demás palabras que lo conforman con (-) con la extensión .html.twig por ejemplo 
hello-base.html.twig
```
|--- templates/
|    |--- hello-base.html.twig
``` 
## Contendio del archivo
La estrucutura de la plantilla depende de su función, para ello revisar la documentación de [Twig](https://twig.symfony.com/doc/), pero un ejempo puede ser este
```html
{% for key,value in data %}
  <strong>{{ key }}:</strong> {{ value }}<br>
{% endfor%}
```
## hook_theme
Para que drupal pueda utilizar la plantilla, esta se debe agregar al hook_theme del módulo en el archivo .module de nuestro módulo personalizado.
Este se encuentra en la raiz del módulo, si no esta, se debe crear
```
|--- modules/custom/hello/
|    |--- hello.module
```
El tema se agrega en la función del hook_theme, en este se definene las varibles que usara el tema, para identificar la plantilla que se usara, en el array debe encontrarse un elemento con el mismo nombre del archivo, la unica diferencia es que en vez de tener - este va a tener _ por ejemplo: 
LLamamos a nuestro template hello-base.html.twig, el nombre de este seria hello-base, y en el hook se llamaria hello_base
```php
<?php
/**
 * Implements hook_theme().
 */
function hello_theme() {
  return [
    'hello_base' => [
      'variables' => [
        'data' => [],
      ],
    ],
  ];
}
```