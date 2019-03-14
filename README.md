# Referencia de Trivial Components 1.0

> Este repositorio prentende ser una guia y referencia rápida para el uso del framework TC 1.0.

* Modelos Persistentes
> Los modelos Persistentes, son la clases que se usan para representar objetos persistido en la base de datos, tienen 
la estructura que se ejemplifica a continuación:

```php 
/**
*  file location: components/Usuario/Usuario.php 
*/ 
<?php
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
* Modelos No Persistentes
> Estos modelos son la clases que se usan para poblar información de componente y que no guarda relacion directa con una entidad , tienen 
la estructura que se ejemplifica a continuación:

```php
<?php
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


* Archivo boot.php
* API
* Recuperar instancias de objetos
* Modificar instancias de objetos
* Ejecurar acciones
* Estructura de un proyecto
* Componentes
* Sintaxis de Plantillas
