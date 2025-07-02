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

## EJERCICIOS PROPUESTOS
### Estructura del proyecto
Crea un paquete btreelab y dentro los siguientes archivos:  
● BTreeNode.java: define la clase para los nodos del árbol.  
● BTree.java: clase que encapsula las operaciones del B‐Tree.  
● Main.java: programa principal para probar el árbol (lectura, inserción, eliminación).  

### ENLACE AL LABORATORIO 03

A continuación se presenta el enlace al cuaderno de Google Colab que contiene los ejercicios correspondientes a las **actividades y problemas propuestos del Laboratorio 03**. Este material debe ser revisado y desarrollado como parte del trabajo práctico.

🔗 [Acceder al cuaderno de ejercicios del Laboratorio 03](https://colab.research.google.com/drive/1RNQ-0Ahra_caUuQPTx-oedzQEIdntowK?usp=sharing)

### CÓDIGO FUENTE

El desarrollo de los ejercicios se realizó en el entorno [CS50.dev](https://cs50.dev/), utilizando el lenguaje de programación Java.  
Los archivos fuente se encuentran organizados por ejercicios y fueron posteriormente documentados en este repositorio.

> Nota: CS50.dev no permite compartir enlaces públicos directos a los archivos. Por lo tanto, el código completo ha sido subido en esta plataforma (GitHub) para su revisión.

### MAIN
- ```sh
    package btreelab;
    
    public class main {
        public static void main(String[] args) {
            int t = 3; // grado minimo
            BTree tree = new BTree(t);
    
            int[] values = {8, 9, 10, 11, 15, 20, 17};
            for (int v : values) tree.insert(v);
    
            System.out.println("Recordio del árbol:");
            tree.traverse();
    
            tree.remove(20);
            System.out.println("\nTras eliminar 10:");
            tree.traverse();
        }
    }
  ```
  
### 1. Agregar un método para contar los elementos de la lista.
- ```sh
    package btreelab;
    
    public class BTree {
        private BTreeNode root;
        private int t;
    
        public BTree(int t) {
            this.root = null;
            this.t = t;
        }
    
        public void traverse() {
            if (root != null) root.traverse();
        }
    
        public BTreeNode search(int key) {
            return (root == null) ? null : root.search(key);
        }
    
        public void insert(int key) {
            if (root == null) {
                root = new BTreeNode(t, true);
                root.keys[0] = key;
                root.numKeys = 1;
            } else {
                if (root.numKeys == 2*t - 1) {
                    BTreeNode s = new BTreeNode(t, false);
                    s.children[0] = root;
                    s.splitChild(0, root);
                    int idx = (s.keys[0] < key) ? 1 : 0;
                    s.children[idx].insertNonFull(key);
                    root = s;
                } else {
                    root.insertNonFull(key);
                }
            }
        }
    
        public void remove(int key) {
            if (root == null) {
                System.out.println("El árbol está vacío");
                return;
            }
            root.remove(key);
            if (root.numKeys == 0) {
                root = root.isLeaf ? null : root.children[0];
            }
        }
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

## REFERENCIAS
- https://www.w3schools.com/java/
- https://www.eclipse.org/downloads/packages/release/2022-03/r/eclipse-ide-enterprise-java-and-web-developers
- https://docs.oracle.com/javase/7/docs/api/java/util/List.html
- https://docs.oracle.com/javase/tutorial/java/generics/types.html
