# Informe Final – Análisis de Churn en Telecom X

---

## Introducción

El objetivo de este análisis es comprender los factores que influyen en la evasión de clientes (churn) en Telecom X y proporcionar insights accionables para reducir la tasa de cancelaciones. A través de la importación, limpieza y exploración de datos de clientes, buscamos identificar patrones de comportamiento y características asociadas a la fuga, de manera que el equipo de Data Science pueda desarrollar modelos predictivos y estrategias de retención eficaces.

---

## Limpieza y Tratamiento de Datos

1. **Importación**  
   - Carga de `TelecomX_Data.json` en un DataFrame de pandas.  
   - Conversión de valores numéricos almacenados como texto (por ejemplo, espacios en `account.Charges.Total`) a `float64`.

2. **Normalización de texto**  
   - Todas las columnas de tipo `object` pasaron a minúsculas.  
   - Eliminación de espacios iniciales/finales y signos de puntuación para homogeneizar categorías.

3. **Codificación categórica**  
   - **LabelEncoder** en variables con ≤ 10 valores únicos (por ejemplo `gender`, `Partner`, `Dependents`).  
   - Resultado: DataFrame `df_cod` con columnas numéricas listas para modelado.

4. **Nuevas variables**  
   - **Cuentas_Diarias**: cálculo de cargo promedio diario = `Charges.Monthly / 30`.  
   - **Transformación logarítmica**: se generó `df_loga`, aplicando log(▿) a todas las columnas numéricas positivas, para atenuar skew y estabilizar varianzas.

---

## Análisis Exploratorio de Datos

### Distribución de Churn

![Distribución de Churn](attachment:churn_distribution.png)

La variable objetivo muestra dos grupos:  
- Clientes que permanecieron  
- Clientes que se dieron de baja  

Visualmente, se observa que la proporción de clientes que se dan de baja es aproximadamente un tercio del total, indicando una tasa de churn significativa.

---

### Churn vs Variables Categóricas

Para cada categoría clave (género, tipo de contrato, método de pago), generamos barras apiladas con porcentajes:

- **Género**  
  - Tasa de evasión ligeramente mayor en un género, sugiriendo posibles diferencias de experiencia o preferencia en el servicio.

- **Tipo de contrato**  
  - Los contratos mes a mes presentan la tasa de churn más alta, mientras que los contratos a uno y dos años muestran mayor fidelidad.

- **Método de pago**  
  - El débito automático retiene mejor a los clientes, comparado con pagos manuales.

---

### Churn vs Variables Numéricas

Se graficaron histogramas con KDE y boxplots para `Charges.Total` (gasto total) y `tenure` (meses de contrato):

- Los clientes que se dieron de baja tienden a tener menor antigüedad (`tenure`) y menor gasto total acumulado.
- Existe un pequeño grupo de outliers con alto gasto que también cancelan, lo que podría indicar insatisfacción pese a nivel de consumo.

---

## Conclusiones e Insights

- Los contratos mes a mes concentran la mayor proporción de churn.  
- Mayor fidelidad observada en clientes con planes anuales o bianuales.  
- El débito automático como método de pago está asociado a menor tasa de fuga.  
- Clientes con bajo `tenure` y bajo gasto total muestran mayor riesgo de evasión, lo que sugiere enfocar campañas de retención temprana.

---

## Recomendaciones

- **Incentivar renovaciones anticipadas**  
  Ofrecer descuentos o beneficios a clientes mes a mes para migrar a contratos anuales.

- **Promover débito automático**  
  Destacar conveniencia y posibles bonificaciones al adoptar pago automático.

- **Onboarding focalizado**  
  Implementar programas de bienvenida y seguimiento en los primeros 3–6 meses para clientes nuevos, mitigando el churn temprano.

- **Segmentación avanzada**  
  Desarrollar modelos predictivos usando `df_loga` para detectar clientes con bajo gasto diario o baja antigüedad y lanzar campañas personalizadas.

- **Monitoreo continuo**  
  Automatizar reportes semanales de churn por segmento y ajustar tácticas según las tendencias emergentes.

---

Con estos hallazgos y acciones recomendadas, Telecom X contará con una base sólida para reducir la evasión y mejorar su retención de clientes.  