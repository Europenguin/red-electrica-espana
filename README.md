# La red eléctrica española en 2026

**Infografía interactiva** sobre el sistema eléctrico español: generación (nuclear, gas, carbón, hidráulica y renovables), **almacenamiento** —bombeo hidráulico y baterías— e interconectores, con énfasis en los proyectos que dan estabilidad a la red tras el apagón del 28 de abril de 2025 y en el objetivo de 22,5 GW de almacenamiento a 2030.

**Web:** https://europenguin.github.io/red-electrica-espana/

Datos actualizados a **20 de octubre de 2026**.

---

## Contenido

| Sección | Qué incluye |
|---|---|
| Portada + KPIs | 142.558 MW instalados (+7,3%), 3.427 MW de almacenamiento, objetivo PNIEC de 22,5 GW y 798 horas con precio ≤0 en 2025 |
| Mapa | 65 puntos sobre mapa SVG de provincias: nuclear, gas (CCGT), carbón en cierre, hidráulica, bombeo, baterías, renovables e interconectores. Filtros por tecnología, etiquetas y panel de detalle con datos y fuentes |
| Fichas | 24 tarjetas agrupadas en nuclear, bombeo, baterías, gas-carbón y renovables/interconectores, enlazadas con el mapa |
| Gráficos | Capacidad instalada por tecnología (cierre 2025) y horas con precio ≤0 (2023-2026), cada uno con su bloque de análisis |
| Almacenamiento | De 3,4 GW heredados a 22,5 GW: pipeline de 39.489 MW de baterías, ayudas FEDER (818,3 M€) y los 11 bombeos adjudicados (BORALMAC) |
| Estabilidad | El apagón del 28-abr-2025, inercia, coste de los servicios de ajuste (3.812 M€), LOLE y el nuevo mercado de capacidad |
| Cronología | 2025-2035: del apagón al cierre del programa nuclear |
| Fuentes y notas | REE, MITECO, BOE, empresas y prensa sectorial, con metodología (criterios de bombeo, baterías y estimaciones) |
| Certificado | Sello circular «Certificado de calidad» en el pie, junto a la fecha de verificación de los datos |

## Estructura

Sin dependencias ni build:

```
index.html             HTML + CSS + JS (mapa, tarjetas, gráficos, filtros, estilos de impresión)
mapa-espana.js         window.SPAIN_GEO → límites provinciales (GeoJSON abierto),
                       proyección Mercator, viewBox 1000×821,7 y recuadro de Canarias
sello-europenguin.png  sello circular «Certificado de calidad» del pie
README.md
```

- **Sin framework ni npm**: se abre directamente en el navegador (`file://` funciona igual que en servidor).
- **El mapa es SVG generado a runtime**: cada provincia es un `<path>`, cada instalación un marcador con forma por tecnología (cuadrado = nuclear, círculo = gas, triángulo invertido = carbón, hexágono = hidráulica, rombo = bombeo, rectángulo = baterías, triángulo = renovable, doble barra = interconector) y estado (relleno = operación, discontinuo = obra/anuncio, gris = cierre).

## Ver en local

Abre `index.html` con doble clic, o sirve la carpeta:

```powershell
npx serve .
```

## Editar los datos

Todo vive en el array `SITES` de `index.html`:

```js
{id:'lamuela',n:'Cortes–La Muela',short:'La Muela',city:'Cortes de Pallás · Valencia',ccaa:'C. Valenciana',
 lat:39.24, lon:-0.94,        // coordenadas del marcador en el mapa
 t:'bom',                      // nuc | gas | car | hid | bom | bes | ren | int
 st:'operativa',               // operativa | obra | anuncio | cierre
 stl:'En operación · bombeo',  // etiqueta visible
 desc:'…', f:[['Capacidad','1.390 MW']], src:'Fuente (fecha)',
 lp:[13,4,'r'],                // etiqueta en el mapa: desplazamiento x,y y lado (l/r)
 card:1}                       // 1 = aparece también como ficha
```

Al añadir una instalación, recuerda actualizar los KPIs, el chip de la portada, los contadores del panel y el sello del pie (número de puntos y fichas).

## PDF / imprimir

Botón **«Guardar en PDF / imprimir»** en el mapa. Los estilos `@media print` fuerzan A4 con paginación (portada · mapa · fichas · gráficos · almacenamiento · estabilidad · cronología y fuentes). Si el contenido crece, revisa la paginación.

## Publicación

GitHub Pages despliega `main` automáticamente en cada push (~1 min):

```powershell
git add index.html
git commit -m "mensaje"
git push
```

Recarga con **Ctrl+F5** si el navegador muestra una versión anterior.

## Fuentes

Red Eléctrica/Redeia (Informe del Sistema Eléctrico 2025, potencia instalada y módulos de generación), MITECO (PNIEC 2023-2030, RD 997/2025, Orden TED/966/2026, 3ª MAP, resoluciones BORALMAC y FEDER), BOE (autorizaciones de almacenamiento y prórroga de Almaraz), comité técnico del apagón del 28-abr-2025, informes ENTSO-E y CNMC, Foro Nuclear, IDAE, OMIE, UNEF, pv magazine, El Periódico de la Energía, Energías Renovables, Aurora Energy Research, y comunicados de Iberdrola, ENGIE, Repsol, Naturgy, Endesa, EDP, Enagás, Enresa y Redeia. El listado completo está en el pie de la infografía.

Las coordenadas son municipales o aproximadas. Las potencias pueden variar según la fuente (bruto/neto; bombeo «puro» vs. parque reversible total) y las estimaciones se marcan como tales en cada ficha.
