# Modelo entidad relación. Viveros

## 1. Entidades

En este apartado se explican las entidades que hemos utilizado para representar la información del sistema de viveros.

### Vivero

La entidad `Vivero` representa cada uno de los viveros que tenemos en el sistema.

**Atributos:**

* `id_vivero`: identificador del vivero.
* `nombre`: nombre del vivero.
* `latitud`: latitud donde se encuentra el vivero.
* `longitud`: longitud donde se encuentra el vivero.

**Ejemplo:**

```text
id_vivero: 1
nombre: Vivero La Laguna
latitud: 28.4874
longitud: -16.3159
```

### Zona

La entidad `Zona` representa las diferentes zonas que puede tener un vivero. Por ejemplo, una zona de cultivo o una zona de almacén. Se trata de una entidad débil dependiente de `Vivero`.

**Atributos:**

* `num_zona`: número que identifica la zona, es un atributo discriminante.
* `nombre`: nombre de la zona.
* `tipo`: tipo de zona.
* `latitud`: latitud de la zona.
* `longitud`: longitud de la zona.

**Ejemplo:**

```text
num_zona: 3
nombre: Zona de cultivo 3
tipo: Cultivo
latitud: 28.4875
longitud: -16.3158
```

### Producto

La entidad `Producto` representa los diferentes productos que se pueden encontrar en el vivero.

**Atributos:**

* `id_producto`: identificador del producto.
* `nombre`: nombre del producto.
* `precio`: precio del producto.
* `categoría`: categoría a la que pertenece.

**Ejemplo:**

```text
id_producto: 25
nombre: Planta de tomate
precio: 4.50
categoría: Hortaliza
```

### Puesto

La entidad `Puesto` representa los diferentes puestos de trabajo que pueden existir en el vivero.

**Atributos:**

* `id_puesto`: identificador del puesto.
* `nombre`: nombre del puesto.

**Ejemplo:**

```text
id_puesto: 4
nombre: Encargado de almacén
```

### Empleado

La entidad `Empleado` representa a las personas que trabajan en los viveros.

**Atributos:**

* `id_empleado`: identificador del empleado.
* `nombre`: nombre del empleado.

**Ejemplo:**

```text
id_empleado: 103
nombre: Juan Pérez
```

### Registro_productividad

La entidad `Registro_productividad` sirve para guardar los datos de productividad de una zona en una fecha determinada.

**Atributos:**

* `fecha`: día en el que se realiza el registro.
* `productividad`: valor de productividad registrado.

**Ejemplo:**

```text
fecha: 01/10/2026
productividad: 87.5
```

### Cliente

La entidad `Cliente` representa a las personas que pueden realizar pedidos en el sistema.

**Atributos:**

* `id_cliente`: identificador del cliente.
* `nombre`: nombre del cliente.
* `teléfono`: teléfono del cliente.

**Ejemplo:**

```text
id_cliente: 501
nombre: María García
teléfono: 600123456
```

### Cliente_plus

`Cliente_plus` representa a los clientes que pertenecen al programa de fidelización Tajinaste Plus. Se trata de una especialización exclusiva y parcial de la entidad `Cliente`. 

**Atributos:**

* `fecha_alta`: fecha en la que el cliente pasa a ser Cliente_plus.

**Ejemplo:**

```text
fecha_alta: 15/09/2026
```

### Pedido

La entidad `Pedido` representa los pedidos realizados por los clientes.

**Atributos:**

* `id_pedido`: identificador del pedido.
* `fecha`: fecha en la que se realiza.
* `importe`: importe total del pedido.

**Ejemplo:**

```text
id_pedido: 10025
fecha: 02/10/2026
importe: 125.75
```

---

## 2. Dominio de los atributos

El dominio indica qué tipo de valores puede tener cada atributo.

| Entidad                | Atributo        | Dominio         | Ejemplo              |
| ---------------------- | --------------- | --------------- | -------------------- |
| Vivero                 | `id_vivero`     | Entero positivo | `1`                  |
| Vivero                 | `nombre`        | Cadena de texto | `"Vivero La Laguna"` |
| Vivero                 | `latitud`       | Número real     | `28.4874`            |
| Vivero                 | `longitud`      | Número real     | `-16.3159`           |
| Zona                   | `num_zona`      | Entero positivo | `3`                  |
| Zona                   | `nombre`        | Cadena de texto | `"Zona de cultivo"`  |
| Zona                   | `tipo`          | Cadena de texto | `"Cultivo"`          |
| Zona                   | `latitud`       | Número real     | `28.4875`            |
| Zona                   | `longitud`      | Número real     | `-16.3158`           |
| Producto               | `id_producto`   | Entero positivo | `25`                 |
| Producto               | `nombre`        | Cadena de texto | `"Planta de tomate"` |
| Producto               | `precio`        | Número real     | `4.50`               |
| Producto               | `categoría`     | Cadena de texto | `"Hortaliza"`        |
| Puesto                 | `id_puesto`     | Entero positivo | `4`                  |
| Puesto                 | `nombre`        | Cadena de texto | `"Encargado"`        |
| Empleado               | `id_empleado`   | Entero positivo | `103`                |
| Empleado               | `nombre`        | Cadena de texto | `"Juan Pérez"`       |
| Registro_productividad | `fecha`         | Fecha           | `01/10/2026`         |
| Registro_productividad | `productividad` | Número real     | `87.5`               |
| Cliente                | `id_cliente`    | Entero positivo | `501`                |
| Cliente                | `nombre`        | Cadena de texto | `"María García"`     |
| Cliente                | `teléfono`      | Cadena de texto | `"600123456"`        |
| Cliente_plus           | `fecha_alta`    | Fecha           | `15/09/2026`         |
| Pedido                 | `id_pedido`     | Entero positivo | `10025`              |
| Pedido                 | `fecha`         | Fecha           | `02/10/2026`         |
| Pedido                 | `importe`       | Número real     | `125.75`             |

También tenemos algunos atributos que pertenecen a las relaciones:

* `cantidad`: número de unidades de un producto almacenadas en una zona.
* `tarea`: tarea que realiza un empleado.
* `productividad`: productividad de empleado.
* `fecha_inicio`: fecha en la que empieza una relación.
* `fecha_fin`: fecha en la que termina una relación.

---

## 3. Relaciones

### Contiene

Relaciona un `Vivero` con las `Zona` que tiene.

La relación es **N:1**:

* Un vivero puede tener una o varias zonas.
* Una zona pertenece a un único vivero.

Por ejemplo, el `Vivero La Laguna` puede tener las zonas 1, 2, 3 y 4, pero la zona 3 solo puede pertenecer a ese vivero.

**Cardinalidad:**

```text
Vivero (1,1) ---- Contiene ---- (1,N) Zona
```

Además, se trata de una dependencia en identificación ya que la entidad debil `Zona` requiere de `Vivero` para identificarse.

### Almacena

Relaciona las zonas con los productos que tienen almacenados.

Es una relación **N:M**:

* Una zona puede almacenar diferentes productos.
* Un producto puede estar almacenado en diferentes zonas.

Esta relación tiene además el atributo `cantidad`, ya que necesitamos saber cuántas unidades de cada producto hay en cada zona.

Por ejemplo, la zona 3 puede tener 50 plantas de tomate y 20 plantas de pimiento.

**Cardinalidad:**

```text
Zona (1,N) ---- Almacena ---- (1,N) Producto
```

### Trabaja

Relaciona a los empleados con las zonas en las que trabajan.

Es una relación **N:M**:

* Un empleado puede trabajar en varias zonas a lo largo del tiempo.
* Una zona puede tener varios empleados o ninguno.

Además, la relación contiene información como la tarea que realiza el empleado, su productividad y las fechas en las que trabaja en esa zona.

**Cardinalidad:**

```text
Empleado (0,N) ---- Trabaja ---- (1,N) Zona
```

### Destinado

Indica en qué vivero está destinado un empleado.

Es una relación **N:M**:

* Un empleado puede estar destinado a diferentes vivero a lo largo del tiempo.
* Un vivero puede tener diferentes empleados destinados o ninguno.

La relación tiene `fecha_inicio` y `fecha_fin` para saber durante qué periodo estuvo destinado el empleado.

**Cardinalidad:**

```text
Empleado (0,N) ---- Destinado ---- (1,N) Vivero
```

### Ocupa

Relaciona a los empleados con los puestos que ocupan.

Es una relación **N:M**:

* Un empleado puede ocupar diferentes puestos a lo largo del tiempo.
* Un puesto puede ser ocupado por diferentes empleados o por ninguno.

Las fechas permiten saber durante qué periodo ocupó el empleado ese puesto.

**Cardinalidad:**

```text
Empleado (0,N) ---- Ocupa ---- (1,N) Puesto
```

### Registra

Relaciona una zona con sus registros de productividad.

Es una relación **1:N**:

* Una zona puede tener varios registros de productividad.
* Cada registro de productividad pertenece a una única zona.

Por ejemplo, podemos tener un registro de productividad diferente para cada día.

**Cardinalidad:**

```text
Zona (1,1) ---- Registra ---- (1,N) Registro_productividad
```

### Realiza

Relaciona a los clientes con los pedidos que realizan.

Es una relación **1:N**:

* Un cliente puede realizar ningún pedido o varios.
* Cada pedido pertenece a un único cliente.

**Cardinalidad:**

```text
Cliente (1,1) ---- Realiza ---- (0,N) Pedido
```

Por ejemplo, un cliente puede registrarse en el sistema y todavía no haber realizado ningún pedido.

### Gestiona

Relaciona a los empleados con los pedidos que gestionan.

Es una relación **1:N**:

* Un empleado puede gestionar varios pedidos o ninguno.
* Cada pedido es gestionado por un único empleado.

**Cardinalidad:**

```text
Empleado (1,1) ---- Gestiona ---- (0,N) Pedido
```

---

## 4. Restricciones semánticas

Además de las cardinalidades que aparecen en el modelo, hemos considerado algunas restricciones para que los datos tengan sentido:


* El `precio` de un producto no puede ser negativo.
* El `importe` de un pedido tampoco puede ser negativo.
* La `cantidad` de productos almacenados debe ser positiva.
* Si una relación tiene `fecha_inicio` y `fecha_fin`, la fecha de fin no puede ser anterior a la fecha de inicio.
* No debería haber dos registros de productividad para la misma zona y la misma fecha.
* Un empleado no puede estar destinado a dos viveros simultáneamente durante el mismo periodo.
* Un empleado solo puede trabajar en una zona perteneciente al vivero al que está destinado durante ese periodo.

Estas restricciones sirven para evitar datos que no tendrían sentido dentro del sistema y para mantener la información coherente.
