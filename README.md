# Laboratorio 3 — Ruta Alpes

La entrega integrada esta en [entrega/laboratorio_3_final.ipynb](entrega/laboratorio_3_final.ipynb), con su [HTML](entrega/laboratorio_3_final.html) y el [CSV de predicciones](entrega/Lab3_datos_Prueba.csv). Se ejecuto completa y sus nueve variantes reprodujeron los resultados originales. Revisar [entrega/LEEME.md](entrega/LEEME.md) y el guion del video para los detalles finales.

Plantillas iniciales para desarrollar en equipo el laboratorio de clasificación de 202620, adaptadas a las prácticas 7–10 del curso. **No contienen ejecuciones, resultados ni conclusiones del laboratorio.** La limpieza queda a cargo del estudiante.

Enunciado consultado: [Laboratorio 3_Clasificación.md](../MaterialDeClase-ISIS-2611/202620/Laboratorios/L3/Laboratorio%203_Clasificación.md).

## Reparto recomendado

El enunciado exige un modelo de cada familia **por tipo de cupón**, seis modelos principales en total. La diferencia entre integrantes es la población y el problema de negocio; no hace falta inventar algoritmos o grillas distintos para evitar duplicación. Usar las mismas grillas facilita comparar ambos cupones. Cada búsqueda encontrará sus propios hiperparámetros.

| Integrante | Cupón | Regresión logística | Árbol de decisión | Bosque |
|---|---|---|---|---|
| 1 | Cafetería | [regresion_logistica_1.ipynb](regresion_logistica_1.ipynb) | [arbol_decision_1.ipynb](arbol_decision_1.ipynb) | [bosque_aleatorio_1.ipynb](bosque_aleatorio_1.ipynb) |
| 2 | Restaurante(<20) | [regresion_logistica_2.ipynb](regresion_logistica_2.ipynb) | [arbol_decision_2.ipynb](arbol_decision_2.ipynb) | [bosque_aleatorio_2.ipynb](bosque_aleatorio_2.ipynb) |

Asignar nombres antes de trabajar. Se reutilizó el archivo vacío `regresion_logistica_1.ipynb` que ya existía. Las hipótesis propuestas son preguntas, no hallazgos. Considerar los hábitos específicos del cupón como posibles factores relevantes, sin eliminar los demás hábitos de la comparación principal.

| Familia | Cómo abordarla | Qué aporta al informe |
|---|---|---|
| Regresión logística | One-hot, escalamiento de temperatura, L1/L2, solvers compatibles y búsqueda de C | Asociaciones y signos de coeficientes; explicar regularización y límites de una frontera lineal |
| Árbol | Buscar profundidad, mínimo de muestras por hoja y criterio | Reglas comprensibles; discutir complejidad, sobreajuste e inestabilidad |
| Random Forest | Buscar número de árboles, profundidad y mínimo de muestras por hoja | Interacciones y desempeño; importancia por reducción de impureza y límites de interpretación |

El integrante 2 realiza además el experimento de balanceo. Las tres plantillas de Restaurante lo incluyen para facilitar la comparación, aunque el enunciado no exige explícitamente repetirlo en las tres familias. Si reparten la carga, acuerden cuál familia usarán para esa actividad y documenten la decisión. El integrante 1 puede encargarse de consolidar tabla y figuras; ambos revisan el análisis, el video y las predicciones.

## Relación con las prácticas del curso

Los notebooks siguen el orden del material: importación, carga, revisión del subconjunto, partición, pipeline, búsqueda, evaluación, interpretación y persistencia. Las llamadas a GridSearchCV y a los pipelines son explícitas; se retiró la función genérica de búsqueda y la infraestructura de huellas del archivo de la primera versión.

| Referencia | Qué se conserva | Adaptación al laboratorio |
|---|---|---|
| [Práctica 7: regresión logística](../MaterialDeClase-ISIS-2611/202620/Prácticas/P7_Regresión%20logística/P7_RegresionLogistica.ipynb) | SimpleImputer, StandardScaler, OneHotEncoder con referencia, ColumnTransformer, grilla L1/L2, C y solvers, coeficientes, joblib | Etiqueta Sí/No; cinco folds; F1 macro común a todos; compatibilidad con versiones nuevas de scikit-learn |
| [Práctica 8: árboles](../MaterialDeClase-ISIS-2611/202620/Prácticas/P8_Árboles%20de%20decisión/ArbolesDecision.ipynb) | Pipeline, criterio, profundidad, matriz de confusión, feature_importances_, plot_tree y export_text | Se añade min_samples_leaf porque lo exige el enunciado; se acota la grilla |
| [Práctica 9: SMOTE](../MaterialDeClase-ISIS-2611/202620/Prácticas/P9_KNN_SMOTE/P9_KNN_SMOTE.ipynb) | ImbPipeline y SMOTE dentro de CV; comparación de métricas | Se cambia KNN por el clasificador correspondiente; se documenta la limitación de sintetizar categorías one-hot |
| [Práctica 10: Random Forest](../MaterialDeClase-ISIS-2611/202620/Prácticas/P10_Ensembles/P10_RandomForest.ipynb) | Misma grilla de número de árboles, profundidad y mínimo por hoja; F1 macro e importancias | Se añade pipeline por las variables categóricas y por el requisito del laboratorio. class_weight queda como posible extensión |

El objetivo es que cada estudiante comprenda, revise y pueda explicar sus celdas. Mantener la declaración del apoyo de IA y escribir las justificaciones y conclusiones a partir de su trabajo y resultados.

## Entrada que debe preparar el equipo

Guardar `data/procesados/datos_limpios.csv` en UTF-8, con encabezados. No se creó un archivo ficticio de datos ni se modificaron los Excel originales.

- `id_fila`: identificador único, estable, asignado **antes** de filtrar, ordenar o eliminar registros. No es predictor. Por ejemplo, al leer el Excel original, pueden añadir `datos['id_fila'] = datos.index` y conservarlo durante su limpieza.
- `cupon`: conservar exactamente `Cafetería` y `Restaurante(<20)`. Se pueden conservar otros cupones en el CSV; los notebooks los filtran.
- `acepta_cupon`: etiquetas `Sí` y `No`, sin faltantes.
- Predictores: conservar los nombres del diccionario. Si descartan columnas, usar la misma decisión en los tres algoritmos de cada cupón y justificarla. Los notebooks admiten columnas descartadas; no necesitan todos los predictores originales.
- Se permiten faltantes en predictores: ahora los pipelines incluyen SimpleImputer, como la práctica 7. Usan mediana para temperatura y moda para las variables categoricas, respetando la decision tomada en el notebook de limpieza. Revisar y justificar estas decisiones. No se corrigen valores inválidos, eliminan filas ni deduplican automáticamente.

El diccionario trata edad, ingreso, educación, hora y frecuencias como categorías; no asumir que todo valor con apariencia numérica es continuo. La plantilla aplica one-hot a todas las variables salvo `temperatura`. Si cambian la representación, modificar `COLUMNAS_NUMERICAS` y justificarlo de forma consistente. Revisar otros identificadores añadidos para excluirlos también.

Una limpieza basada en reglas del diccionario puede aplicarse de manera uniforme. Las operaciones que **aprenden de los datos** (imputación por mediana/moda, escalamiento, selección por asociación con la etiqueta, etc.) deben ajustarse con train dentro de cada fold. La imputación y la codificación ya están incorporadas al pipeline; no calcular esas estadísticas sobre todo el CSV. Revisar duplicados antes de partir para evitar copias del mismo registro en train y test; el identificador de fila no es un identificador de conductor. Si se identifican grupos de un mismo conductor, reconsiderar la partición para mantenerlos separados.

Aplicar las mismas reglas de preparación al archivo externo sin etiqueta, conservando su número de filas y orden. No usarlo para escoger decisiones de limpieza ni modelos.

## Evaluación comparable

1. Cada notebook ordena por `id_fila` y filtra su cupón. Se usa 80 % train y 20 % test estratificado con semilla 42. Los tres modelos de un cupón deben usar el mismo CSV, predictores y configuración. Los dos cupones tienen conjuntos distintos: comparar sus métricas de forma descriptiva, considerando sus distribuciones.
2. La búsqueda se hace en train mediante cinco folds estratificados y un pipeline. Se exploran todos los hiperparámetros mínimos del enunciado. No ignorar advertencias de convergencia en regresión.
3. Se elige por **F1 macro de CV**, que da igual peso a ambas clases. Reportamos además precisión, recall y F1 de `Sí` y recall de la clase minoritaria definida en train. El F1 binario de aceptación y el F1 macro son métricas distintas; nombrarlas siempre.
4. Para Restaurante se compara sin balanceo frente a **SMOTE**, siguiendo la práctica 9, con la misma grilla y folds. El muestreo ocurre dentro de ImbPipeline, solo en train. Test permanece intacto. Se escala temperatura en ambas variantes de Restaurante porque SMOTE utiliza distancias; mantener ese paso en ambas evita cambiar dos factores simultáneamente. A diferencia del vino de la práctica, aquí hay categorías: SMOTE sobre one-hot puede generar valores fraccionarios sin significado categórico directo. Documentar esta limitación al recomendar su uso. SMOTENC o sobremuestreo aleatorio son alternativas para una extensión; el experimento actual no presupone que SMOTE vaya a mejorar.
5. La variante se elige por CV antes de abrir test. Si desean cambiar esa regla para priorizar recall minoritario, acordarlo y codificarlo **antes** de mirar test. Comparar ambas métricas y justificar la recomendación de balanceo.
6. Al final se evalúan las variantes en test y se interpreta el modelo congelado. No modificar hiperparámetros, variables o umbrales en función de ese test. Si se experimenta de nuevo, hace falta una evaluación independiente.

En el Excel original, antes de la limpieza, Cafetería tiene 1.989 aceptaciones y 1.997 rechazos; Restaurante(<20), 1.962 aceptaciones y 814 rechazos. Son conteos descriptivos, **no resultados de modelos**. En Restaurante la minoritaria es `No`: medir solo recall de aceptación ocultaría si se detectan los rechazos. Recalcular tras la limpieza.

## Ejecutar

Desde la raíz del laboratorio, se recomienda un entorno aislado. Estos comandos no necesitan activar PowerShell ni actualizar el Anaconda global:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m jupyter lab
```

Elegir el kernel del entorno donde se instalaron las dependencias. Se corrigio el error de importacion de SMOTE en Anaconda actualizando imbalanced-learn de 0.10.1 a 0.11.0, compatible con el scikit-learn 1.3.0 instalado. Se verificaron los pipelines de los tres notebooks de Restaurante con SMOTE y una grilla reducida, usando ese mismo entorno.

Despues de actualizar una dependencia, reiniciar el kernel y ejecutar el notebook desde el principio. Para reproducir esta correccion en otro kernel con scikit-learn 1.3.0, ejecutar una vez en una celda:

```python
%pip install --no-deps imbalanced-learn==0.11.0
```

Si trabajan en Colab, subir la carpeta con README, notebooks y CSV, y ajustar el directorio de trabajo. La búsqueda de Random Forest puede tardar; se pueden ensayar grillas pequeñas para depurar, pero restaurar y justificar la grilla final antes de reportar resultados.

1. Preparar el CSV compartido y completar los nombres.
2. Revisar el código y las decisiones; adaptar lo necesario antes de ejecutar.
3. Ejecutar de principio a fin. Sin el CSV, el notebook se detiene con un mensaje que indica la entrada faltante.
4. Completar las justificaciones y conclusiones con evidencia obtenida. Guardar las salidas visibles.
5. Cada notebook exporta en `resultados/<cupon>_<algoritmo>/` métricas, CV, coeficientes o importancias, predicciones del test interno, partición y pipeline evaluado. Comparar los archivos particion.csv entre los tres algoritmos del mismo cupón y trabajar sobre la misma versión del CSV.

Se validaron el formato y la sintaxis y se ejecutaron los seis notebooks de principio a fin con datos artificiales de prueba y grillas reducidas, incluyendo faltantes, SMOTE, exportación y recarga del pipeline. También se comprobaron particiones iguales por cupón. No se usaron datos del laboratorio para entrenar ni se guardaron esas salidas en los notebooks entregados. Falta ejecutar con el CSV definitivo y las grillas completas; las pruebas técnicas no demuestran desempeño predictivo.

## Integración posterior y entregables

El notebook final se construye **después** de terminar y revisar estos experimentos. No basta con concatenar los seis archivos: debe quedar un documento que ejecute completo, sin configuraciones sobrescritas ni secciones repetidas.

Orden propuesto:

1. Portada con los dos nombres, contexto y objetivo.
2. Exploración de ambos cupones y justificación de la limpieza elaborada por ustedes.
3. Preparación y protocolo compartidos, con separación train/test.
4. Tres modelos de Cafetería y tres de Restaurante, con búsquedas documentadas.
5. Comparación de balanceo en Restaurante: F1 general claramente definido y recall minoritario, con recomendación.
6. Tabla de test de los seis modelos principales (identificar las variantes con balanceo) y selección argumentada por CV de un ganador por cupón. Mostrar precisión, recall y F1; añadir F1 macro y recall minoritario.
7. Variables relevantes e interpretación de reglas/importancias, sin atribuir causalidad.
8. Responder explícitamente las ocho preguntas de «Análisis de resultados» del enunciado. Esta actividad vale 30 %; no reemplazarla por tablas.
9. Reajustar cada pipeline ganador con todo su subconjunto etiquetado. Preparar las 20 filas de `Lab3_datos_Prueba.xlsx` con las mismas reglas, predecir con el ganador del cupón correspondiente y exportar `Lab3_datos_Prueba.csv` con las columnas originales, su orden y la etiqueta `acepta_cupon` en `Sí`/`No`. No incluir `id_fila` si no pertenece al archivo original.
10. Completar «Uso de herramientas de IA generativa»: herramienta y propósito, prompts principales, análisis crítico de al menos dos preguntas de la rúbrica y aportes propios.

Entregar un notebook **ejecutado** `.ipynb`, su `.html`, el CSV de predicciones y un video para Ruta Alpes de máximo tres minutos. Para HTML, cuando el documento final exista y esté ejecutado:

```powershell
python -m jupyter nbconvert --to html laboratorio_3_final.ipynb
```

Video sugerido: problema y datos (25 s), comparación y ganador de cada cupón (65 s), balanceo e interpretación (45 s), límites, sesgos y recomendación (45 s). Ajustar a sus resultados reales.

El enunciado fija la entrega el **19 de octubre a las 8:00 p. m.**, y pide registrar los dos integrantes en el grupo de Bloque Neón. Verificar el enlace de entrega con el docente.

## Uso de herramientas de IA generativa

Codex ayudó a interpretar los requisitos, proponer la división por cupón y generar estas plantillas. No realizó la limpieza ni obtuvo resultados de entrenamiento. Los notebooks incluyen el prompt principal resumido y espacios para que cada estudiante documente su evaluación crítica y contribuciones. No entregar esas secciones con marcadores pendientes.

## Archivo de preparacion compartido

procesamiento_datos.ipynb exporta datos_limpios.csv y datos_prueba_preparados.csv en data/procesados. Se excluyen vehiculo por su alta proporcion de faltantes, tiempo_cupon_mayor_5min por ser constante y direccion_opuesta por repetir de forma inversa la informacion de misma_direccion. Las mismas columnas se eliminan de la copia preparada de prueba. La imputacion por moda se aprende en los pipelines; los nulos de frecuencia permanecen en el CSV. Los valores originales de las categorias se conservan.
