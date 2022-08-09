# Sobre el curso de capacitación

**Nombre**: Next.js: El framework de React para producción

Link:

## Sesiones y anotaciones respectivas

### 28. Archivos de JavaScript a TypeScript

Dos observaciones:

1. `tsconfig.json` que fue generado automáticamente le faltó en `"compilerOptions"` la propiedad:

    ````json
    "moduleResolution": "node"
    ````

2. El video del curso se desarrolló con React v17 y ahora estamos en React v18.

    Hay un setting que se rompe porque los defaults cambian. La solución consiste en cambiar esto:

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
