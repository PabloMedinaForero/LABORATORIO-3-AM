# Entrega del laboratorio 3

Estudiantes:

- Pablo Medina Forero - 202323276.
- Santiago Serrano Perico - 202313958.

Archivos principales:

- laboratorio_3_final.ipynb: notebook integrado con exploracion, limpieza, seis modelos, balanceo, comparacion, analisis y generacion de predicciones.
- laboratorio_3_final.html: version para revisar sin ejecutar Python.
- Lab3_datos_Prueba.csv: archivo original de prueba con las 20 etiquetas predichas.
- guion_video.md: apoyo para grabar un video de menos de tres minutos.

Archivos de apoyo:

- comparacion_seis_modelos.csv y comparacion_todas_variantes.csv.
- detalle_predicciones.csv: incluye el modelo elegido y su puntaje por fila. No reemplaza el CSV de entrega.
- modelos/: pipelines reajustados con todos los datos etiquetados de cada cupon.

Para repetir la ejecucion, abrir el notebook desde la raiz del proyecto o desde entrega, conservando la carpeta data del proyecto. Usar un entorno compatible con las dependencias. Se verifico en Anaconda con scikit-learn 1.3.0 e imbalanced-learn 0.11.0.

La seleccion usa F1 macro de validacion cruzada. El mayor F1 macro de test de Restaurante corresponde a la regresion con SMOTE, pero se conserva el bosque elegido antes de consultar test.

Antes de subir:

- Revisar redaccion, nombres y que todas las salidas sean visibles.
- Grabar el video y confirmar que dure como maximo tres minutos.
- Confirmar el grupo y el enlace de entrega en Bloque Neon.
- La rubrica exige un registro de uso de IA. Esa seccion no se incluyo en el notebook final, conservando la instruccion anterior de retirarla; este requisito de la entrega sigue sin cubrirse.

Se entregan el notebook, el HTML, el CSV de predicciones y el video. Los archivos auxiliares sirven para revisar y reproducir el trabajo.
