### Cliente:

| ID  | Estatura | Fecha_Nacimiento | Nombres | Apellidos |
| --- | -------- | ---------------- | ------- | --------- |
| 1   | 170      | 1990-05-15       | Juan    | Pérez     |
| 2   | 165      | 1985-12-28       | María   | García    |

### Correos_Clientes:

| Cliente_ID | Correo                  |
| ---------- | ----------------------- |
| 1          | juanperez@example.com   |
| 2          | mariagarcia@example.com |

### Cliente_Atrracion:

| ClienteAtraccion | Cliente_ID | Atraccion_ID |
| ---------------- | ---------- | ------------ |
| 1-201            | 1          | 201          |
| 2-202            | 2          | 202          |

### Brazalete:

| ID  | Clase    | Precio | Límite_Usos |
| --- | -------- | ------ | ----------- |
| 101 | Extremo  | 49400  | NULL        |
| 102 | Aventura | 37700  | 10          |
| 103 | Fusión   | 32500  | NULL        |

### Brazalete_Atraccion:

| BrazaleteAtraccion | Brazalete_ID | Atraccion_ID |
| ------------------ | ------------ | ------------ |
| 101-201            | 101          | 201          |
| 103-202            | 103          | 202          |

### Brazalete_Unidad:

| Brazalete_ID | Número | Valido_Hasta | Fecha_Usado | Cantidad_Usos | Cliente_ID |
| ------------ | ------ | ------------ | ----------- | ------------- | ---------- |
| 102          | 001    | 2024-06-30   | 2024-03-10  | 5             | 1          |
| 101          | 001    | 2024-08-15   | NULL        | 0             | 2          |

### Atracción:

| ID  | Estado            | Nombre      | Categoria | Precio_Uso | Precio_Compra | Altura_Min | Altura_Max | Edad_Min | Intensidad | Proveedor_ID | Operador_ID |
| --- | ----------------- | ----------- | --------- | ---------: | ------------: | ---------- | ---------- | -------- | ---------- | ------------ | ----------- |
| 201 | Funcionando       | Kamikaze    | Extremas  |      12000 |   120_000_000 | 160        | NULL       | 14       | Alta       | 301          | 501         |
| 202 | Fuera de servicio | Gas Station | Fantasía  |       5000 |    40_000_000 | 80         | 125        | NULL     | Baja       | 301          | 502         |

### Proveedor:

| ID  | Tipo          | Nombre                   | Correo                     |
| --- | ------------- | ------------------------ | -------------------------- |
| 301 | Nacional      | Diversión Extrema S.A.   | info@diversionextrema.com  |
| 302 | Internacional | Aventuras Globales Ltda. | info@aventurasglobales.com |

### Orden_Servicio:

| ID  | Fecha      | Duración_Dias | Estado    |  Precio | Atraccion_ID | Tecnico_ID |
| --- | ---------- | ------------- | --------- | ------: | ------------ | ---------- |
| 401 | 2024-03-20 | 3             | Completo  | 250_000 | 201          | 503        |
| 402 | 2024-04-22 | 2             | Pendiente | 150_000 | 202          | 504        |

### Operador:

| ID  | Nombre         | Correo                 | Sueldo    |
| --- | -------------- | ---------------------- | --------- |
| 501 | Pedro Martínez | pedrom@example.com     | 2_000_000 |
| 502 | Marta Pérez    | martaperez@example.com | 1_800_000 |

### Técnico:

| ID  | Nombre      | Correo                 | Especialidad |
| --- | ----------- | ---------------------- | ------------ |
| 503 | Ana López   | analopez@example.com   | Mecánica     |
| 504 | Luis García | luisgarcia@example.com | Electricidad |
