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

### ENLACE AL LABORATORIO 06

A continuación se presenta el enlace al cuaderno de Google Colab que contiene los ejercicios correspondientes a las **actividades y problemas propuestos del Laboratorio 06**. Este material debe ser revisado y desarrollado como parte del trabajo práctico.

🔗 [Acceder al cuaderno de ejercicios del Laboratorio 06](https://colab.research.google.com/drive/1hS5_CQPfKLQiPvkfUPuKh3T2AN92Vpt-?usp=sharing)

### CÓDIGO FUENTE

El desarrollo de los ejercicios se realizó en el entorno [CS50.dev](https://cs50.dev/), utilizando el lenguaje de programación Java.  
Los archivos fuente se encuentran organizados por ejercicios y fueron posteriormente documentados en este repositorio.

> Nota: CS50.dev no permite compartir enlaces públicos directos a los archivos. Por lo tanto, el código completo ha sido subido en esta plataforma (GitHub) para su revisión.

### MAIN
- ```sh
    package btreelab;
    
    import java.io.File;
    import java.io.FileNotFoundException;
    import java.util.Scanner;
    
    public class Main {
        public static void main(String[] args) throws FileNotFoundException {
            int t = 3;
            BTree tree = new BTree(t);
    
            File file = new File("btreelab/datos.csv");
            Scanner sc = new Scanner(file);
    
            if (sc.hasNextLine()) sc.nextLine(); // Saltar encabezado
    
            System.out.println("Iniciando inserción...");
    
            long startTime = System.currentTimeMillis();
    
            while (sc.hasNextLine()) {
                String line = sc.nextLine();
                String[] parts = line.split(",");
                if (parts.length >= 2) {
                    try {
                        double value = Double.parseDouble(parts[1]);
                        tree.insert(value);
                    } catch (NumberFormatException e) {
                        System.out.println("Error al parsear: " + parts[1]);
                    }
                }
            }
    
            sc.close();
    
            long endTime = System.currentTimeMillis();
            long elapsed = endTime - startTime;
    
            System.out.println("Inserción completada.");
            System.out.println("Tiempo total: " + elapsed + " ms");
    
            double[] ejemplos = {0.5, 0.19428027181445773, 0.9582492199402736};
    
            for (double key : ejemplos) {
                System.out.println("Buscando " + key + " ... " +
                    (tree.search(key) != null ? "Encontrado" : "No encontrado"));
            }
        }
    }
  ```
  
### BTree
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
    
        public BTreeNode search(double key) {
            return (root == null) ? null : root.search(key);
        }
    
        public void insert(double key) {
            if (root == null) {
                root = new BTreeNode(t, true);
                root.keys[0] = key;
                root.numKeys = 1;
            } else {
                if (root.numKeys == 2 * t - 1) {
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
    
        public void remove(double key) {
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

### BTreeNode
- ```sh
    package btreelab;
    
    public class BTreeNode {
        double[] keys;             // claves
        int minDegree;             // grado mínimo t
        BTreeNode[] children;      // hijos
        int numKeys;               // número de claves actuales
        boolean isLeaf;            // indica si es hoja
    
        public BTreeNode(int t, boolean leaf) {
            this.minDegree = t;
            this.isLeaf = leaf;
            this.keys = new double[2 * t - 1];         // ← cambiado a double
            this.children = new BTreeNode[2 * t];
            this.numKeys = 0;
        }
    
        public void traverse() {
            int i;
            for (i = 0; i < numKeys; i++) {
                if (!isLeaf)
                    children[i].traverse();
                System.out.print(keys[i] + " ");
            }
            if (!isLeaf)
                children[i].traverse();
        }
    
        public BTreeNode search(double key) {
            int i = 0;
            while (i < numKeys && key > keys[i])
                i++;
    
            if (i < numKeys && keys[i] == key)
                return this;
    
            if (isLeaf)
                return null;
    
            return children[i].search(key);
        }
    
        public void insertNonFull(double key) {
            int i = numKeys - 1;
    
            if (isLeaf) {
                while (i >= 0 && keys[i] > key) {
                    keys[i + 1] = keys[i];
                    i--;
                }
                keys[i + 1] = key;
                numKeys++;
            } else {
                while (i >= 0 && keys[i] > key)
                    i--;
    
                if (children[i + 1].numKeys == 2 * minDegree - 1) {
                    splitChild(i + 1, children[i + 1]);
    
                    if (keys[i + 1] < key)
                        i++;
                }
                children[i + 1].insertNonFull(key);
            }
        }
    
        public void splitChild(int i, BTreeNode y) {
            BTreeNode z = new BTreeNode(y.minDegree, y.isLeaf);
            z.numKeys = minDegree - 1;
    
            for (int j = 0; j < minDegree - 1; j++)
                z.keys[j] = y.keys[j + minDegree];
    
            if (!y.isLeaf) {
                for (int j = 0; j < minDegree; j++)
                    z.children[j] = y.children[j + minDegree];
            }
    
            y.numKeys = minDegree - 1;
    
            for (int j = numKeys; j >= i + 1; j--)
                children[j + 1] = children[j];
    
            children[i + 1] = z;
    
            for (int j = numKeys - 1; j >= i; j--)
                keys[j + 1] = keys[j];
    
            keys[i] = y.keys[minDegree - 1];
            numKeys++;
        }
    
        public int findKey(double key) {
            int idx = 0;
            while (idx < numKeys && keys[idx] < key)
                idx++;
            return idx;
        }
    
        public void remove(double key) {
            System.out.println("\nFunción remove() aún no implementada completamente.");
        }
    }
  ```

## REFERENCIAS
- https://www.w3schools.com/java/
- https://www.eclipse.org/downloads/packages/release/2022-03/r/eclipse-ide-enterprise-java-and-web-developers
- https://docs.oracle.com/javase/7/docs/api/java/util/List.html
- https://docs.oracle.com/javase/tutorial/java/generics/types.html
