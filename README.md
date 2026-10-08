# PanIA 5S

**Autodiagnóstico de 5S y Buenas Prácticas de Manufactura para panaderías de barrio**, conforme a la
Resolución 2674 de 2013 (Ministerio de Salud y Protección Social, vigilada por el INVIMA).
Mejora de procesos y cumplimiento normativo en una sola herramienta, gratuita y de código abierto.

> Proyecto presentado en el ENSIU 2026 de UNIMINUTO — Misión 4: Inteligencia Artificial para la equidad.

![Diagnóstico](docs/capturas/shot_diag.png)

## ¿Qué hace?
| Módulo | Descripción |
|---|---|
| **Evaluar** | 40 ítems organizados por las 5S; cada uno cita el artículo y capítulo de la Res. 2674/2013 que lo exige. |
| **Diagnóstico** | Cumplimiento global, radar 5S, semáforo por capítulo y hallazgos críticos para una visita del INVIMA. |
| **Plan de acción** | Acciones priorizadas por impacto sanitario × facilidad de implementación (urgente / corto / mediano plazo). |
| **Documentos** | Plan de saneamiento del Art. 26 con sus 4 programas, pre-diligenciado y exportable a PDF. |
| **Tablero territorial** | Resultados agregados del piloto por municipio, provincia y S. |
| **Asistente IA** | Responde en lenguaje sencillo con base en el diagnóstico (reglas; LLM cuando el entorno lo provee). |

## Ejecutar en macOS

### Opción A — Descargar la app lista
1. Ve a la pestaña **Releases** (o a **Actions → Build PanIA 5S → Artifacts**) y descarga `PanIA 5S-1.0.0-arm64.dmg`
   (Apple Silicon) o `PanIA 5S-1.0.0.dmg` (Intel).
2. Abre el DMG y arrastra **PanIA 5S** a *Aplicaciones*.
3. Primera apertura: clic derecho → **Abrir** (la app no está firmada con certificado de Apple Developer).

### Opción B — Desde el código fuente
Requiere [Node.js 20+](https://nodejs.org).
```bash
git clone https://github.com/irozo/pania-5s.git
cd pania-5s
npm install
npm start          # abre la app de escritorio
```
Para generar el instalador localmente:
```bash
npm run build:mac  # crea dist/PanIA 5S-1.0.0-arm64.dmg y dist/PanIA 5S-1.0.0.dmg
```

### Opción C — Sin instalar nada (navegador)
```bash
npm run web        # sirve src/ en http://localhost:8080
```
o simplemente abre `src/index.html` en Safari o Chrome. La app funciona sin conexión y guarda las respuestas en el dispositivo.

## Estructura del repositorio
```
pania-5s/
├─ main.js                  # proceso principal de Electron (ventana, menú, guardado nativo, PDF)
├─ preload.js               # puente seguro renderer ↔ sistema operativo
├─ src/index.html           # la aplicación completa (HTML + CSS + JS, sin dependencias)
├─ data/
│  ├─ generar_datos.py      # genera los datos del piloto (semilla fija, reproducible)
│  ├─ datos_piloto.json     # 20 panaderías × 40 ítems, pre-test y post-test
│  └─ datos_piloto.csv      # mismo contenido en formato tabular (Excel, R, SPSS)
├─ docs/capturas/           # capturas de pantalla (escritorio y móvil)
├─ .github/workflows/       # CI: compila el DMG en macOS en cada push
├─ build/                   # íconos del instalador (icon.icns / icon.ico / icon.png)
└─ package.json
```

## Datos del piloto
`data/datos_piloto.csv` contiene una fila por panadería × ítem con: municipio, provincia, empleados, estrato,
S, capítulo, artículo, pregunta, impacto, facilidad, `pre_test` y `post_test` (0 = no cumple, 1 = parcial, 2 = cumple).
Cumplimiento = suma de puntos / 80. Son **datos sintéticos** generados con `data/generar_datos.py` para el
desarrollo y la demostración; se reemplazan por los datos de campo del pilotaje real.

Resumen del piloto simulado: cumplimiento promedio **46,4 % → 73,7 %** (+27,3 pp); panaderías en riesgo
sanitario alto **13 → 0**.

## Marco normativo
- Resolución 2674 de 2013 — Ministerio de Salud y Protección Social.
- Decreto 3075 de 1997 (antecedente).
- Metodología 5S (Hirano, 1995).

## Contribuir
Lee [CONTRIBUTING.md](CONTRIBUTING.md). Las mejoras más valiosas: nuevos ítems con su artículo, traducción a otros
subsectores de alimentos regulados por la misma resolución, y validación en campo.

## Licencia
MIT — ver [LICENSE](LICENSE). Puedes usar, modificar y redistribuir citando la fuente.

## Cita sugerida
Rozo Rojas, I. (2026). *PanIA 5S: aplicación con inteligencia artificial para la evaluación de las 5S y las
Buenas Prácticas de Manufactura en panaderías de Colombia* [Software]. UNIMINUTO. https://github.com/irozo/pania-5s
