<div align="center">
<table>
    <theader>
        <tr>
            <td><img src="https://github.com/rescobedoq/pw2/blob/main/epis.png?raw=true" alt="EPIS" style="width:50%; height:auto"/></td>
            <th>
                <span style="font-weight:bold;">UNIVERSIDAD NACIONAL DE SAN AGUSTIN</span><br />
                <span style="font-weight:bold;">FACULTAD DE INGENIERÍA DE PRODUCCIÓN Y SERVICIOS</span><br />
                <span style="font-weight:bold;">DEPARTAMENTO ACADÉMICO DE INGENIERÍA DE SISTEMAS E INFORMÁTICA</span><br />
                <span style="font-weight:bold;">ESCUELA PROFESIONAL DE INGENIERÍA DE SISTEMAS</span>
            </th>
            <td><img src="https://github.com/rescobedoq/pw2/blob/main/abet.png?raw=true" alt="ABET" style="width:50%; height:auto"/></td>
        </tr>
    </theader>
    <tbody>
        <tr><td colspan="3"><span style="font-weight:bold;">Formato</span>: Guía de Práctica de Laboratorio</td></tr>
        <tr><td><span style="font-weight:bold;">Aprobación</span>:  2022/03/01</td><td><span style="font-weight:bold;">Código</span>: GUIA-PRLD-001</td><td><span style="font-weight:bold;">Página</span>: 1</td></tr>
    </tbody>
</table>
</div>


<table>
<theader>
<tr><th colspan="6">INFORMACIÓN BÁSICA</th></tr>
</theader>
<tbody>
<tr><td>ASIGNATURA:</td><td colspan="5">Estructura de Datos y Algoritmos</td></tr>
<tr><td>TÍTULO DE LA PRÁCTICA:</td><td colspan="5">TDA BST</td></tr>
<tr>
<td>NÚMERO DE PRÁCTICA:</td><td>04</td><td>AÑO LECTIVO:</td><td>2025 A</td><td>NRO. SEMESTRE:</td><td>III</td>
</tr>
<tr>
<td>FECHA INICIO::</td><td>28-May-2025</td><td>FECHA FIN:</td><td>03-Jun-2025</td><td>DURACIÓN:</td><td>02 horas</td>
</tr>
<tr><td colspan="6">ESTUDIANTE:
<ul>
<li>Jimmy Joaquín Vilca Peralta</li>
</ul>
</td>
</<tr>
</<tr>
<tr><td colspan="6">DOCENTES:
<ul>
<li>Edson Luque Mamani</li>
</ul>
</td>
</<tr>
</tdbody>
</table>


## OBJETIVOS TEMAS Y COMPETENCIAS

### OBJETIVOS
Realizar ejercicios en temas de Estructuras de datos, tipos de datos abstractos, bucles, Arrays, Listas enlazadas, Recursión.

### TEMAS
TAD  
BST

### COMPETENCIAS
C.m. Construye responsablemente soluciones haciendo uso de estructuras de datos y algoritmos, siguiendo un proceso adecuado para resolver problemas computacionales que se ajustan al uso de los recursos disponibles y a especificaciones concretas.

## EJERCICIOS PROPUESTOS

### ENLACE AL LABORATORIO 04

A continuación se presenta el enlace al cuaderno de Google Colab que contiene los ejercicios correspondientes a las **actividades y problemas propuestos del Laboratorio 04**. Este material debe ser revisado y desarrollado como parte del trabajo práctico.

🔗 [Acceder al cuaderno de ejercicios del Laboratorio 04](https://colab.research.google.com/drive/184aV6gfGLSEaWylsbV5feozoC2E6nDzo?usp=sharing)

### Parte 01 (clase)
- Elabore un informe implementando Arboles de Búsqueda Binarios con toda la lista de operaciones:
  - search(), getMin(), getMax(), parent(), son(), insert().
  - INPUT: Una sóla palabra en mayúsculas.
  - OUTPUT: Se debe contruir el BST considerando el valor decimal de su código ascii.  

Luego, pruebe todas sus operaciones implementadas.
## Resolución

### 1. Clase Nodo
- ```sh
  public class Nodo<T> {
    T dato;
    Nodo<T> izquierdo;
    Nodo<T> derecho;
  
    public Nodo(T dato) {
        this.dato = dato;
        this.izquierdo = null;
        this.derecho = null;
    }
  }
  ```
### 2. Clase ArbolBinarioBusqueda
- ```sh
  public class ArbolBinarioBusqueda<T extends Comparable<T>> {
      private Nodo<T> raiz;
  
      public ArbolBinarioBusqueda() {
          raiz = null;
      }
  
      public void insertar(T dato) {
          raiz = insertarRecursivo(raiz, dato);
      }
  
      private Nodo<T> insertarRecursivo(Nodo<T> nodo, T dato) {
          if (nodo == null) return new Nodo<>(dato);
          if (dato.compareTo(nodo.dato) < 0)
              nodo.izquierdo = insertarRecursivo(nodo.izquierdo, dato);
          else if (dato.compareTo(nodo.dato) > 0)
              nodo.derecho = insertarRecursivo(nodo.derecho, dato);
          return nodo;
      }
  
      public boolean buscar(T clave) {
          return buscarRecursivo(raiz, clave) != null;
      }
  
      private Nodo<T> buscarRecursivo(Nodo<T> nodo, T clave) {
          if (nodo == null || nodo.dato.equals(clave))
              return nodo;
          return (clave.compareTo(nodo.dato) < 0) ?
              buscarRecursivo(nodo.izquierdo, clave) : buscarRecursivo(nodo.derecho, clave);
      }
  
      public T obtenerMinimo() {
          if (raiz == null) return null;
          Nodo<T> actual = raiz;
          while (actual.izquierdo != null)
              actual = actual.izquierdo;
          return actual.dato;
      }
  
      public T obtenerMaximo() {
          if (raiz == null) return null;
          Nodo<T> actual = raiz;
          while (actual.derecho != null)
              actual = actual.derecho;
          return actual.dato;
      }
  
      public T padre(T clave) {
          return padreRecursivo(raiz, clave, null);
      }
  
      private T padreRecursivo(Nodo<T> nodo, T clave, Nodo<T> padre) {
          if (nodo == null) return null;
          if (nodo.dato.equals(clave))
              return (padre != null) ? padre.dato : null;
          return (clave.compareTo(nodo.dato) < 0) ?
              padreRecursivo(nodo.izquierdo, clave, nodo) : padreRecursivo(nodo.derecho, clave, nodo);
      }
  
      public String hijos(T clave) {
          Nodo<T> nodo = buscarRecursivo(raiz, clave);
          if (nodo == null) return "Nodo no encontrado";
          StringBuilder sb = new StringBuilder("Hijos de " + clave + ": ");
          if (nodo.izquierdo != null)
              sb.append("Izquierdo -> ").append(nodo.izquierdo.dato).append(" ");
          if (nodo.derecho != null)
              sb.append("Derecho -> ").append(nodo.derecho.dato);
          if (nodo.izquierdo == null && nodo.derecho == null)
              sb.append("No tiene hijos");
          return sb.toString();
      }
  
      public void recorridoEnOrden() {
          recorridoEnOrdenRecursivo(raiz);
          System.out.println();
      }
  
      private void recorridoEnOrdenRecursivo(Nodo<T> nodo) {
          if (nodo != null) {
              recorridoEnOrdenRecursivo(nodo.izquierdo);
              System.out.print(nodo.dato + " ");
              recorridoEnOrdenRecursivo(nodo.derecho);
          }
      }
  }
  ```
### 3. Clase Principal
- ```sh
  public class Arbol {
      public static void main(String[] args) {
          String palabra = "HOLAMUNDO";
          ArbolBinarioBusqueda<Integer> arbol = new ArbolBinarioBusqueda<>();
  
          System.out.println("Insertando caracteres de: " + palabra);
          for (char c : palabra.toCharArray()) {
              int ascii = (int) c;
              arbol.insertar(ascii);
              System.out.println("Insertado: " + c + " (" + ascii + ")");
          }
  
          System.out.print("Recorrido en orden: ");
          arbol.recorridoEnOrden();
  
          System.out.println("¿Existe 'A' (65)?: " + arbol.buscar(65));
          System.out.println("¿Existe 'Z' (90)?: " + arbol.buscar(90));
  
          System.out.println("Valor mínimo (menor ASCII): " + arbol.obtenerMinimo());
          System.out.println("Valor máximo (mayor ASCII): " + arbol.obtenerMaximo());
  
          System.out.println("Padre de 'M' (77): " + arbol.padre(77));
          System.out.println("Padre de 'O' (79): " + arbol.padre(79));
  
          System.out.println("Hijos de 'O' (79): " + arbol.hijos(79));
          System.out.println("Hijos de 'H' (72): " + arbol.hijos(72));
          System.out.println("Hijos de 'X' (88): " + arbol.hijos(88));
      }
  }
  ```

## REFERENCIAS
- https://www.w3schools.com/java/
- https://www.eclipse.org/downloads/packages/release/2022-03/r/eclipse-ide-enterprise-java-and-web-developers
- https://docs.oracle.com/javase/7/docs/api/java/util/List.html
- https://docs.oracle.com/javase/tutorial/java/generics/types.html
