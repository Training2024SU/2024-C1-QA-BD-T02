# Solución taller #2 MR Parque Norte

## 1. Verificar el modelo entidad relación realizado en la actividad anterior.

Actualizo el modelo entidad relación para volverlo extendido y documentarlo para consulta de personal no técnico.

![Parque MERE](./Parque_MERE.png)

### Entidades y sus atributos

1. **Cliente**
   - ID (Llave)
   - Estatura
   - Fecha_Nacimiento
   - Edad (Derivado)
   - Nombre_Completo (Compuesto de: Nombres, Apellidos)
   - Correo (multivaluado)
2. **Brazalete**
   - ID (Llave)
   - Clase
   - Precio
   - Límite_Usos (Nullable)
3. **Brazalete_Unidad (Entidad Debil sin ID y dependiente de Brazalete)**
   - Número (Discriminador)
   - Valido_Hasta
   - Fecha_Usado
   - Cantidad_Usos (Default: 0)
4. **Atracción**
   - ID (Llave)
   - Nombre
   - Estado
   - Categoria
   - Precio_Uso
   - Precio_Compra
   - Altura_Min (Nullable)
   - Altura_Max (Nullable)
   - Edad_Min (Nullable)
   - Intensidad
5. **Proveedor**
   - ID (Llave)
   - Tipo
   - Nombre
   - Correo
6. **Orden_Servicio**
   - ID (Llave)
   - Fecha
   - Duración
   - Estado
   - Precio
7. **Empleado (SuperEntidad Disyuntiva)**
   - ID (Llave)
   - Nombre
   - Correo
8. **Operador (SubEntidad de Empleado)**
   - Sueldo
9. **Técnico (SubEntidad de Empleado)**
   - Especialidad

### Relaciones, cardinalidad y participación

#### Muchos a Muchos

- Un cliente puede **usar muchas** atracciones y una atracción puede **ser utilizada por muchos** clientes. Los clientes pueden **no usar** las atracciones y una atracción nueva puede **no haber sido usada** aún por clientes.
- Un brazalete puede **incluir muchas** atracciones y una atracción puede **estar incluida en varios** brazaletes. Un brazalete **debe incluir** atracciones, sin embargo una atracción **no necesita estar incluida** en un brazalete.

#### Uno a Muchos

- Un cliente puede **comprar muchas** unidades de brazalete, pero una unidad de brazalete puede **ser comprada por solo un** cliente. Los clientes pueden **no comprar** unidades de brazaletes y una unidad de brazalete **tiene que ser comprado por un** cliente.
- Un brazalete puede **generar muchas** unidades y una unidad puede **ser generada de solo un** brazalete. Un brazalete **debe tener** unidades, y las unidades **tienen que ser generadas de un** brazalete. Esta es una relación identificadora lo que significa que la llave primaria se compone del ID del brazalete y el discriminador Número de la unidad
- Un proveedor puede **vender muchas** atracciones y una atracción puede **ser vendida por solo un** proveedor. Un proveedor **debe haber vendido una** atracción y una atracción puede **no haber sido vendida** por un proveedor.
- Una atracción puede **ser reparada con muchas** ordenes de servicio y una orden de servicio **solo puede ser para reparar una** atracción. Una atracción no necesita tener una orden de servicio, mientras que una orden de servicio **debe ser para reparar una** atracción.
- Un tecnico puede **completar muchas** ordenes de servicio y una orden de servicio puede **ser completada por solo un** técnico. Un técnico **debe haber completado una** orden de servicio, mientras que una orden puede **no ser completada por un** técnico (suponiendo que se cancele la orden, o no hay técnicos disponibles).

#### Uno a Uno

- Un operador puede **operar solo una** atracción y una atracción puede **ser operada por solo un** operador. Un operador **tiene que operar una** atracción, mientras que una atracción puede **no ser operada por un** operador.

## 2. Transformar el modelo E-R en un M-R.

- Transformé todas las entidades en tablas con sus atributos, exceptuando los derivados y multivaluados. Para la super entidad Empleado, como su generalización es total con disyunción, solo tuve que crear las tablas de las subentidades Técnico y Operador, cada una incluyendo todos los atributos de la superclase.
- Creé las tablas intermedias de las relaciones muchos a muchos, las cuales tienen como llave primaria la concatenación de las llaves primarias de las entidades relacionadas.
  - Cliente-Atraccion
  - Brazalete-Atraccion
- Para las relaciones uno a muchos, la _entidad de muchos_ le agregué como atributo la llave primaria de la _entidad de uno_ con la que se relaciona
  - Unidad_Brazalete-Cliente
  - Unidad_Brazalete-Brazalete
  - Atraccion-Proveedor
  - Orden_Servicio-Atraccion
  - Orden_Servicio-Tecnico
- Para la relación uno a uno analicé la participación, como el operador tiene una participación total en la relación su llave primaria pasa como atributo a la tabla de Atracciónes y no es necesario una tabla intermedia.
  - Atraccion-Operador

## 3. Normalizar el modelo.

Al revisar el modelo en el punto 1 del taller cambié la entidad Brazalete separando los atributos específicos de cada unidad de brazalete a una nueva entidad llamada Unidad_Brazalete. Además de esta forma optimizo la relacion entre los brazaletes y las atracciones que incluye cada una de las unidades. Ahora en lugar de tener registradas todas las atracciones incluidas por cada unidad de brazalete, esta relación se especifica solo entre los tipos de brazalete y las atracciones.

### Un esquema relacional R está en 1NF si:

- [x] Todos los atributos tienen valores atómicos.
- [x] No hay atributos multivaluados.
- [x] No deben existir registros duplicados.
- [x] Las columnas repetidas deben eliminarse y colocarse agrupadas en tablas separadas bajo un contexto.
- [x] Definir clave principal.

### Un esquema relacional R está en 2NF si:

- [x] Estar en 1FN
- [x] Todos los valores de las columnas deben depender únicamente de la llave primaria de la tabla.
- [x] Las tablas deben tener una única llave primaria que identifique a la tabla y que sus atributos dependen de ella.

### Un esquema relacional R está en 3NF si:

- [x] Estar en 2FN.
- [x] Cada atributo que no está incluido en la clave primaria no depende transitivamente de la clave primaria

#### Otras posibles transofrmaciones sugeribles según los últimos niveles de normalización puede ser separar los siguientes atributos en otras tablas:

- (Atraccion) Estado
- (Atraccion) Categoría
- (Atraccion) Intensidad
- (Orden_Servicio) Estado
- (Tecnico) Especialidad
- (Proveedor) Tipo
