
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
<tr><td>TÍTULO DE LA PRÁCTICA:</td><td colspan="5">AVL</td></tr>
<tr>
<td>NÚMERO DE PRÁCTICA:</td><td>05</td><td>AÑO LECTIVO:</td><td>2025 A</td><td>NRO. SEMESTRE:</td><td>III</td>
</tr>
<tr>
<td>FECHA INICIO::</td><td>11-Jun-2025</td><td>FECHA FIN:</td><td>17-Jun-2025</td><td>DURACIÓN:</td><td>02 horas</td>
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
Realizar ejercicios en temas de AVL.

## EJERCICIOS PROPUESTOS

### ENLACE AL LABORATORIO 05

A continuación se presenta el enlace al cuaderno de Google Colab que contiene los ejercicios correspondientes a las **actividades y problemas propuestos del Laboratorio 05**. Este material debe ser revisado y desarrollado como parte del trabajo práctico.

🔗 [Acceder al cuaderno de ejercicios del Laboratorio 05](https://colab.research.google.com/drive/1i9Cykms3NxEimVC7ICZEmld-ch-JFlhr?usp=sharing)

### TAREA
Elabore un informe implementando Arboles AVL con toda la lista de operaciones : 
- search(),
- getMin(), 
- getMax(), 
- parent(), 
- son(), 
- insert()

INPUT: Una sóla palabra en mayúsculas.  
OUTPUT: Se debe construir el  árbol AVL considerando el valor decimal de su código ascii.

Luego, pruebe todas sus operaciones implementadas.
## Resolución

### 1. Clase Nodo
- ```sh
  public class Nodo<T> {
      T dato;
      Nodo<T> izquierdo;
      Nodo<T> derecho;
      int altura;
  
      public Nodo(T dato) {
          this.dato = dato;
          this.izquierdo = null;
          this.derecho = null;
          this.altura = 1;
      }
  }
  ```
  
### 2. Clase ArbolAVL
- ```sh
  public class ArbolAVL {
      private Nodo<Integer> raiz;
  
      public void insertar(int dato) {
          raiz = insertarRec(raiz, dato);
      }
  
      private Nodo<Integer> insertarRec(Nodo<Integer> nodo, int dato) {
          if (nodo == null) return new Nodo<>(dato);
  
          if (dato < nodo.dato)
              nodo.izquierdo = insertarRec(nodo.izquierdo, dato);
          else if (dato > nodo.dato)
              nodo.derecho = insertarRec(nodo.derecho, dato);
          else
              return nodo; // no duplicados
  
          actualizarAltura(nodo);
          return balancear(nodo);
      }
  
      public boolean buscar(int clave) {
          return buscarRec(raiz, clave) != null;
      }
  
      private Nodo<Integer> buscarRec(Nodo<Integer> nodo, int clave) {
          if (nodo == null || nodo.dato == clave) return nodo;
          return (clave < nodo.dato) ?
              buscarRec(nodo.izquierdo, clave) : buscarRec(nodo.derecho, clave);
      }
  
      public int getMin() {
          if (raiz == null) throw new IllegalStateException("Árbol vacío");
          Nodo<Integer> actual = raiz;
          while (actual.izquierdo != null)
              actual = actual.izquierdo;
          return actual.dato;
      }
  
      public int getMax() {
          if (raiz == null) throw new IllegalStateException("Árbol vacío");
          Nodo<Integer> actual = raiz;
          while (actual.derecho != null)
              actual = actual.derecho;
          return actual.dato;
      }
  
      public Integer parent(int clave) {
          return parentRec(raiz, clave, null);
      }
  
      private Integer parentRec(Nodo<Integer> nodo, int clave, Nodo<Integer> padre) {
          if (nodo == null) return null;
          if (nodo.dato == clave)
              return (padre != null) ? padre.dato : null;
          return (clave < nodo.dato) ?
              parentRec(nodo.izquierdo, clave, nodo) : parentRec(nodo.derecho, clave, nodo);
      }
  
      public String son(int clave) {
          Nodo<Integer> nodo = buscarRec(raiz, clave);
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
  
      private void actualizarAltura(Nodo<Integer> nodo) {
          int altIzq = (nodo.izquierdo != null) ? nodo.izquierdo.altura : 0;
          int altDer = (nodo.derecho != null) ? nodo.derecho.altura : 0;
          nodo.altura = 1 + Math.max(altIzq, altDer);
      }
  
      private int getBalance(Nodo<Integer> nodo) {
          if (nodo == null) return 0;
          int altIzq = (nodo.izquierdo != null) ? nodo.izquierdo.altura : 0;
          int altDer = (nodo.derecho != null) ? nodo.derecho.altura : 0;
          return altIzq - altDer;
      }
  
      private Nodo<Integer> balancear(Nodo<Integer> nodo) {
          int balance = getBalance(nodo);
  
          if (balance < -1 && getBalance(nodo.derecho) <= 0)
              return rotarIzquierda(nodo);
  
          if (balance > 1 && getBalance(nodo.izquierdo) >= 0)
              return rotarDerecha(nodo);
  
          if (balance < -1 && getBalance(nodo.derecho) > 0) {
              nodo.derecho = rotarDerecha(nodo.derecho);
              return rotarIzquierda(nodo);
          }
  
          if (balance > 1 && getBalance(nodo.izquierdo) < 0) {
              nodo.izquierdo = rotarIzquierda(nodo.izquierdo);
              return rotarDerecha(nodo);
          }
  
          return nodo;
      }
  
      private Nodo<Integer> rotarDerecha(Nodo<Integer> y) {
          Nodo<Integer> x = y.izquierdo;
          Nodo<Integer> T2 = x.derecho;
          x.derecho = y;
          y.izquierdo = T2;
          actualizarAltura(y);
          actualizarAltura(x);
          return x;
      }
  
      private Nodo<Integer> rotarIzquierda(Nodo<Integer> x) {
          Nodo<Integer> y = x.derecho;
          Nodo<Integer> T2 = y.izquierdo;
          y.izquierdo = x;
          x.derecho = T2;
          actualizarAltura(x);
          actualizarAltura(y);
          return y;
      }
  }
  ```
  
  ### 3. Clase Main
- ```sh
  public class Main {
      public static void main(String[] args) {
          ArbolAVL arbol = new ArbolAVL();
          String palabra = "HOLA";
  
          for (char c : palabra.toCharArray()) {
              int ascii = (int) c;
              arbol.insertar(ascii);
              System.out.println("Insertado: " + c + " (" + ascii + ")");
          }
  
          System.out.println("Min: " + arbol.getMin());
          System.out.println("Max: " + arbol.getMax());
          System.out.println("Buscar 79: " + arbol.buscar(79)); // O
          System.out.println("Padre de 79: " + arbol.parent(79));
          System.out.println(arbol.son(76)); // L
      }
  }
  ```
  ### Ejemplo de salida (HOLAMUNDO)
  ![image](https://github.com/user-attachments/assets/1d74e269-f5e9-4d92-a6c5-a0eb78b7db9a)
  
## Cuestionario
### ¿Explique como es el algoritmo que implementó para obtener el factor de equilibrio de un nodo?
<p align="justify">
El algoritmo que implementé para obtener el factor de equilibrio de un nodo en un árbol AVL se basa en calcular la diferencia entre las alturas de sus subárboles izquierdo y derecho. Para ello, primero se verifica si el nodo es nulo; en ese caso, se considera que su factor de equilibrio es cero. Luego, si el nodo no es nulo, se obtiene la altura del hijo izquierdo (si existe) y del hijo derecho (si existe). Si alguno de ellos no existe, su altura se considera como cero. Finalmente, se calcula el factor de equilibrio restando la altura del subárbol derecho a la altura del subárbol izquierdo.  
</p>
<p align="justify">
Este valor permite determinar si el nodo está balanceado. Si el resultado es 0, 1 o -1, el nodo se considera equilibrado. Sin embargo, si el valor es mayor que 1 o menor que -1, se considera que el nodo está desbalanceado y se deben aplicar rotaciones para restaurar el equilibrio del árbol.
</p>

## REFERENCIAS
- https://www.w3schools.com/java/
- https://www.eclipse.org/downloads/packages/release/2022-03/r/eclipse-ide-enterprise-java-and-web-developers
- https://docs.oracle.com/javase/7/docs/api/java/util/List.html
- https://docs.oracle.com/javase/tutorial/java/generics/types.html
