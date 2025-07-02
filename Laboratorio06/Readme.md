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
<tr><td>TÍTULO DE LA PRÁCTICA:</td><td colspan="5">B‐Tree (en Java)</td></tr>
<tr>
<td>NÚMERO DE PRÁCTICA:</td><td>03</td><td>AÑO LECTIVO:</td><td>2025 A</td><td>NRO. SEMESTRE:</td><td>III</td>
</tr>
<tr>
<td>FECHA INICIO::</td><td>25-Jun-2025</td><td>FECHA FIN:</td><td>01-Jul-2025</td><td>DURACIÓN:</td><td>02 horas</td>
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

- Para este laboratorio, explorarán cómo implementar un B‐Tree en Java, junto con sus operaciones principales: búsqueda,
inserción y eliminación, manteniendo las propiedades de balanceo.

### Propiedades del B-Tree:
Todos las hojas están en el mismo nivel.
● El B-Tree está definido por el término grado mínimo ‘b‘.
● Cada nodo excepto la raíz debe contener al menos b-1 llaves. La raíz puede contener un mínimo de 1 llave.
● Todos los nodos (incluida la raíz) pueden contener como máximo (2*b – 1) llaves.
● El número de hijos de un nodo es igual al número de llaves en él más 1.
● Todas las llaves de un nodo están ordenadas en orden creciente. El hijo entre dos llaves k1 y k2 contiene todas las llaves en el rango de k1 y k2.
● El B-Tree crece y se reduce desde la raíz, a diferencia del Árbol de Búsqueda Binaria. Los Árboles de Búsqueda Binaria crecen hacia abajo y también se reducen hacia abajo.
● Al igual que otros Árboles de Búsqueda Binaria equilibrados, la complejidad temporal para buscar, insertar y eliminar es O(log_b n).
● La inserción de un nodo en un B-Tree ocurre solo en un nodo hoja.

### COMPETENCIAS

- C.m. Construye responsablemente soluciones haciendo uso de estructuras de datos y algoritmos, siguiendo un proceso adecuado para resolver problemas computacionales que se ajustan al uso de los recursos disponibles y a especificaciones concretas.

## EJERCICIOS PROPUESTOS

### ENLACE AL LABORATORIO 03

A continuación se presenta el enlace al cuaderno de Google Colab que contiene los ejercicios correspondientes a las **actividades y problemas propuestos del Laboratorio 03**. Este material debe ser revisado y desarrollado como parte del trabajo práctico.

🔗 [Acceder al cuaderno de ejercicios del Laboratorio 03](https://colab.research.google.com/drive/1RNQ-0Ahra_caUuQPTx-oedzQEIdntowK?usp=sharing)

### CÓDIGO FUENTE

El desarrollo de los ejercicios se realizó en el entorno [CS50.dev](https://cs50.dev/), utilizando el lenguaje de programación Java.  
Los archivos fuente se encuentran organizados por ejercicios y fueron posteriormente documentados en este repositorio.

> Nota: CS50.dev no permite compartir enlaces públicos directos a los archivos. Por lo tanto, el código completo ha sido subido en esta plataforma (GitHub) para su revisión.

### MAIN
- ```sh
  public class ListaCircularMain {
    public static void main(String[] args) {
        ListaCircular lista = new ListaCircular();

        System.out.println("Insertando elementos...");
        lista.insertar(10);
        lista.insertar(20);
        lista.insertar(30);
        lista.mostrar();

        System.out.println("Eliminando 20...");
        lista.eliminar(20);
        lista.mostrar();

        System.out.println("Eliminando 10...");
        lista.eliminar(10);
        lista.mostrar();

        System.out.println("Eliminando 30...");
        lista.eliminar(30);
        lista.mostrar();

        System.out.println("Insertando de nuevo...");
        lista.insertar(100);
        lista.mostrar();
    }
  }
  ```
## ACTIVIDADES

### 1. Agregar un método para contar los elementos de la lista.
- ```sh
  public int contar() {
      if (ultimo == null) return 0;
      int contador = 0;
      Nodo actual = ultimo.siguiente;
      do {
          contador++;
          actual = actual.siguiente;
      } while (actual != ultimo.siguiente);
      return contador;
  }
  ```

### 2. Agregar un método para buscar un elemento en la lista.
- ```sh
  public boolean buscar(int dato) {
      if (ultimo == null) return false;
      Nodo actual = ultimo.siguiente;
      do {
          if (actual.dato == dato) return true;
          actual = actual.siguiente;
      } while (actual != ultimo.siguiente);
      return false;
  }
  ```
### 3. Modificar la lista para que también acepte datos String (usando generics).
- ```sh
  public class Nodo<T> {
      T dato;
      Nodo<T> siguiente;
  
      public Nodo(T dato) {
          this.dato = dato;
          this.siguiente = null;
      }
  }
  ```
Muestra de cambios en clase ListaCircular
- ```sh
  public class ListaCircular<T> {
      private Nodo<T> ultimo;
  
      public ListaCircular() {
          ultimo = null;
      }
  
      public void insertar(T dato) {
          Nodo<T> nuevo = new Nodo<>(dato);
          if (ultimo == null) {
              ultimo = nuevo;
              ultimo.siguiente = ultimo;
          } else {
              nuevo.siguiente = ultimo.siguiente;
              ultimo.siguiente = nuevo;
              ultimo = nuevo;
          }
      }
  ```
#

## PROBLEMAS PROPUESTOS
📌 Problema 1: Insertar al inicio y al final
Objetivo: Implementa una lista doblemente enlazada que permita insertar nodos tanto al
inicio como al final.
Desafío adicional: Mostrar la lista en orden normal y reverso.

AL INICIO
- ```sh
  public void insertarInicio(int dato) {
      Nodo nuevo = new Nodo(dato);
      if (cabeza == null) {
          cabeza = cola = nuevo;
      } else {
          nuevo.siguiente = cabeza;
          cabeza.anterior = nuevo;
          cabeza = nuevo;
      }
  }
  ```
AL FINAL
- ```sh
  public void insertarFinal(int dato) {
      Nodo nuevo = new Nodo(dato);
      if (cola == null) {
          cabeza = cola = nuevo;
      } else {
          cola.siguiente = nuevo;
          nuevo.anterior = cola;
          cola = nuevo;
      }
  }
  ```
 MOSTRAR
- ```sh
    public void mostrarNormal() {
        Nodo actual = cabeza;
        while (actual != null) {
            System.out.print(actual.dato + " ⇄ ");
            actual = actual.siguiente;
        }
        System.out.println("null");
    }
    
    
    public void mostrarReverso() {
        Nodo actual = cola;
        while (actual != null) {
            System.out.print(actual.dato + " ⇄ ");
            actual = actual.anterior;
        }
        System.out.println("null");
    }
  ```

📌 Problema 2: Eliminar nodos
Objetivo: Agrega métodos para eliminar nodos por valor, por posición, y eliminar el primer y
último elemento.
Desafío adicional: Manejar bien los casos extremos (lista vacía, un solo nodo, nodo no
encontrado).
POR VALOR
- ```sh
    public void eliminarPorValor(int valor) {
        Nodo actual = cabeza;
        while (actual != null) {
            if (actual.dato == valor) {
                if (actual == cabeza) cabeza = actual.siguiente;
                if (actual == cola) cola = actual.anterior;
                if (actual.anterior != null) actual.anterior.siguiente = actual.siguiente;
                if (actual.siguiente != null) actual.siguiente.anterior = actual.anterior;
                return;
            }
            actual = actual.siguiente;
        }
    }
  ```
POR POSICION
- ```sh
    public void eliminarPorPosicion(int posicion) {
        if (posicion < 0) return;
        Nodo actual = cabeza;
        for (int i = 0; actual != null && i < posicion; i++) {
            actual = actual.siguiente;
        }
        if (actual == null) return;
        if (actual == cabeza) cabeza = actual.siguiente;
        if (actual == cola) cola = actual.anterior;
        if (actual.anterior != null) actual.anterior.siguiente = actual.siguiente;
        if (actual.siguiente != null) actual.siguiente.anterior = actual.anterior;
    }
    ```
PRIMERO Y ÚLTIMO
- ```sh
    public void mostrarNormal() {
        if (cabeza == null) {
            System.out.println("Lista vacía");
            return;
        }
        Nodo actual = cabeza;
        while (actual != null) {
            System.out.print(actual.dato);
            if (actual.siguiente != null) System.out.print(" ⇄ ");
            actual = actual.siguiente;
        }
        System.out.println();
    }

    public void mostrarReverso() {
        if (cola == null) {
            System.out.println("Lista vacía");
            return;
        }
        Nodo actual = cola;
        while (actual != null) {
            System.out.print(actual.dato);
            if (actual.anterior != null) System.out.print(" ⇄ ");
            actual = actual.anterior;
        }
        System.out.println();
    }
    ```

📌 Problema 3: Revertir la lista
Objetivo: Implementa un método que invierta el orden de los nodos en la lista doblemente
enlazada.
Entrada: 1 ⇄ 2 ⇄ 3 ⇄ 4
Salida esperada: 4 ⇄ 3 ⇄ 2 ⇄ 1
- ```sh
    public void revertir() {
        Nodo actual = cabeza;
        Nodo temp = null;
        while (actual != null) {
            temp = actual.anterior;
            actual.anterior = actual.siguiente;
            actual.siguiente = temp;
            actual = actual.anterior;
        }
        if (temp != null) cabeza = temp.anterior;
    }
  ```

📌 Problema 4: Eliminar duplicados
Objetivo: Eliminar nodos duplicados en una lista doblemente enlazada (por valor).
Entrada: 2 ⇄ 3 ⇄ 2 ⇄ 5 ⇄ 3
Salida esperada: 2 ⇄ 3 ⇄ 5
- ```sh
    public void eliminarDuplicados() {
        Nodo actual = cabeza;
        while (actual != null) {
            Nodo comparador = actual.siguiente;
            while (comparador != null) {
                if (comparador.dato == actual.dato) {
                    if (comparador == cola) cola = comparador.anterior;
                    comparador.anterior.siguiente = comparador.siguiente;
                    if (comparador.siguiente != null)
                        comparador.siguiente.anterior = comparador.anterior;
                }
                comparador = comparador.siguiente;
            }
            actual = actual.siguiente;
        }
    }
  ```

📌 Problema 5: Lista ordenada
Objetivo: Implementar una lista doblemente enlazada que mantenga los nodos ordenados
al insertar.
Entrada de inserciones: 4, 1, 3, 2
Lista final: 1 ⇄ 2 ⇄ 3 ⇄ 4
- ```sh
    public void insertarOrdenado(int dato) {
        Nodo nuevo = new Nodo(dato);
        if (cabeza == null || dato < cabeza.dato) {
            insertarInicio(dato);
            return;
        }
        Nodo actual = cabeza;
        while (actual.siguiente != null && actual.siguiente.dato < dato) {
            actual = actual.siguiente;
        }
        nuevo.siguiente = actual.siguiente;
        if (actual.siguiente != null) actual.siguiente.anterior = nuevo;
        nuevo.anterior = actual;
        actual.siguiente = nuevo;
        if (nuevo.siguiente == null) cola = nuevo;
    }
  ```

## REFERENCIAS
- https://www.w3schools.com/java/
- https://www.eclipse.org/downloads/packages/release/2022-03/r/eclipse-ide-enterprise-java-and-web-developers
- https://docs.oracle.com/javase/7/docs/api/java/util/List.html
- https://docs.oracle.com/javase/tutorial/java/generics/types.html
