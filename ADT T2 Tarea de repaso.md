
### 1. Añadir un campo booleano `becado`.

# Refactorización y nuevas clases

Reorganizar el código de la clase Estudiante.

Utilizar `ArrayList<Estudiante>` en lugar de `Estudiante[]`. A la hora de realizar la lectura, disfrutaremos de varias ventajas: flexibilidad en el tamaño, métodos útiles como `add()`, `remove()`, `size()`, `isEmpty()`, y otros que nos simplificarán la manipulación de la colección. Más allá del uso que nosotros le demos en nuestros gestores de archivos, la colección será más útil en este formato para futuras operaciones que queramos hacer con la misma.

```java
public void cargarLista(List<Estudiante> listaEmpleados)
public void guardarLista(List<Estudiante> listaEmpleados)
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

### A implementar solo por GestorFicherosDAT

```Java
public static Estudiante cargarRegistro(String fileName, int numReg)
}
```

### Main
Incluye instrucciones para comprobar que todos los métodos funcionan.

### Ejemplos de contenido de archivos
ejemplo de formato CSV:
```CSV
ID,Nombre,Calificación  
1,Juan,8.56  
2,María,6.83  
3,Sara,9.23  
4,Jacinto,5.45  
5,Mario,7.83
```

Ejemplo de formato XML:
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
