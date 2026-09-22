# Reporte EERR Consolidado — TASCO

Sitio estatico (`index.html`) publicado con GitHub Pages. Contiene el estado de resultados
consolidado y la proyeccion de impuesto teorico SII por empresa, para las 18 sociedades del
grupo TASCO (Inmobiliaria, Constructora, Rentas y Holding).

## Confidencialidad

Este repositorio y el sitio publicado son **publicos**: cualquier persona con la URL puede
verlo (no aparece en buscadores, pero no requiere login). Contiene cifras financieras
internas (ingresos, costos, resultados y proyeccion de impuestos por empresa). Antes de
compartir la URL fuera del equipo, confirma que ese nivel de exposicion es aceptable. Si mas
adelante se requiere restringir el acceso, las alternativas son:

- **GitHub Enterprise Cloud + Pages privado**: el sitio solo es visible para miembros
  logueados de la organizacion (requiere plan Enterprise).
- **Cloudflare Pages + Cloudflare Access**: el repo puede seguir en GitHub (publico o
  privado) y Cloudflare agrega una capa de login (ej. con correo corporativo) antes de
  mostrar el sitio, sin depender de un plan Enterprise de GitHub.

## Como actualizar el reporte

Cada vez que se regenera `Reporte_EERR_Consolidado_Tasco.html` con datos nuevos (nueva carga
mensual en "Proyeccion Resultados SII 2026.xlsx" u otra base del mismo formato):

```bash
cp "../Reporte_EERR_Consolidado_Tasco.html" index.html
git add index.html
git commit -m "Actualizar reporte: <breve descripcion, ej. 'datos a septiembre 2026'>"
git push
```

GitHub Pages redespliega automaticamente unos segundos/minutos despues del push. Todo el
historial de cambios queda disponible con `git log` — permite ver cuando cambio cada cifra
y revertir (`git revert <commit>`) si una actualizacion tuvo un error.

## Fuente de datos

El reporte se arma cruzando la pestana CONSOLIDADO (y las 18 pestanas por empresa) del
archivo `Proyeccion Resultados SII <año>.xlsx` de esta misma carpeta. Ver
`../estructura-eerr-consolidado-sii.md` (o el doc equivalente en el proyecto de Claude) para
el detalle de formulas, mapeo de empresas/RUT/tasas y los dos ajustes aplicados al modelo
original.

## Publicar por primera vez (pendiente de hacer)

1. Crea un repositorio nuevo en GitHub (publico), por ejemplo `tasco-reporte-eerr`.
   **No** marques "Add a README" ni ".gitignore" al crearlo (ya los trae esta carpeta).
2. En esta carpeta, conecta el repo remoto y sube el primer commit:

   ```bash
   git remote add origin https://github.com/<tu-usuario-u-org>/tasco-reporte-eerr.git
   git branch -M main
   git push -u origin main
   ```

3. En GitHub: **Settings -> Pages** -> en "Build and deployment", Source = *Deploy from a
   branch* -> Branch = `main` / `/(root)` -> Save.
4. Espera 1-2 minutos. La URL queda publicada en la misma pantalla de Settings -> Pages,
   con el formato:

   ```
   https://<tu-usuario-u-org>.github.io/tasco-reporte-eerr/
   ```

   Esa URL es fija — no cambia aunque se sobrescriba `index.html` en el futuro.
