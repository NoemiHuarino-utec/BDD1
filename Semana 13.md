# SPARQLing Alumni
Laboratorio 13_1

### P3
 La lista de directores de cine educados en universidades peruanas. Retorne el nombre
del director y de la universidad.

```ruby
SELECT ?unom ?pnom  WHERE {
  ?uni wdt:P31 wd:Q3918.
  ?uni rdfs:label ?unom.
  ?uni wdt:P17 wd:Q419.
  ?person wdt:P69 ?uni.
  ?person rdfs:label ?pnom.
  ?person wdt:P106 wd:Q2526255.
  FILTER((LANG(?unom)) = "es")
}
```

### P4
La lista de las pel ıculas de dichos directores. Retorne el nombre de la película, del
director y de la universidad.

```ruby
SELECT ?unom ?pnom ?pelicula_nom WHERE {
  ?uni wdt:P31 wd:Q3918.
  ?uni rdfs:label ?unom.
  ?uni wdt:P17 wd:Q419.
  ?person wdt:P69 ?uni.
  ?person rdfs:label ?pnom.
  ?person wdt:P106 wd:Q2526255.
  ?peliculas wdt:P57 ?person.
  ?peliculas rdfs:label ?pelicula_nom.
  
  FILTER((LANG(?unom)) = "es")
  FILTER((LANG(?pnom)) = "es")
  FILTER((LANG(?pelicula_nom)) = "es")

}
ORDER BY ASC (?pelicula_nom)
```

### P5 
La lista anterior, pero ordenada por la fecha de estreno de la pel ́ıcula, partiendo con la
más reciente. Retorne el nombre de la película, del director, de la universidad y la fecha de
estreno.

```ruby
SELECT ?pnom ?unom ?movie_nom ?fecha_estreno WHERE {
  ?uni wdt:P31 wd:Q3918.
  ?uni rdfs:label ?unom.
  ?uni wdt:P17 wd:Q419.
  ?person wdt:P69 ?uni.
  ?person rdfs:label ?pnom.
  
  ?person wdt:P106 wd:Q2526255 .
  ?movie wdt:P57 ?person .
  ?movie rdfs:label ?movie_nom.
  ?movie wdt:P577 ?fecha_estreno
  
  FILTER((LANG(?pnom)) = "es")
  FILTER((LANG(?unom)) = "es")
  FILTER((LANG(?movie_nom)) = "es")

}
```

### P6
Para cada universidad, cuente el número de pel ́ıculas dirigidas por sus alumnos. Ordene la lista por número de películas.

```ruby

```

### P7
Encuentre la causa de muerte m ́as com ́un para las personas educadas en universidades
peruanas. Retorne el nombre de la causa de muerte y la cuenta. Ordene convenientemente.
Podemos ver que, si sabemos algo de SPARQL, Wikidata nos permite responder consultas
muy espec ́ıficas, las que ser ́ıa horrible responder manualmente. El  ́unico problema es la
incompletitud: mientras un modelo basado en grafos nos permite modelar datos diversos e
incompletos de forma f ́acil, es dificil saber cu ́ando estamos obteniendo todos los resultados
deseados. Sin embargo, podemos obtener r ́apidamente al menos algunos resultados y, a
medida que Wikidata est ́a siendo editada cada vez m ́as por m ́as y m ́as usuarios, podemos
esperar que la completitud aumente.


```ruby
SELECT ?causa_muerte (COUNT(?causas_muertes) AS ?num_muertes_por_causa) WHERE {
  ?uni wdt:P31 wd:Q3918.
  ?uni rdfs:label ?unom.
  ?uni wdt:P17 wd:Q419.
  ?person wdt:P69 ?uni.
  ?person rdfs:label ?pnom.
  ?person wdt:P509 ?causas_muertes.
  ?causas_muertes rdfs:label ?causa_muerte.
  
  FILTER((LANG(?pnom)) = "es")
  FILTER((LANG(?unom)) = "es")
  FILTER((LANG(?causa_muerte)) = "es")
 

}
                      
GROUP BY (?causa_muerte)
GROUP BY (?num_muertes_por_causa)   
```

👀: **No correr los dos "GROUP BY" al mismo tiempo.**

## Tarea extra y voluntaria
Se habilitará en Canvas hasta la **semana 16** y es **+1** punto en la nota final de la Evaluación Continua I del curso.
