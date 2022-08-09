# Sobre el curso de capacitación

**Nombre**: Next.js: El framework de React para producción

**Link**: <https://www.udemy.com/course/nextjs-fh>

***

## Índice

- [Sobre el curso de capacitación](#sobre-el-curso-de-capacitación)
  - [Índice](#índice)
  - [Sesiones y anotaciones respectivas](#sesiones-y-anotaciones-respectivas)
    - [28. Archivos de JavaScript a TypeScript](#28-archivos-de-javascript-a-typescript)
      - [Problemas resueltos](#problemas-resueltos)
      - [Trivia](#trivia)
    - [29. Migrando _app.jsx a _app.tsx](#29-migrando-_appjsx-a-_apptsx)

***

## Sesiones y anotaciones respectivas

### 28. Archivos de JavaScript a TypeScript

El instructor está enseñando cómo realizar los cambios en objetos y props de JavaScript a TypeScript, usando strictmode (`"strict": true`).

#### Problemas resueltos

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

#### Trivia

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

Artículo que explica la diferencia: <https://medium.com/@martin_hotell/interface-vs-type-alias-in-typescript-2-7-2a8f1777af4c>

### 29. Migrando _app.jsx a _app.tsx

Para investigar luego:

````ts
type NextPageWithLayout = NextPage & {
  getLayout?: (page: JSX.Element) => JSX.Element;
};
````

**Por qué usa signos de interrogación?**
Respuesta: declarar atributo opcional.
