# Optimización de Crédito - Segmentación de Clientes

## 1. Introducción

En el sector financiero, la correcta administración del crédito es fundamental para maximizar la rentabilidad y minimizar los riesgos. Sin embargo, la asignación de límites de crédito y la gestión del sobreendeudamiento son desafíos constantes, especialmente para instituciones que manejan una gran cantidad de clientes con perfiles diversos. Determinar cuáles clientes podrían beneficiarse de un aumento en su límite de crédito, o identificar aquellos a los que sería prudente reducir dicho límite, puede ayudar a optimizar el rendimiento y mitigar los riesgos de impagos.

Este proyecto presenta una solución basada en la **segmentación de clientes mediante algoritmos de clustering** para agrupar a los clientes en función de su comportamiento de pagos y uso de crédito. Esto se logra aplicando técnicas de machine learning, como K-Means y DBSCAN, que han demostrado ser útiles en problemas de segmentación en sectores como la banca y el retail. La segmentación proporciona una comprensión profunda de los patrones de comportamiento de los clientes, facilitando la identificación de perfiles específicos. En última instancia, esta segmentación permitirá a la empresa ajustar los límites de crédito de forma precisa y personalizada.

## 2. Metodología

Para abordar el problema, se utilizó una metodología estructurada que incluye las siguientes etapas:

1. **Análisis exploratorio de datos** para comprender las características principales del conjunto de datos y detectar patrones iniciales.
2. **Preprocesamiento de datos** mediante limpieza y escalado para asegurar que los datos sean adecuados para el modelado.
3. **Entrenamiento de modelos de clustering** usando K-Means y DBSCAN para identificar grupos de clientes con comportamientos similares.
4. **Interpretación de clusters** para relacionar los resultados del modelo con el contexto de negocio.
5. **Evaluación y comparación de modelos** para seleccionar la solución más efectiva.

### 3. Análisis exploratorio

El dataset contiene información relevante sobre el comportamiento financiero de los clientes de una institución crediticia. Los datos incluyen diversas métricas relacionadas con el uso y el comportamiento de los clientes en cuanto a su límite de crédito, pagos y otras características de gasto. A continuación se presentan algunos de los descubrimientos clave realizados durante la exploración de este dataset:

-   **Balance y Crédito**:

    -   **CREDIT_LIMIT**: Refleja el límite de crédito asignado a cada cliente. Es una característica crucial, ya que buscamos optimizar su ajuste con base en el comportamiento del cliente.
    -   **BALANCE**: Muestra el saldo promedio de cada cliente. Clientes con saldos consistentemente altos en comparación con su límite de crédito pueden indicar un comportamiento de alto riesgo o un posible candidato para un aumento de crédito.

-   **Comportamiento de Pago**:

    -   **MINIMUM_PAYMENTS**: Representa el pago mínimo realizado por el cliente, lo cual da una idea de su compromiso financiero. Un valor bajo o inconsistente podría indicar riesgo de incumplimiento.
    -   **PAYMENTS**: La cantidad total pagada por el cliente. Un análisis de esta variable en conjunto con `BALANCE` y `CREDIT_LIMIT` permite identificar patrones de pago.

-   **Comportamiento de Gastos**:

    -   **PURCHASES**: Indica el total de compras realizadas. Al analizar esta variable junto con `BALANCE` y `CREDIT_LIMIT`, se puede inferir el nivel de actividad financiera de cada cliente.
    -   **ONEOFF_PURCHASES y INSTALLMENTS_PURCHASES**: Estas columnas diferencian entre compras realizadas en una sola transacción y aquellas en cuotas, lo que ayuda a entender las preferencias de gasto de cada cliente.

-   **Características adicionales**:
    -   **TENURE**: La cantidad de meses que el cliente lleva en la institución. Clientes con una alta tenencia y un buen comportamiento de pagos son candidatos ideales para un aumento de crédito.

Durante el análisis, observamos que muchos clientes muestran comportamientos consistentes en el pago completo de su saldo y utilizan solo una fracción de su límite de crédito. Esto sugiere la presencia de varios grupos de clientes, con algunos más conservadores en el uso de su crédito y otros con un comportamiento más riesgoso.

## 4. Procesamiento de Datos

Los datos pasaron por varias etapas de preprocesamiento:

-   **Limpieza**: Se eliminaron registros incompletos y valores atípicos extremos.
-   **Escalado**: Todas las variables numéricas fueron escaladas para garantizar que los algoritmos de clustering funcionaran de manera eficiente.
-   **Codificación de Variables Categóricas**: Se convirtieron las variables categóricas en formato numérico mediante técnicas de codificación, para que pudieran ser utilizadas en los modelos de machine learning.

Estas transformaciones fueron necesarias para mejorar la calidad de los datos y asegurar que el modelo fuera preciso en la detección de patrones.

## 5. Entrenamiento y Tuneo de Hiperparámetros

Se entrenaron dos modelos de clustering:

-   **K-Means**: Se seleccionó el número óptimo de clusters usando el Método del Codo, lo cual resultó en 4 clusters. K-Means es útil para agrupar datos homogéneos y permite obtener una segmentación general.
-   **DBSCAN**: Este modelo fue útil para detectar outliers (clientes con comportamientos inusuales), utilizando una métrica de distancia adecuada y ajustando los parámetros `eps` y `min_samples` para encontrar la estructura de los datos.

Ambos modelos se evaluaron utilizando el Silhouette Score, y se compararon sus resultados para decidir cuál capturaba mejor la heterogeneidad en los comportamientos de los clientes.

## 6. Interpretación de los Clusters

Los clusters obtenidos muestran distintos perfiles de clientes en términos de su comportamiento de pago y uso de crédito:

-   **Cluster 0**: Clientes con comportamiento conservador, quienes regularmente pagan su saldo completo y utilizan solo una pequeña parte de su límite.
-   **Cluster 1**: Clientes de alto riesgo que utilizan la mayor parte de su límite de crédito y no siempre realizan el pago completo.
-   **Cluster 2**: Clientes de bajo uso de crédito, que podrían beneficiarse de un aumento en su límite dado su bajo nivel de endeudamiento.
-   **Cluster 3**: Clientes moderados en el uso de su crédito y que ocasionalmente pagan el saldo completo.

Estas interpretaciones permiten una visión detallada de cada segmento, facilitando decisiones estratégicas sobre ajustes en los límites de crédito y estrategias de fidelización.

## 7. Implementación en el Negocio

Para implementar esta solución en el negocio:

1. **Integración con el sistema de administración de crédito**: Utilizar los clusters para ajustar automáticamente los límites de crédito en función de las características de cada grupo.
2. **Monitoreo y actualización**: Revisar y ajustar los clusters periódicamente para adaptarse a los cambios en los comportamientos de los clientes.
3. **Alertas para clientes atípicos**: Los outliers detectados por DBSCAN pueden ser monitorizados más de cerca para prevenir riesgos de sobreendeudamiento.

Empresas en el sector bancario ya aplican segmentaciones basadas en machine learning para la asignación de límites de crédito, lo cual reduce riesgos financieros y mejora la experiencia del cliente.

## 8. Limitaciones

Algunas limitaciones de esta solución incluyen:

-   **Datos limitados**: La ausencia de variables clave, como historial de empleo o ingresos del cliente, limita la precisión del modelo.
-   **Poder computacional**: Algunos parámetros de DBSCAN requieren recursos computacionales altos, especialmente con grandes volúmenes de datos.
-   **Generalización de K-Means**: Los clusters de K-Means son homogéneos y pueden subestimar a clientes con comportamientos extremos.

## 9. Conclusiones y Recomendaciones

### Conclusiones

El proyecto logró segmentar a los clientes en grupos con comportamientos diferenciados, permitiendo una estrategia de optimización de crédito más personalizada. DBSCAN demostró ser más eficaz en detectar comportamientos atípicos, cruciales para la gestión de riesgos.

### Recomendaciones

-   Para mejorar la precisión, se recomienda registrar datos adicionales, como los ingresos y el historial de empleo.
-   Se aconseja a futuros científicos de datos ajustar los parámetros de DBSCAN para adaptarse a sus datos específicos, ya que este modelo puede ser sensible a los parámetros.

## 10. Future Work

Para mejorar el proyecto, se podrían considerar las siguientes mejoras:

1. **Agregar más variables:** como puntuaciones de crédito, historial de ingresos, y detalles adicionales de gasto.
2. **Incorporar técnicas de aprendizaje supervisado:** para validar los clusters en función de los riesgos de crédito reales.
