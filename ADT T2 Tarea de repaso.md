
# Refactorización y nuevas clases

Reorganizar el código de la clase Estudiante.

Utilizar `ArrayList<Estudiante>` en lugar de `Estudiante[]`. A la hora de realizar la lectura, disfrutaremos de varias ventajas: flexibilidad en el tamaño, métodos útiles como `add()`, `remove()`, `size()`, `isEmpty()`, y otros que nos simplificarán la manipulación de la colección. Más allá del uso que nosotros le demos en nuestros gestores de archivos, la colección será más útil en este formato para futuras operaciones que queramos hacer con la misma.

```java
public ArrayList<Estudiante> cargarLista(List<Estudiante> listaEstudiantes, String nombreArchivo)
public void guardarLista(List<Estudiante> listaEstudiantes, String nombreArchivo)
```

## Clases
En la organización propuesta, aparecerán las siguientes clases:
- Main
- Estudiante
- GestorFicherosDAT
- GestorFicherosCSV
- GestorFicherosXML
### Estudiante
```java
// Constructor con parámetros
public Estudiante (int id, String nombre, double calificacion, boolean beca)

// Constructor vacío
public Estudiante ()

// toString
public String toString()

//Getters y Setters
...
```
### GestorFicherosXXX
Declararemos las tres clases como abstractas, ya que no precisamos crear objetos para disfrutar de su funcionalidad. 

Las tres clases implementarán dos métodos con las siguientes cabeceras:
```java
public ArrayList<Estudiante> cargarLista(String fileName)
public void guardarLista(ArrayList<Estudiante> listaEmpleados)
```

### GestorFicherosDAT
Además de los dos métodos implementados por todas las clases GestorDeficherosXXX:
```java
public ArrayList<Estudiante> cargarLista(String fileName)
public void guardarLista(ArrayList<Estudiante> listaEmpleados)
```
GestordeFicherosDAT podrá implementar un método para cargar un registro concreto de forma directa indicando el número de registro.
```Java
public static Estudiante cargarRegistro(String fileName, int numReg)
```

### Main
Incluye instrucciones para comprobar que todos los métodos funcionan.
1. Crear un `ArrayList<Estudiante>` de ejemplo con estudiantes de muestra.
2. Guardar el contenido de este array en un archivo `.dat`, `xml`, y `csv`.
3. Leerá los contenidos de cada uno de estos arrchivos en arrays correspondientes:
   1. `ArrayList<Estudiante> estudiantesDAT`
   2. `ArrayList<Estudiante> estudiantesXML`
   3. `ArrayList<Estudiante> estudiantesCSV`
4. Imprimirá por pantalla el array de estudiantes original, así como cada uno de los creados a partir de las correspondientes lecturas de los archivos.

Ejemplo de impresión por pantalla:
```
===============================
Lista en XML
===============================
Nombre: Juan. ID: 1. Calif.: 8.56. Beca: true
Nombre: María. ID: 2. Calif.: 6.83. Beca: false
Nombre: Sara. ID: 3. Calif.: 9.23. Beca: false
Nombre: Jacinto. ID: 4. Calif.: 5.45. Beca: true
Nombre: Mario. ID: 5. Calif.: 7.83. Beca: false
```

## Ejemplos de contenido de los archivos: 
### Ejemplo de formato estudiantes.csv:
```CSV
ID;Nombre;Calificación  
1;Juan;8.56  
2;María;6.83  
3;Sara;9.23  
4;Jacinto;5.45  
5;Mario;7.83
```

### Ejemplo de formato estudiantes.xml:
```XML
<?xml version="1.0" encoding="UTF-8"?>  
<estudiantes>  
    <estudiante>       
	   <id>1</id>  
       <nombre>Juan</nombre>  
       <calificacion>8.56</calificacion>  
    </estudiante>
    <estudiante>       
	   <id>2</id>  
       <nombre>María</nombre>  
       <calificacion>6.83</calificacion>  
    </estudiante>    
    <estudiante>       
       <id>3</id>  
       <nombre>Sara</nombre>  
       <calificacion>9.23</calificacion>  
    </estudiante>    
    <estudiante>       
       <id>4</id>  
       <nombre>Jacinto</nombre>  
       <calificacion>5.45</calificacion>  
    </estudiante>    
    <estudiante>       
       <id>5</id>  
       <nombre>Mario</nombre>  
       <calificacion>7.83</calificacion>  
    </estudiante>
</estudiantes>
```

## Opcional: Impresión de datos por pantalla:
Cambiar el método `toString` de la clase `Estudiante` para que los campos tengan una longitud fija y se puedan leer más fácilmente

```
Nombre: Juan.        ID: 1.   Calif.: 8.56.   Beca: true
Nombre: María.       ID: 2.   Calif.: 6.83.   Beca: false
Nombre: Sara.        ID: 3.   Calif.: 9.23.   Beca: false
Nombre: Jacinto.     ID: 4.   Calif.: 5.45.   Beca: true
Nombre: Mario.       ID: 5.   Calif.: 7.83.   Beca: false
```


# Parte 2

Implementa en las clases GestorFicherosDAT y GestorFicherosCSV las siguientes funciones: 
- Añadir registro (al final del archivo)
- Modificar registro.
- Borrar registro.

## Borrado de un registro en un archivo de Acceso Aleatorio
Nota: Cuando borramos un registro en un fichero de acceso aleatorio, si borramos los datos y queremos utilizar su espacio, el sistema dejará de acceder al registro correctamente utilizando nuestro método. Para solucionarlo nos podemos plantear a grandes rasgos dos opciones:

### Opción A:
Cuando borremos un registro, lo marcaremos como borrado dando al `id` un valor de 0 o un valor negativo. Cuando leamos un registro y observemos este valor, daremos instrucciones a nuestro programa para que lo interprete como un registro eliminado.

### Opción B:
Implementar un sistema de indexado. Podemos crear una clase índice que mantendrá un mapeo de IDs de estudiantes a sus posiciones en el archivo. Puede ser una simple `HashMap` o cualquier otra estructura de datos adecuada.

De esta forma, la ubicación concreta del registro en el archivo no está directamente relacionada con el id del registro, sino que estará almacenada en el `HashMap`. Cuando creemos un archivo para guardar nuestros registros, crearemos un índice y lo inicializaremos con los valores oportunos. En adelante, siempre que hagamos una operación de adición, borrado o modificación del id, deberemos actualizar no solo el registro, si no su referencia en el `HashMap`. Si borramos un registro, podemos asociar a su índice, una posición `null`.

Esta opción puede ser interesante para sistemas que sufren muchos cambios.

#### Modificación de métodos existentes.
Si utilizamos un índice, tendremos que modificar los métodos existentes para que utilicen este índice al buscar registros.
    



---

**Método para Borrar un Registro**: Esto puede ser complicado, ya que implica no solo eliminar el registro del archivo sino también actualizar el índice y potencialmente mover otros registros en el archivo para llenar el espacio vacío.

Crea una clase que implemente operaciones para añadir, buscar, borrar y modificar registros de un fichero con organización secuencial indexada. Existirá un único índice para el campo clave del fichero. El índice será un fichero adicional cuyo nombre indique el fichero principal (de datos) y el campo de indexación (que, en este caso, y según se ha dicho, es el campo clave). El índice lo creará el constructor de la clase, junto con el fichero principal. Los registros borrados no se deben borrar, sino marcarse como borrados tanto en el fichero principal como en el fichero de índice. En este último se podría poner un número negativo como posición para indicar que el registro está borrado. Los nuevos registros se añadirán siempre al final del fichero principal.

La operación de inserción debe recomponer el índice, para ello hay que insertar una nueva entrada en el lugar apropiado. El índice no es más que un tipo especial de fichero secuencial ordenado, y el fichero principal un fichero secuencial no ordenado, por lo que se pueden utilizar las clases desarrolladas en ejercicios anteriores.