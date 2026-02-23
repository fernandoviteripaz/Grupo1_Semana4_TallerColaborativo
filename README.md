Análisis Interpretativo
Transparencia del Modelo:
La transparencia técnica del modelo se identifica como moderada; se logra explicar, con herramientas como LIME, cómo se descomponen las decisiones locales del modelo en factores comprensibles, con rangos de edad o tipos de afiliación específicos, hacia el estado final de las citas, es decir, si hubo cumplimiento o insistencia.

Riesgos éticos y sociales si se implementa el sistema:
Se identificaron 3 riesgos principales:
1. Sesgo debido al tipo de afiliación: esto quiere decir que el modelo puede aprender y perpetuar desigualdades basadas en el nivel socioeconómico. Cuando el Tipo de Afiliación es una variable principal, el sistema puede priorizar o penalizar a ciertos grupos basados en el tipo de afiliación que pudieron adquirir.
2. Discriminación por Edad o Género: las distribuciones en el modelo fueron visualizadas en el análisis exploratorio; en caso de que el modelo asocie erróneamente el incumplimiento de ctias con género o edad específicos, podría generar sesgos en el acceso a la salud para esos grupos.
3. Deshumanización: ejecutar tareas como gestión de citas de manera automatizadas basados en parámetros como probabilidades de asistencia sin considerar factores como problemas en transporte o emergencias, podría afectar el acceso a los servicios médicos.

Consideraciones para mejorar el modelo:
1. Inclusión de variables externas para automatizaciones: el uso de datos como clima, tráfico o ubicación del paciente puede ayudar a entender las causas del incumplimiento de citas.
2. Balanceo de datos: asegurar que las clases para la interpretación del estado final de la cita estén equilibradas para evitar que el modelo sesgue hacia clases mayoritarias.
3. Monitoreo del modelo: implementar sistemas de auditoría para analizar sesgos y detectar si el modelo comienza a discriminar a grupos vulnerables con el tiempo.

Reflexión sobre el proceso
¿Qué aprendizaje desarrolló sobre cómo el modelo toma decisiones?:
Se aprendió que el tipo de decisiones del modelo no es lineal, sino que analiza varias características de manera simultánea; adicionalmente, LIME nos ayuda a ver que, para predicciones de variables como Tipo de Afiliación, dentro de ciertos rangos de edad, como por ejemplo menor a 29 años, actúan basados en la probabilidad de la clase final, dado que el modelo busca patrones históricos en las combinaciones para seleccionar un resultado y darle su peso.

¿Hay alguna variable que tenga un peso excesivo?:
Basados en el análisis  de explicación de variables, vimos que TIPO_ESPECIALIDAD y ESPECIALIDAD parecen tener influencia significativa en los resultados de las predicciones en el modelo. Se puede tener como ejemplo que el rango de afiliación marca un peso negativo de 0.19, marcando un factor determinante para esa predicción.

¿Qué pasaría si este modelo se implementa sin explicabilidad?:
Esto podría generar problemas como falta de confianza dado que personal administrativo y médicos, no entenderían por que el sistema marcaría a un paciente como propenso a no asistir. Otro problema sería la falta de capacidad para corregir errores, el modelo tomaría decisiones basados en sesgos, y no se sabría como identificar que variable causa esto y ajustarla. Finalmente, el paciente no tendría una justificación clara de por qué se le ha negado una cita basada en una predicción automatizada.
