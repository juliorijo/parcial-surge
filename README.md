# Parcial: GitHub Actions y Surge

Pagina HTML en espanol con despliegue automatico al hacer push a `main`.

Repositorio: https://github.com/juliorijo/parcial-surge

Sitio publicado: https://juliorijo-parcial-surge.surge.sh

El despliegue en GitHub Actions se completo correctamente el 14 de octubre
de 2026. El secret `SURGE_TOKEN` esta configurado en GitHub, sin incluir
su contenido en el repositorio.

## Archivos

- `index.html`: pagina web.
- `.github/workflows/main.yml`: workflow de despliegue.
- `package.json` y `package-lock.json`: instalacion reproducible de Surge.

El workflow copia solamente `index.html` a `public` y publica esa carpeta.
No publica el repositorio, las dependencias, el README ni las credenciales.

## Configurar las credenciales de forma segura

1. En una terminal local dentro del proyecto, ejecutar `npm ci`.
2. Ejecutar `npx --no-install surge login` e iniciar sesion directamente
   en la terminal. No compartir la contrasena ni el token en un chat.
3. Ejecutar `npx --no-install surge token`. Copiar el token directamente
   al secret de GitHub, sin guardarlo en archivos del proyecto.
4. En el repositorio, abrir **Settings > Secrets and variables > Actions >
   New repository secret** y crear `SURGE_TOKEN` con el token obtenido
   en el paso anterior. Surge autentica el despliegue usando solo ese token.
5. En **Actions > Desplegar en Surge > Run workflow**, ejecutar el workflow
   sobre `main`. Los siguientes pushes lo ejecutaran automaticamente.
6. Comprobar que el job `deploy` termina correctamente y abrir el sitio
   para verificar que muestra esta pagina.

No escribir tokens en el YAML, argumentos de comandos, commits o capturas.
GitHub entrega el secret como variable de entorno durante el despliegue.
Si falta, el workflow falla con un mensaje explicito.

## Probar un cambio

Modificar un texto de `index.html` y ejecutar:

```powershell
git add index.html
git commit -m "Actualizar pagina"
git push origin main
```

Revisar el nuevo despliegue en Actions y actualizar el sitio en el navegador.
Si Surge indica que el dominio ya pertenece a otra cuenta, elegir un dominio
disponible y actualizar `SURGE_DOMAIN` en el workflow y este README.

## Entrega

Enlace del repositorio: https://github.com/juliorijo/parcial-surge

El repositorio se crea privado por precaucion. Para entregar el parcial,
conceder acceso al docente o cambiarlo a publico desde Settings cuando se
autorice esa visibilidad. Solo considerar terminada la prueba de despliegue
cuando exista una ejecucion exitosa y el sitio responda con la pagina esperada.
