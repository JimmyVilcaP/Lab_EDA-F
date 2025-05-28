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
<tr><td>TÍTULO DE LA PRÁCTICA:</td><td colspan="5">TDA lista parte 01</td></tr>
<tr>
<td>NÚMERO DE PRÁCTICA:</td><td>02</td><td>AÑO LECTIVO:</td><td>2025 A</td><td>NRO. SEMESTRE:</td><td>III</td>
</tr>
<tr>
<td>FECHA INICIO::</td><td>14-May-2025</td><td>FECHA FIN:</td><td>21-May-2025</td><td>DURACIÓN:</td><td>02 horas</td>
</tr>
<tr><td colspan="6">ESTUDIANTE:
<ul>
<li>Jimmy Joaquín Vilca Peralta</li>
</ul>
</td>
</<tr>
<tr><td colspan="6">RECURSOS:
    <ul>
        <li>https://www.w3schools.com/java/</li>
        <li>https://www.eclipse.org/downloads/packages/release/2022-03/r/eclipse-ide-enterprise-java-and-web-developers</li>
        <li>https://docs.oracle.com/javase/7/docs/api/java/util/List.html</li>
        <li>https://docs.oracle.com/javase/tutorial/java/generics/types.html</li>
    </ul>
</td>
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

- Realizar ejercicios en temas de Estructuras de datos, tipos de datos abstractos, bucles, Arrays, Listas enlazadas, Recursión.

### TEMAS
- TAD
- Arrays

### COMPETENCIAS

- C.m. Construye responsablemente soluciones haciendo uso de estructuras de datos y algoritmos, siguiendo un proceso adecuado para resolver problemas computacionales que se ajustan al uso de los recursos disponibles y a especificaciones concretas.

## EJERCICIOS PROPUESTOS

### ENLACE AL LABORATORIO 02

A continuación se presenta el enlace al cuaderno de Google Colab correspondiente al **Laboratorio 02**, el cual contiene únicamente los **Ejercicios 3**. Se recomienda revisar y desarrollar este contenido como parte del trabajo asignado.

🔗 [Acceder al cuaderno de ejercicios del Laboratorio 02](https://colab.research.google.com/drive/1It7GUnp6GxjFwvHcAYo--s68-C6UXPdJ?usp=sharing)

### CÓDIGO FUENTE

El desarrollo de los ejercicios se realizó en el entorno [CS50.dev](https://cs50.dev/), utilizando el lenguaje de programación Java.  
Los archivos fuente se encuentran organizados por ejercicios y fueron posteriormente documentados en este repositorio.

> Nota: CS50.dev no permite compartir enlaces públicos directos a los archivos. Por lo tanto, el código completo ha sido subido en esta plataforma (GitHub) para su revisión.


EJERCICIO 01. Invertir un matriz de enteros
Ejemplo:
A=[1 2 3] -> Ain=[3 2 1]
- ```sh
  public int[] invertirArray(int[] A){
  /** */
  //Procedimiento para invertir la matriz
  /** */
  return Ain;
  }
  ```
### SOLUCIÓN
- ```sh
  public int[] invertirArray(int[] A) {
      int n = A.length - 1;
      int[] Ain = new int[A.length];
  
      for (int i = 0; i <= n; i++) {
          Ain[i] = A[n - i];
      }
  
      return Ain;
  }
  ```

EJERCICIO 02. Rotación a la Izquierda
Ejemplo:
Si d=2
A=[1 2 3 4 5] -> Aiz=[3 4 5 1 2]
- ```sh
  public int[] rotarIzquierdaArray(int[] A){
  /** */
  //Procedimiento para rotar la matriz
  /** */
  return Aiz;
  }
  ```
### SOLUCIÓN
- ```sh
  public int[] rotarIzquierdaArray(int[] A) {
      int d = 2;
      int n = A.length;
      int[] Aiz = new int[n];
  
      for (int i = 0; i < n - d; i++) {
          Aiz[i] = A[i + d];
      }
  
      for (int i = 0; i < d; i++) {
          Aiz[n - d + i] = A[i];
      }
  
      return Aiz;
  }
  ```

EJERCICIO 03. Triángulo recursivo
Ejemplo:
b=5
- ```sh
  *
  **
  ***
  ****
  *****
  ```
- ```sh
  public void trianguloRecursivo(int base){
  /** */
  //Procedimiento para imprimir triángulo
  /** */
  }
  ```
### SOLUCIÓN
- ```sh
  public void trianguloRecursivo(int base) {
      if (base == 0) return;
  
      trianguloRecursivo(base - 1);
      for (int i = 0; i < base; i++) {
          System.out.print("*");
      }
      System.out.println();
  }
  ```

#

## CUESTIONARIO
¿Qué diferencia hay entre un List y un ArrayList en Java? ¿Qué beneficios y oportunidades ofrecen las clases genéricas en Java?
### Diferencias entre List y ArrayList
- **List**: interfaz que define operaciones para listas.
- **ArrayList**: implementación concreta de List basada en arrays dinámicos.

### Beneficios de las clases genéricas en Java
- Seguridad de tipos en tiempo de compilación.
- Reutilización de código para diferentes tipos.
- Código más limpio sin necesidad de casts.

#

## REFERENCIAS
- https://www.w3schools.com/java/
- https://www.eclipse.org/downloads/packages/release/2022-03/r/eclipse-ide-enterprise-java-and-web-developers
- https://docs.oracle.com/javase/7/docs/api/java/util/List.html
- https://docs.oracle.com/javase/tutorial/java/generics/types.html
