# GITT — Gestión de Inventario de Talleres Tecnológicos

Aplicación web para administrar los recursos tecnológicos de los talleres de la Facultad de Ingeniería en Sistemas, Electrónica e Industrial (FISEI) de la Universidad Técnica de Ambato (UTA). GITT centraliza el inventario, los préstamos y la información de ubicación y custodia de los bienes.

## Funcionalidades

- Registro, consulta y edición de equipos e ítems de inventario, con información técnica y administrativa.
- Organización del inventario por categorías, tipos, materiales, colores, estados, condiciones y ubicaciones.
- Búsqueda y flujo de trabajo apoyados por lectura de códigos.
- Gestión de préstamos y devoluciones.
- Administración de usuarios y permisos por rol.
- Generación de reportes en PDF.

## Tecnologías

- [Next.js 15](https://nextjs.org/) con App Router y [React 19](https://react.dev/)
- [TypeScript](https://www.typescriptlang.org/)
- [Tailwind CSS](https://tailwindcss.com/) y componentes basados en Radix UI
- Axios para la comunicación con la API
- React Hook Form y Zod para formularios y validación

## Requisitos

- Node.js 20.18 o posterior
- npm
- Acceso a la API de GITT

## Configuración local

1. Clona el repositorio y entra en el directorio del proyecto:

   ```bash
   git clone <URL_DEL_REPOSITORIO>
   cd <DIRECTORIO_DEL_PROYECTO>
   ```

2. Instala las dependencias:

   ```bash
   npm install
   ```

3. Crea un archivo `.env.local` en la raíz del proyecto y configura la URL base de la API:

   ```dotenv
   NEXT_PUBLIC_API_URL=https://<HOST_DE_LA_API>
   ```

   La aplicación usa esta variable para las solicitudes al backend. En despliegues con Docker, el Dockerfile también declara `NEXT_PUBLIC_API_URLIMAGE` como argumento de build para la URL de imágenes.

4. Inicia el servidor de desarrollo:

   ```bash
   npm run dev
   ```

   Abre [http://localhost:3001](http://localhost:3001).

## Comandos

| Comando | Descripción |
| --- | --- |
| `npm run dev` | Inicia Next.js en modo desarrollo en el puerto 3001. |
| `npm run build` | Genera la compilación de producción. |
| `npm run start` | Sirve la compilación de producción (puerto 3000 por defecto). |
| `npm run lint` | Ejecuta el script de lint definido en `package.json`. |

## Estructura del proyecto

```text
app/          Rutas, layouts y endpoints internos de Next.js
components/   Componentes de interfaz compartidos
config/       Configuración de la aplicación
core/         Infraestructura HTTP y utilidades centrales
features/     Módulos funcionales organizados por dominio
  auth/       Autenticación
  inventory/  Inventario y artículos
  loans/      Préstamos y devoluciones
  reports/    Reportes y exportación PDF
  users/      Usuarios
shared/       Componentes, datos e interfaces compartidos
public/       Recursos estáticos
```

## Autenticación y acceso

La sesión se basa en un token JWT almacenado en una cookie `auth_token`. El middleware protege las rutas de la aplicación y aplica las restricciones por rol configuradas en `shared/data/user-routes.ts`. Se requiere una cuenta habilitada en el servicio de backend para acceder al panel.

## Docker

El repositorio incluye `Dockerfile.frontend`. La URL de la API se puede pasar como argumento de compilación:

```bash
docker build -f Dockerfile.frontend \
  --build-arg NEXT_PUBLIC_API_URL=https://<HOST_DE_LA_API> \
  -t gitt-frontend .
```

Inicia el contenedor publicando el puerto que expone la imagen:

```bash
docker run --rm -p 3000:3000 gitt-frontend
```

## Contribuciones

1. Crea una rama para tu cambio.
2. Mantén los cambios alineados con la organización por módulos de `features/`.
3. Antes de enviar una contribución, ejecuta la compilación y revisa los cambios localmente.
4. Abre un pull request con un resumen y los pasos para verificarlo.

## Licencia

No se especifica una licencia en este repositorio. Consulta con el equipo responsable antes de reutilizar o distribuir el código.
