# Patrones de éxito en videojuegos

Análisis exploratorio de datos y pruebas de hipótesis sobre ventas históricas de videojuegos, con el objetivo de identificar qué factores determinan el éxito de un juego y planificar las campañas publicitarias de 2017 para una tienda online que vende videojuegos en todo el mundo.

![Python](https://img.shields.io/badge/Python-3.9-3776AB?logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?logo=scipy&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white)

---

## Contexto

La tienda online **Ice** vende videojuegos a nivel mundial. Se cuenta con datos de fuentes abiertas que llegan hasta 2016: ventas por región, plataformas, géneros, calificaciones de críticos y usuarios, y la clasificación ESRB de cada juego. El análisis se plantea como si fuera diciembre de 2016 y hubiera que decidir en qué invertir para 2017.

**Preguntas que responde el proyecto:**

- ¿Cuánto dura una plataforma en el mercado y qué periodo de datos es relevante para pronosticar?
- ¿Qué plataformas lideran, cuáles crecen y cuáles van en declive?
- ¿Influyen las reseñas de críticos y usuarios en las ventas?
- ¿Qué géneros son más rentables?
- ¿Cómo cambian las preferencias entre Norteamérica, Europa y Japón?
- ¿Son distintas las calificaciones de usuarios entre plataformas y géneros?

## Datos

`datasets/games.csv` — 16,715 registros, 11 columnas.

| Columna | Descripción |
|---|---|
| `Name` | Nombre del juego |
| `Platform` | Plataforma (PS4, XOne, 3DS, PC, etc.) |
| `Year_of_Release` | Año de lanzamiento |
| `Genre` | Género |
| `NA_sales` / `EU_sales` / `JP_sales` / `Other_sales` | Ventas por región (millones de USD) |
| `Critic_Score` | Calificación de críticos (0-100) |
| `User_Score` | Calificación de usuarios (0-10) |
| `Rating` | Clasificación ESRB |

Los datos de 2016 pueden estar incompletos.

## Metodología

1. **Exploración inicial:** estructura, tipos de datos, valores ausentes y duplicados.
2. **Preparación de datos:**
   - Normalización de nombres de columnas.
   - Conversión de tipos (`year_of_release` a `Int64`, `user_score` a `float`).
   - Tratamiento del valor `tbd` en calificaciones de usuarios como ausente.
   - Decisión justificada para cada columna con nulos y corrección de un registro duplicado.
   - Cálculo de ventas totales por juego.
3. **Análisis exploratorio:**
   - Lanzamientos por año y relevos generacionales de consolas.
   - Ciclo de vida de las plataformas y selección del periodo relevante (2013-2016).
   - Diagramas de caja de ventas por plataforma, con media, mediana, varianza y desviación estándar.
   - Correlación entre reseñas y ventas, y comparación de un mismo juego entre plataformas.
   - Rentabilidad por género.
4. **Perfil de usuario por región:** top 5 de plataformas y géneros con cuota de mercado, e impacto de la clasificación ESRB.
5. **Pruebas de hipótesis:** prueba de Levene para varianzas y prueba t para muestras independientes (Welch cuando las varianzas difieren), con α = 0.05.

## Resultados principales

**Mercado y plataformas**
- Una plataforma exitosa vive alrededor de **10 años**, y surge una nueva generación cada **6-7 años**. Por eso el pronóstico se basa en el periodo **2013-2016**.
- **PS4** lidera el periodo (314 M USD), seguida de PS3, XOne, 3DS y X360. PS4 y XOne son las plataformas en crecimiento; las de generación anterior van en declive.
- Las ventas por juego están muy sesgadas: la mediana de PS4 es 0.20 M frente a un promedio de 0.80 M, es decir, pocos títulos concentran la mayor parte de las ventas.

**Factores de éxito**
- La **calificación de la crítica** tiene una correlación positiva moderada con las ventas (≈ 0.41 en PS4). La calificación de usuarios prácticamente no influye, salvo en consolas de Nintendo.
- Un mismo juego vende de forma muy similar en PS4 y XOne (correlación 0.96), aunque en el 93 % de los casos vende más en PS4.
- **Shooter** es el género más rentable por juego (mediana 0.45 M), seguido de Sports y Platform. Action lidera en ventas totales por su volumen de lanzamientos.

**Perfiles por región**

| Región | Plataforma líder | Género líder | ESRB con más ventas |
|---|---|---|---|
| Norteamérica | PS4 (24.8 %), XOne muy cerca | Action / Shooter | M |
| Europa | PS4 (36.0 %) | Action / Shooter | M |
| Japón | 3DS (48.2 %) | Role-Playing | Sin clasificación ESRB |

**Pruebas de hipótesis**

| Hipótesis nula | Valor p | Resultado |
|---|---|---|
| La calificación promedio de usuarios es igual en Xbox One y PC | ≈ 0.15 | No se rechaza |
| La calificación promedio de usuarios es igual en Acción y Deportes | ≈ 1.4e-20 | Se rechaza (Acción 6.84 vs Deportes 5.24) |

## Recomendaciones para 2017

- Concentrar el presupuesto en **PS4 y XOne** para Norteamérica y Europa, priorizando **Shooter, Action y Sports** con buena calificación de la crítica.
- Diseñar una campaña separada para **Japón**, enfocada en **3DS** y juegos de **Role-Playing**.
- Mantener presencia en **PC** como mercado estable y reducir la inversión en plataformas de generación anterior.
- Usar la calificación de la crítica como señal temprana para elegir qué títulos promocionar.

## Estructura del repositorio

```
analisis-ventas-videojuegos/
├── analisis_videojuegos.ipynb   # Notebook con el análisis completo
├── datasets/
│   └── games.csv                # Datos de ventas de videojuegos
├── requirements.txt
└── README.md
```

## Cómo ejecutarlo

```bash
git clone https://github.com/rubenugu/analisis-ventas-videojuegos.git
cd analisis-ventas-videojuegos
pip install -r requirements.txt
jupyter notebook analisis_videojuegos.ipynb
```

## Autor

**Ruben Ulises Montaño Sanchez** — [GitHub](https://github.com/rubenugu)
