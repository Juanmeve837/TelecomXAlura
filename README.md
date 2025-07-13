
# 📊 Análisis de Deserción de Clientes - TelecomX

Este proyecto tiene como objetivo identificar y analizar los factores que contribuyen a la deserción de clientes (`Churn`) en una empresa de telecomunicaciones ficticia llamada **TelecomX**. Se utilizan técnicas de análisis exploratorio de datos (EDA), procesamiento de datos anidados en formato `.JSON` y visualizaciones para generar *insights accionables* que puedan ayudar a mejorar la retención de clientes.

## 🧾 Contenido

- [Descripción del problema](#problema)
- [Fuente de datos](#fuente-de-datos)
- [Librerías utilizadas](#librerías-utilizadas)
- [Procesamiento de datos](#procesamiento-de-datos)
- [Análisis exploratorio](#análisis-exploratorio)
- [Hallazgos clave](#hallazgos-clave)
- [Conclusiones](#conclusiones)
- [Cómo ejecutar](#cómo-ejecutar)

## 📌 Problema

La retención de clientes es un desafío constante para empresas de telecomunicaciones. Este proyecto busca **identificar patrones de abandono** para actuar a tiempo y reducir la pérdida de usuarios. Para ello, se analiza la variable `Churn` (abandono), que indica si un cliente dejó la compañía (`Yes`) o no (`No`).

## 🌐 Fuente de datos

El conjunto de datos fue extraído desde un archivo JSON disponible públicamente:

📄 [`TelecomX_Data.json`](https://raw.githubusercontent.com/alura-cursos/challenge2-data-science-LATAM/main/TelecomX_Data.json)

## 🛠️ Librerías utilizadas

- `pandas` – Manipulación y limpieza de datos
- `numpy` – Tratamiento de valores nulos
- `seaborn` / `matplotlib` – Visualización de datos
- `requests` – Descarga del archivo JSON
- `summarytools` – Exploración tabular rápida de estructuras

## ⚙️ Procesamiento de datos

- Se realizó **normalización del archivo JSON** para separar variables anidadas (`customer`, `phone`, `internet`, `account`).
- Se **limpiaron los valores faltantes** en:
  - `Churn` → Eliminados (3% del total), al ser la variable objetivo.
  - `Charges.Total` → Inferidos como `MonthlyCharges × tenure` (usando `.clip(lower=1)` para evitar multiplicación por 0).
- Se **convirtieron columnas categóricas binarias** (`Yes`/`No`, `1`/`0`) a tipo `boolean`.
- Se detectaron **valores inconsistentes** (espacios vacíos) usando expresiones regulares.

## 🔍 Análisis exploratorio

- Comparación de medias entre clientes que desertan y los que permanecen.
- Tablas cruzadas (`value_counts(normalize=True)`) para columnas categóricas.
- Segmentación específica sobre los clientes que abandonaron (`Churn == True`).
- Uso de `.clip()` para normalizar la antigüedad en casos de primer mes.

## 📈 Hallazgos clave

| Área                   | Insight |
|------------------------|---------|
| **Tenure**             | Clientes con menor antigüedad son significativamente más propensos a abandonar. |
| **Contract**           | El 89% de los que abandonaron tenían contratos tipo `Month-to-month`. |
| **TechSupport**        | El 78% de los desertores no contaban con soporte técnico. |
| **Online Services**    | Altas tasas de abandono en usuarios sin `OnlineSecurity`, `OnlineBackup` y `DeviceProtection`. |
| **Payment Method**     | `Electronic check` se asocia más con abandono. |
| **Charges**            | No hay diferencia significativa en el monto mensual (`Charges.Monthly`). |
| **Perfil general del desertor** | Tiene teléfono, no tiene pareja ni dependientes, factura electrónica, y es menor de 65 años. |

## 📌 Conclusiones

- El abandono está **altamente relacionado con la antigüedad y tipo de contrato**.
- Los **servicios adicionales (seguridad, backup, soporte)** tienen una influencia significativa en la retención.
- Las variables de entretenimiento (`StreamingTV`, `StreamingMovies`) no tienen impacto claro en la deserción.
- El análisis permite construir un **perfil de riesgo** para clientes propensos a dejar la empresa.

## ▶️ Cómo ejecutar

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/Juanmeve837/TelecomXAlura.git
   cd TelecomXAlura
   ```

2. Ejecutar en Google Colab (recomendado):
   - Asegúrate de instalar `summarytools` al inicio:
     ```python
     %pip install summarytools -q
     ```

3. Alternativamente, ejecutar en entorno local:
   ```bash
   pip install pandas numpy seaborn matplotlib summarytools requests
   python churn_analysis.py
   ```

## 📂 Estructura del proyecto (sugerida)

```
telecom-churn-analysis/
│
├── 📁 data/
│   └── TelecomX_Data.json
│
├── 📁 notebooks/
│   └── TelecomXAlura.ipynb
├── README.md
```

## 💡 Autor

Este análisis fue desarrollado como ejercicio exploratorio y académico para la comprensión del fenómeno de *Churn* en servicios de telecomunicaciones.  
Email: jmesav@gmail.com
readme porwered by ChatGPT
