# Sobre el curso de capacitación

**Nombre**: Next.js: El framework de React para producción

**Link**: <https://www.udemy.com/course/nextjs-fh>

***

## Índice

- [Sobre el curso de capacitación](#sobre-el-curso-de-capacitación)
  - [Índice](#índice)
  - [SSR en general](#ssr-en-general)
    - [¿Por qué usaría Next.js y SSR?:](#por-qué-usaría-nextjs-y-ssr)
    - [PROs vs CONs](#pros-vs-cons)
      - [PROs](#pros)
      - [CONs](#cons)
  - [Sesiones y anotaciones respectivas](#sesiones-y-anotaciones-respectivas)
    - [28. Archivos de JavaScript a TypeScript](#28-archivos-de-javascript-a-typescript)
      - [Problema resueltos](#problema-resueltos)
      - [Aprendido](#aprendido)
    - [29. Migrando _app.jsx a _app.tsx](#29-migrando-_appjsx-a-_apptsx)
    - [49. Mostrar tarjetas de Pokémons](#49-mostrar-tarjetas-de-pokémons)
      - [Problemas resueltos](#problemas-resueltos)
    - [64. Leer y verificar si existe en favoritos](#64-leer-y-verificar-si-existe-en-favoritos)
      - [Problemas resueltos](#problemas-resueltos-1)
    - [71. Optimizar la data necesaria del pokémon](#71-optimizar-la-data-necesaria-del-pokémon)
      - [Problemas resueltos](#problemas-resueltos-2)
      - [Aprendido](#aprendido-1)

***

## SSR en general

### ¿Por qué usaría Next.js y SSR?:

- Mostly SEO. This is 95% of why people do it, I'm guessing.

- It can make initial page load feel faster for lower powered or low bandwidth devices since they directly receive the HTML content of the page instead of having to load many JavaScript bundles (including React, itself) and then spend CPU cycles parsing that JavaScript and executing it all before they see the UI of the page.

- It makes a website usable even with JavaScript disabled

[Fuente: Reddit](https://www.reddit.com/r/nextjs/comments/qzo72r/comment/hlnfbw3/?utm_source=share&utm_medium=web2x&context=3)

### PROs vs CONs

#### PROs

- The content is immediately available. That's going to make it look great on slow connections.

- You're not required to make any additional API calls from the client.

- Ideal for SEO. The search engine doesn't need to execute the JS in order to see what's on the page.

#### CONs

- Slower for the server. Basically, we're rendering the app twice: once for the client and once for the server.

- Some UI frameworks can be incompatible with SSR because they are looking for the window element which is not available in the node context.

[Fuente: Reddit](https://www.reddit.com/r/nextjs/comments/qzo72r/comment/hlrfukn/?utm_source=share&utm_medium=web2x&context=3)

## Sesiones y anotaciones respectivas

### 28. Archivos de JavaScript a TypeScript

El instructor está enseñando cómo realizar los cambios en objetos y props de JavaScript a TypeScript, usando strictmode (`"strict": true`).

#### Problema resueltos

1. `tsconfig.json` que fue generado automáticamente le faltó en `"compilerOptions"` la propiedad:

    ````json
    "moduleResolution": "node"
    ````

2. El video del curso se desarrolló con React v17 y ahora estamos en React v18.

    Hay un setting que se rompe porque los defaults cambian.
    La solución consiste en cambiar esto:

````ts
import { FC } from "react";

type Props = {};

export const DarkLayout: FC = ({ children }) => {
  return (
    <div
      style={{
        backgroundColor: "rgba(0,0,0,0.3)",
        borderRadius: "5px",
        padding: "10px",
      }}
    >
      <h3>Dark-Layout</h3>
      <div>{children}</div>
    </div>
  );
};

````

a esto:

````ts
import { FC, PropsWithChildren } from "react";

type Props = {};

export const DarkLayout: FC<PropsWithChildren<Props>> = ({ children }) => {
  return (
    <div
      style={{
        backgroundColor: "rgba(0,0,0,0.3)",
        borderRadius: "5px",
        padding: "10px",
      }}
    >
      <h3>Dark-Layout</h3>
      <div>{children}</div>
    </div>
  );
};

````

#### Aprendido

Instructor agrega `interface` pero parece funcionar de la misma manera utilizando `type`:

**Instructor**:

````ts
interface Props {
  text: string;
  href: string;
};
````

**Yo**:

````ts
type Props = {
  text: string;
  href: string;
};
````

Al parecer es más seguro usar `interface` porque se puede expandir y continuar elaborándolo. En cambio, `type` se define una sola vez.

Artículos que explican la diferencia:

<https://medium.com/@martin_hotell/interface-vs-type-alias-in-typescript-2-7-2a8f1777af4c>

<https://www.pluralsight.com/guides/defining-props-in-react-function-component-with-typescript>

### 29. Migrando _app.jsx a _app.tsx

Para investigar luego:

````ts
type NextPageWithLayout = NextPage & {
  getLayout?: (page: JSX.Element) => JSX.Element;
};
````

**Por qué usa signos de interrogación?**
Respuesta: declarar atributo opcional.

Documento que lo explica: <https://www.pluralsight.com/guides/defining-props-in-react-function-component-with-typescript>

### 49. Mostrar tarjetas de Pokémons

#### Problemas resueltos

1. El instructor utiliza parámetros de props para el componente `Card` que han sido actualizados desde la grabación del video.

Antes:

````ts
<Card hoverable clicable>
</Card>
````

Después:

````ts
<Card isHoverable isPressable>
</Card>
````

### 64. Leer y verificar si existe en favoritos

#### Problemas resueltos

El instructor utiliza un estado inicializado con comandos ejecutados que según ciertas circunstancias (de velocidad de carga del servidor?) no siempre pueden ejecutarse correctamente.

````ts
 const [isInFavorites, setIsInFavorites] = useState(localFavorites.existInFavorites(pokemon.id));
````

Esto genera un error con la carga del localStorage con `existInFavorites`. Luego, la solución que él propone utilizando:

````ts
if (typeof window === 'undefined') return false;
````

no es la mejor según procedimientos recomendados por la documentación de Next.js.

Se encontró una mejor alternativa utilizando useEffect. De esta manera la página puede iniciar correctamente sin tener que esperar a que la info esté lista.

**Antes:**

````ts
  const [isInFavorites, setIsInFavorites] = useState(localFavorites.existInFavorites(pokemon.id));
````

**Después:**

````ts
  const [isInFavorites, setIsInFavorites] = useState(false);

  useEffect(() => {
    setIsInFavorites(localFavorites.existInFavorites(pokemon.id))
  }, [pokemon.id]) 
````

### 71. Optimizar la data necesaria del pokémon

#### Problemas resueltos

Observamos que la navegación de la página durante el dev y el build era bastante lenta. Luego de completar este video se aprendió que la lentitud era debido al tamaño de los archivos cargados (cada JSON pesaba >200KiB).

#### Aprendido

Se reveló que optimizando la cantidad de data que se pide al API puede reducir drásticamente el tamaño del build del server y por ende mejora también el rendimiento cuando se navega en el site.

Comparando tamaño del build,

| Antes | Después |
|-|-|
|![build size before](src/pokemon-build-size-before.png)|![build size after](src/pokemon-build-size-after.png)

Inicialmente el website solicitaba el objeto entero de cada Pokémon a través del API en `getStaticProps`:

````ts
export const getStaticProps: GetStaticProps = async ({ params }) => {
  const { id } = params as { id: string };
  const { data } = await pokeApi.get<Pokemon>(`/pokemon/${id}`);

  return {
    props: {
      pokemon: data,
    },
  };
};
````

Sin embargo, se puede elegir no pasar a Static Props las propiedad innecesarias:

````ts
export const getStaticProps: GetStaticProps = async ({ params }) => {
  const { id } = params as { id: string };

  return {
    props: {
      pokemon: await getPokemonInfo( id ),
    },
  };
};
````

````ts
import pokeApi from "../api/pokeApi";
import { Pokemon } from "../interfaces";

export const getPokemonInfo = async (nameOrId: string) => {
  const { data } = await pokeApi.get<Pokemon>(`/pokemon/${nameOrId}`);

  return {
    id: data.id,
    name: data.name,
    sprites: {
      front_default: data.sprites.front_default,
      back_default: data.sprites.back_default,
      front_shiny: data.sprites.front_shiny,
      back_shiny: data.sprites.back_shiny,
      other: {
        dream_world: {
          front_default: data.sprites.other?.dream_world.front_default,
        },
      },
    },
  };
};

````

Aquí solamente se pasa a través de `getStaticProps` las propiedades del JSON que se utilizarán.

En cuando al tiempo que se demoró en generar el build, fue aproximadamente lo mismo:

**Antes**:

````txt
Page                                       Size     First Load JS
┌ ● / (646 ms)                             1.56 kB         142 kB
├   /_app                                  0 B             115 kB
├ ○ /404                                   186 B           115 kB
├ ○ /favorites (860 ms)                    1.92 kB         143 kB
├ ● /name/[name] (58346 ms)                1.58 kB         151 kB
├   ├ /name/charmeleon (559 ms)
├   ├ /name/squirtle (552 ms)
├   ├ /name/charizard (551 ms)
├   ├ /name/golbat (516 ms)
├   ├ /name/nidoqueen (513 ms)
├   ├ /name/nidoran-m (506 ms)
├   ├ /name/jigglypuff (504 ms)
├   └ [+144 more paths] (avg 379 ms)
└ ● /pokemon/[id] (78177 ms)               1.58 kB         151 kB
    ├ /pokemon/95 (1132 ms)
    ├ /pokemon/96 (1118 ms)
    ├ /pokemon/99 (1053 ms)
    ├ /pokemon/97 (1043 ms)
    ├ /pokemon/94 (1035 ms)
    ├ /pokemon/93 (817 ms)
    ├ /pokemon/101 (816 ms)
    └ [+144 more paths] (avg 494 ms)
+ First Load JS shared by all              115 kB
  ├ chunks/framework-9b5d6ec4444c80fa.js   45.7 kB
  ├ chunks/main-f0e16f48d3775e5e.js        30.7 kB
  ├ chunks/pages/_app-e41591127e174d14.js  38.1 kB
  ├ chunks/webpack-7ee66019f7f6d30f.js     755 B
  └ css/ef46db3751d8e999.css               20 B

○  (Static)  automatically rendered as static HTML (uses no initial props)
●  (SSG)     automatically generated as static HTML + JSON (uses getStaticProps)

Done in 33.74s.
````

**Después**:

````txt
Page                                       Size     First Load JS
┌ ● / (2591 ms)                            1.56 kB         142 kB
├   /_app                                  0 B             115 kB
├ ○ /404                                   186 B           115 kB
├ ○ /favorites (800 ms)                    1.92 kB         143 kB
├ ● /name/[name] (56555 ms)                1.58 kB         151 kB
├   ├ /name/persian (1130 ms)
├   ├ /name/alakazam (1019 ms)
├   ├ /name/poliwrath (958 ms)
├   ├ /name/kadabra (914 ms)
├   ├ /name/golduck (794 ms)
├   ├ /name/machop (742 ms)
├   ├ /name/machoke (707 ms)
├   └ [+144 more paths] (avg 349 ms)
└ ● /pokemon/[id] (80483 ms)               1.58 kB         151 kB
    ├ /pokemon/3 (16558 ms)
    ├ /pokemon/4 (6381 ms)
    ├ /pokemon/2 (6168 ms)
    ├ /pokemon/1 (6138 ms)
    ├ /pokemon/5 (6122 ms)
    ├ /pokemon/6 (5092 ms)
    ├ /pokemon/7 (3569 ms)
    └ [+144 more paths]
+ First Load JS shared by all              115 kB
  ├ chunks/framework-9b5d6ec4444c80fa.js   45.7 kB
  ├ chunks/main-f0e16f48d3775e5e.js        30.7 kB
  ├ chunks/pages/_app-e41591127e174d14.js  38.1 kB
  ├ chunks/webpack-7ee66019f7f6d30f.js     755 B
  └ css/ef46db3751d8e999.css               20 B

○  (Static)  automatically rendered as static HTML (uses no initial props)
●  (SSG)     automatically generated as static HTML + JSON (uses getStaticProps)

Done in 36.94s.
````
