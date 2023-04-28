# XQUERY

# libros.xml
## 1- Títulos ordenados

```
for $x in doc("libros.xml")/libros/libro
return $x/titulo
```
## 2- Títulos ordenados por el nombre del primer autor

```
for $x in doc("libros.xml")/libros/libro
let $i := $x/autores/autor[1]
order by $i/nombre
return $x/titulo
```
## 3- Nombre y apellido del primer autor de cada libro

```
for $x in doc("libros.xml")/libros/libro
return $x/autores/autor[1]/concat(nombre, ' ',apellido)
```

## 4- Título y número de autores de cada libro

```
for $x in doc("libros.xml")/libros/libro
return $x/concat(titulo, "  Autores: ", autores/count(autor))
```

## 5- Libros que tienen varios autores y libros que tienen un autor

```
for $x in doc("libros.xml")/libros/libro
return if ($x/autores/count(autor)>1)
then ($x/concat("Libros con varios autor: ", titulo))
else ($x/concat("Libros con un único autor: ", titulo))
```

## 6- Libros cuyo autor es “Axel”

```
for $x in doc("libros.xml")/libros/libro
where $x/autores/autor/nombre = ("Axel")
return $x/concat("Libros escritos por Axel: ",titulo)
```

## 7- Mostrar título y precio en una lista HTML

```
<ul>
{
for $x in doc("libros.xml")/libros/libro
return <li>{$x/concat(titulo, " ", precio, " €")}</li>
}
</ul>
```

## 8- Mostrar: título, isbn y precio en una tabla HTML

```
<table>
<tr>
<th> Titulo </th>
<th> ISBN </th>
<th> Precio </th>
</tr>
{
for $x in doc("libros.xml")/libros/libro
return
<tbody>
<tr>
<td>{$x/titulo}</td>
<td>{$x/isbn}</td>
<td>{$x/concat(precio, " €")}</td>
</tr>
</tbody>
}
</table>
```
# alumnos.xml

## 1- Mostrar el nombre de los alumnos aprobados

```
for $x in doc ("alumnos.xml")/alumnos/alumno
where $x/nota>4
return $x/nombre
```

## 2- Mostrar el DNI y la nota de los alumnos que han aprobado

```
for $x in doc ("alumnos.xml")/alumnos/alumno
where $x/nota>4
return data($x/concat("Alumno aprobado: ", @dni, " ", nota))
```

## 3- Indicar el nombre de los alumnos cuyas notas están entre 6 y 8 (ambas inclusive)

```
for $x in doc ("alumnos.xml")/alumnos/alumno
where $x/nota>=6 and $x/nota<=8
return data($x/nombre)
```

## 4- Mostrar listado de nombres ordenados por apellidos

```
for $x in doc ("alumnos.xml")/alumnos/alumno
let $i := $x/apells
order by $i
return $i
```

## 5- Mostrar nombres ordenados por DNI

```
for $x in doc ("alumnos.xml")/alumnos/alumno
let $i := $x/@dni
order by $i
return data($x/nombre)
```

## 6- Mostrar el Nº de cada alumno y su nombre

```
for $x at $i in doc ("alumnos.xml")/alumnos/alumno
return concat($i, " ", $x/nombre)
```