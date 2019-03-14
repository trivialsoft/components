# Referencia de Trivial Components 1.0

> Este repositorio prentende ser una guia y referencia rápida para el uso del framework TC 1.0.

## Estructura de un componente

> Se ejemplifica con el siguiente ejemplo:

```plain

Usuario(carpeta)/Usuario.php             -- Modelo          
                /Usuario.html            -- Plantilla
                /Usuario.js              -- Script Frontend 
                /UsuarioComponent.php    -- Script Backend 
```

## Modelo Persistente
> Un modelo Persistente, es la clase que se usa para representar objetos persistidos en la base de datos, tienen 
la estructura que se ejemplifica a continuación:

```php 
<?php
/**
*  file location: components/Usuario/Usuario.php 
*/ 
namespace Usuario;
use \core\SSD\Model as Model;
class Usuario extends Model implements \JsonSerializable {
	public $Usuario;
	public $Nombre;
	function __construct()
	{
		parent::__construct();
	}
	
function subinstances()
	{    
		return array("Ciudad"=>"Ciudad");
	}	

public function jsonSerialize() 
	{
	return [  
		'Usuario' => $this->Usuario,
		'Nombre' => $this->Nombre
		];
		}		
	}
?>
```

## Modelo No Persistentes
> Un modelo No Persistente es una clase que se usan para poblar información de componente y que no guarda relacion directa con una entidad , tienen 
la estructura que se ejemplifica a continuación:

```php
<?php
/**
*  file location: components/Home/Home.php 
*/ 
namespace Home;
class Home {
function __construct()
	{	
	}

function Nombre()
	{
		return "TrivialSoft";
	}	
function select()
	{
		return array(0=>$this);
	}	
}
?>

```

## Plantilla

> Se refiere al texto html que sepresenta la representación grafica del componente(server-side), se ejemplifica a continuación:

```html
<!--file:components/Home/Home.html-->
<div class="container">
     <div class="row">
	 <div class="col">
	    <ts:Ciudad m:(Ciudad) f:({}) t:()></ts:Ciudad>
	 </div>
	 </div>
</div>

```

```html
<!--file: components/Ciudad/Ciudad.html -->
<div class="alert alert-info">
<li>{{Nombre[]}}, {{Estado.Nombre[]}}</li>
</div>
```



## API Trivial

> a continuacion se explica como interactuar con el backend

```plain
Nota: todas los request deben llevar en el header un token oauth
Authorization Bearer 1234abc

Si se necesita recuperar una coleccion de elementos 
GET: /api/v4/ciudades
Si se necesita recuperar una coleccion de elementos ordenada por una propiedad
GET: /api/v4/ciudades/Nombre_desc
Si se necesita recuperar una coleccion de elementos filtrada por una propiedad
GET: /api/v4/ciudades/{"Estado":1}
Si se necesita recuperar una coleccion de elementos con sus subinstacias hasta un tercer nivel
GET: /api/v4/ciudades/3
Si se necesita modificar una o mas instancias 
POST: /api/v4/ciudades
headers:
Content-Type:application/json

body(raw+JSON(application/json)):
[
{"modelname":"Ciudad",
"Ciudad":1
"Nombre":"Monterrey"
},
{"modelname":"Ciudad",
"Ciudad":2
"Nombre":"Tuxpan"
}
]

Si se necesita modificar una o mas instancias y ademas aplicar una accion
POST: /api/v4/preguntas/like

Nota:similar al ejemplo de modificacion.

```
* Configuración mode_rewrite
* Archivo boot.php
* Estructura de un proyecto
* Componentes core