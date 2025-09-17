# Comparativa: Filtro de Kalman, Filtro de Partículas y Filtro de Monte Carlo  

---

## Filtro de Kalman
El filtro de Kalman es un algoritmo recursivo que se utiliza para estimar el estado de un sistema dinámico cuando este se puede modelar de manera lineal y está afectado por ruido gaussiano. Representa el estado mediante la media y la covarianza, y en cada iteración realiza dos pasos: una predicción a partir del modelo dinámico y una corrección en función de la observación disponible. Su principal ventaja es que bajo estos supuestos resulta óptimo y muy eficiente, lo que lo hace ampliamente utilizado en áreas como la navegación con GPS, el control de aeronaves y la robótica. Sin embargo, se ve limitado cuando el sistema es no lineal o el ruido no es gaussiano. Para esos casos se emplean variantes como el Filtro de Kalman Extendido (EKF) o el Unscented (UKF).  

---

## Filtro de Partículas
El filtro de partículas es un método de estimación bayesiana secuencial que aproxima la distribución de probabilidad del estado mediante un conjunto de muestras aleatorias llamadas partículas, cada una con un peso asociado. Estas partículas representan diferentes hipótesis sobre el estado real y se actualizan en cada paso usando el modelo dinámico y las observaciones. Con el proceso de remuestreo (*resampling*) se evita que unas pocas partículas dominen la representación, lo que se conoce como degeneración. Este método es más flexible que el de Kalman, ya que puede trabajar con sistemas no lineales y distribuciones no gaussianas. Su desventaja principal es el alto costo computacional, ya que la precisión mejora al aumentar el número de partículas. Se utiliza mucho en aplicaciones como SLAM en robótica, visión por computador y seguimiento de objetos.  

---

## Filtro de Monte Carlo
El método de Monte Carlo no es un filtro en sí, sino una técnica general que se basa en generar un gran número de muestras aleatorias para aproximar distribuciones o resolver integrales difíciles de calcular de manera analítica. Es muy flexible, ya que no requiere suposiciones estrictas sobre el sistema ni sobre la forma de la distribución. Sin embargo, puede necesitar una gran cantidad de simulaciones para alcanzar una buena precisión, lo que lo hace costoso en términos de cálculo. Se utiliza en problemas variados como la estimación de constantes matemáticas (por ejemplo, π), en simulaciones físicas y en finanzas.  

---

## Tabla comparativa

| Característica                | **Filtro de Kalman**                                                  | **Filtro de Partículas**                                                      | **Filtro de Monte Carlo**                                                           |
| ----------------------------- | --------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **Base teórica**              | Estimación bayesiana con **linealidad + gaussianidad**                | Estimación bayesiana con **partículas y pesos**                               | Método general de **muestreo aleatorio**                                            |
| **Representación del estado** | Media y covarianza (gaussiana)                                         | Conjunto de partículas ponderadas                                             | Conjunto de muestras aleatorias (no siempre con pesos)                              |
| **Modelo del sistema**        | Lineal con ruido gaussiano                                            | **No lineal y no gaussiano**                                                  | Cualquier modelo (flexible)                                                         |
| **Costo computacional**       | Muy bajo, rápido en tiempo real                                       | Alto (depende de # de partículas)                                             | Alto si se requieren muchas simulaciones                                            |
| **Precisión**                 | Óptima en lineal + gaussiano                                         | Aproximada (mejora con más partículas)                                        | Aproximada (mejora con más muestras)                                                |
| **Ventajas**                  | Rápido, matemáticamente óptimo, muy usado en ingeniería               | Flexible, maneja no linealidad y distribuciones complejas                     | General, adaptable a cualquier problema                                             |
| **Desventajas**               | Limitado a lineal y gaussiano (salvo EKF, UKF)                       | Costoso en cómputo, degeneración si pocas partículas                          | Puede requerir muchas muestras para buena precisión                                 |
| **Ejemplos de uso**           | GPS + INS, navegación de robots, aeronáutica                         | SLAM, seguimiento de objetos, visión por computador                           | π, finanzas, simulaciones físicas                                                   |

---

## Relación entre métodos
Los tres métodos están relacionados de manera jerárquica. El filtro de Kalman es un caso particular, óptimo en sistemas lineales con ruido gaussiano. El método de Monte Carlo es una técnica más general de muestreo aleatorio que sirve de base para otros enfoques. El filtro de partículas es, de hecho, una aplicación específica de Monte Carlo al problema de filtrado bayesiano, lo que le permite trabajar en contextos más complejos que los abordados por Kalman.  
