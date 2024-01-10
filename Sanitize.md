# Sanitización
El equipo de Sanity, recomienda instalar el siguiente paquete: ``` npm i @portabletext/react ```.

Este paquete nos sirve para poder sanitizar todo el contenido que este almacenado en el CDN de Sanity, y al pasar los datos por la API, desde nuestra aplicacion tenemos que sanitizar los datos.

### Modo de Uso:
Supongamos que ya tenemos las entradas listas en nuestro Blog, creadas desde la Api de sanity port:3333.
Y ya tenemos nuestros archivos configurados, libs, interfaces, etc.
Para implementar este paquete solo tenemos que importar el componente ```<PortableText value={~~~.content}/>```, y pasarle el atributo de value, y en este mismo, pasar la variable de data, la cual contiene toda la informacion desde el backend por medio de la querie.

``` typescript
import { fullBlog } from "@/app/lib/interface";
import { client, urlFor } from "@/app/lib/sanity";
import { PortableText } from "@portabletext/react";
import Image from "next/image";

async function getData(slug: string){
    const query = `
    *[_type == "blog" && slug.current == '${slug}'] {
        "currentSlug": slug.current,
        title,
        content,
        titleImage
    }[0]`;
    const data = await client.fetch(query);
    return data;
}

export default async function BlogArticle({params}: { params: {slug: string} }) {
    const data: fullBlog = await getData(params.slug);
    return(
        <div className="mt-8 flex flex-col justify-center items-center">
            <h1>
                <span className="block text-base text-primary text-center font-semibold tracking-wide uppercase">RamaDEV - Blog</span>
                <span className="mt-2 block text-3xl text-center leading-8 font-bold tracking-tight sm:text-4xl">{data.title}</span>
            </h1>
            <Image
                src={urlFor(data.titleImage).url()}
                alt="image"
                width={500} height={500}
                priority
                className="rounded-lg mt-5 border"
            />

            <div className='mt-16'>
                <PortableText value={data.content}/>
            </div>
        </div>
    )
}
```
En este ejemplo, el componente se vera asi: ```<PortableText value={data.content}/>``` ya que esta variable contiene los datos desde la funcion asincrona, y no cualquier dato, sino los datos del respectivo **SLUG** del posteo.