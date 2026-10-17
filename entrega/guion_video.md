# Guion para el video - Ruta Alpes

Duracion objetivo: entre 2:30 y 3:00 minutos. Ensayar antes de grabar y ajustar el ritmo para no superar el limite.

## 0:00 a 0:25 - Problema y datos

Somos Pablo Medina Forero y Santiago Serrano Perico. Estudiamos como Ruta Alpes puede anticipar la aceptacion de cupones de Cafeteria y Restaurante de menos de 20 dolares, para ofrecer promociones mas relevantes durante el trayecto.

Revisamos datos del conductor, sus habitos y el contexto de cada oferta. Eliminamos duplicados y variables constantes, redundantes o casi vacias. La imputacion y la codificacion se aprendieron solo con entrenamiento.

## 0:25 a 1:10 - Comparacion de modelos

Construimos una regresion logistica, un arbol y un bosque para cada cupon. Reservamos un test estratificado y elegimos los modelos por F1 macro en validacion cruzada, dando igual importancia a aceptaciones y rechazos.

El bosque fue seleccionado en ambos casos. En Cafeteria obtuvo F1 macro de test de 0.725 y en Restaurante, con SMOTE, de 0.685.

La regresion tuvo un F1 macro de test algo mayor en Restaurante. Conservamos la eleccion hecha por validacion para mantener el test como una evaluacion final. Los bosques muestran una diferencia importante entre entrenamiento y test, que limita la confianza en su generalizacion.

## 1:10 a 1:50 - Balanceo e interpretacion

En Restaurante predominan las aceptaciones. Con SMOTE, el bosque aumento el recall del rechazo de 35.2% a 45.7% y mejoro el F1 macro. Al mismo tiempo, el F1 de aceptacion bajo ligeramente. El balanceo implica un intercambio entre errores.

En Cafeteria destaca el habito de visitar cafeterias. En Restaurante destacan la vigencia y la hora. Los arboles permiten describir reglas: por ejemplo, en Restaurante, una oferta con un dia de vigencia y a no mas de 25 minutos lleva a aceptacion en las ramas del arbol ajustado.

## 1:50 a 2:35 - Recomendacion y limites

Recomendamos usar estos resultados como base para un piloto, junto con cercania, vigencia y limites de notificaciones. La aplicacion debe evitar distraer al conductor.

Edad, genero, ingreso y ocupacion pueden introducir diferencias entre grupos. Se deben revisar sus errores y proteger la privacidad antes de desplegar. Ademas, SMOTE sobre categorias codificadas puede generar valores fraccionarios; conviene contrastarlo con otras formas de balanceo.

Finalmente, reajustamos el ganador de cada cupon con todos sus datos etiquetados y generamos las 20 predicciones solicitadas. Las asociaciones encontradas apoyan la personalizacion, pero no prueban que enviar un cupon cause una compra.

## Apoyo visual

Mostrar la tabla de los seis modelos, la comparacion del recall de rechazo con SMOTE y una figura de importancia de variables. Evitar leer codigo durante el video.
