# Análisis económico de Argentina vs. Sudamérica (2010-2025)

Análisis exploratorio de datos (EDA) que compara la evolución económica de Argentina con la de otros siete países sudamericanos, usando indicadores macroeconómicos del Banco Mundial y del FMI.

> **Estado del proyecto: en progreso.** Este es mi primer proyecto personal de ciencia de datos. El avance se interrumpió durante mi época de parciales y lo estoy retomando. Las secciones marcadas como pendientes se van completando a medida que avanzo.

## Sobre este proyecto

Soy estudiante de la Licenciatura en Inteligencia Artificial y Ciencia de Datos, y este es el primer proyecto que desarrollo por mi cuenta, fuera de las consignas de la facultad.

Lo empecé con dos objetivos:

- **Poner a prueba mis capacidades de procesamiento y análisis de datos** con datos reales, que vienen incompletos, con formatos distintos y con decisiones que tomar (qué limpiar, qué dejar como nulo, qué fuente usar).
- **Llevar a la práctica lo que aprendí en la carrera**: Python, Pandas, NumPy, estadística descriptiva y visualización de datos, aplicados de punta a punta sobre una pregunta concreta.

Fui armando el proyecto por etapas: elegir el dataset, definir las preguntas, limpiar, completar con una segunda fuente, calcular estadística descriptiva y recién después visualizar. Prefiero dejar documentado el proceso, incluidos los errores que fui corrigiendo en el camino, porque es parte de lo que quería practicar.

## Preguntas de análisis

1. ¿Cómo evolucionó el PBI per cápita de Argentina entre 2010 y 2025 comparado con el resto de la región?
2. ¿Cuándo tuvo Argentina sus picos de inflación y cómo se compara con los demás países en esos años?
3. ¿Cómo cambió el desempleo antes y después de la pandemia, y cómo se compara ese cambio con el de los otros países?
4. ¿Qué indicador (crecimiento, inflación o desempleo) fue más volátil en Argentina frente al resto de la región?
5. ¿Se movió la economía argentina en sintonía con la región o con una dinámica más aislada? *(pendiente)*

## Países incluidos

Argentina, Bolivia, Brasil, Chile, Colombia, Ecuador, Perú y Uruguay.

## Indicadores

| Indicador | Columna en el dataset |
|---|---|
| PBI total (USD corrientes) | `GDP (Current USD)` |
| PBI per cápita (USD corrientes) | `GDP per Capita (Current USD)` |
| Crecimiento anual del PBI (%) | `GDP Growth (% Annual)` |
| Inflación, precios al consumidor (%) | `Inflation (CPI %)` |
| Tasa de desempleo (%) | `Unemployment Rate (%)` |

## Fuentes de datos

- **Banco Mundial (2010-2023):** dataset *Global Economic Indicators (2010-2025)* publicado en Kaggle. El archivo original no se redistribuye si la licencia no lo permite; se puede descargar desde la página del dataset en Kaggle y guardar como `data/raw/world_bank_data_2025.csv`.
- **FMI, World Economic Outlook (2024-2025):** descargado desde el [DataMapper del FMI](https://www.imf.org/external/datamapper/datasets) en cinco archivos Excel, uno por indicador.

## Decisiones sobre los datos

Estas decisiones afectan los resultados, por eso las dejo explícitas:

- **Se descartaron las columnas que no responden a las preguntas** (deuda pública, tasa de interés, gasto e ingresos del gobierno, etc.), que además tenían muchos nulos.
- **Inflación de Argentina 2010-2017 queda vacía.** El dataset no tiene datos de inflación argentina para esos años y no encontré una serie comparable y confiable en otras fuentes. Para 2018-2023 se completó con los valores del Banco Mundial. No rellené el hueco con datos de otras metodologías para no mezclar series no comparables.
- **Los datos de 2024-2025 vienen del FMI**, no del Banco Mundial. El FMI marca parte de esos valores como estimaciones. Para cada indicador y país se vaciaron los años posteriores al indicado en la columna *Estimates start after* (se conserva el año indicado). Esto implica que **Uruguay 2025 queda sin PBI, PBI per cápita ni crecimiento**, pero sí tiene desempleo e inflación.
- **Los valores de PBI del FMI vienen en miles de millones** y se convirtieron a dólares para que coincidan con la unidad del Banco Mundial.
- **2023 está en ambas fuentes.** Para evitar duplicados se conservó el dato del Banco Mundial y el FMI se usa solo para 2024-2025. Se verificó que no queden filas repetidas por país y año.
- **Las comparaciones de inflación y volatilidad usan una ventana común (2018-2025)**, que es el único rango donde los ocho países tienen datos de inflación. Con solo 8 observaciones por país, los desvíos estándar son orientativos y no estadísticamente sólidos.

## Estructura del repositorio

```
data/
  raw/          Datos originales, sin modificar (archivos .xls del FMI y CSV del Banco Mundial)
  processed/    Datos transformados por mí (datos_fmi_final.csv)
analisis_economico_argentina.ipynb    Notebook con el análisis completo
README.md
```

## Herramientas

Python, Pandas, NumPy, Matplotlib, Seaborn y Jupyter Notebook.

## Cómo reproducirlo

1. Clonar el repositorio.
2. Descargar el dataset del Banco Mundial desde Kaggle y guardarlo en `data/raw/` (ver *Fuentes de datos*).
3. Instalar las dependencias: `pip install pandas numpy matplotlib seaborn jupyter`.
4. Abrir `analisis_economico_argentina.ipynb` y ejecutar `Restart & Run All`.

## Avance

- [x] Elección del dataset y definición de las preguntas
- [x] Limpieza y filtrado de los países e indicadores relevantes
- [x] Incorporación de datos 2024-2025 del FMI
- [x] Estadística descriptiva por país
- [~] Visualizaciones (PBI per cápita, inflación, desempleo, volatilidad)
- [ ] Pregunta 5: sintonía de Argentina con la región
- [ ] Conclusiones

## Hallazgos

*Se completan cuando termine el análisis.*

## Próximos pasos

- Replicar el mismo análisis en R para comparar ambos lenguajes sobre el mismo problema.
- Cargar los datos en una base SQLite y repetir algunas consultas en SQL.

## Autoría

Proyecto personal desarrollado como parte de mi formación en la Licenciatura en Inteligencia Artificial y Ciencia de Datos.
