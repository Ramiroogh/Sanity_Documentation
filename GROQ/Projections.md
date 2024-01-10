# Projections
Las projections en **GROQ**, es una sintaxis que se incluye en las queries, esto se ve reflejado con llaves { }.

```*[_type == 'movie' && releaseYear >= 1979]{ _id, title, releaseYear } ```

## Brandwith
Con esta sintaxis, estamos recolectando en las queries, los datos que realmente nos interesa, de esta manera no sobrecargamos el ancho de banda, y mejoramos el performance de nuestra apicacion.
