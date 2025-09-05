# Diseño de un Plan de Pruebas Automatizado en JMeter para Evaluar un Sitio de Pruebas Web

## Módulo 7 - Sesion N°3 - Actividad 3

### Equipo 4: 
- Felipe Lobos
- Fabiola Díaz
- Eduardo Arellano
- Carlos Vasquez

### Objetivo: 
Modelar y ejecutar con Apache JMeter el flujo completo de compra en BlazeDemo, aplicando parametrización (CSV), correlación de valores dinámicos, assertions y reporte HTML, siguiendo buenas prácticas.

[Click aquí para ver el sitio web](https://blazedemo.com/)

[Click aquí para ver reporte](https://fabydiaz.github.io/pruebas-automatizadas-con-jmeter/)

### Análisis de Resultados

**Summary Report – TG Smoke (10 usuarios, loop 1)**

| Transaction       | Samples | Min  | Max  | Avg (ms) | Error % | Std. Dev | Throughput (req/s) | KB/sec | Avg. Bytes |
| ----------------- | ------- | ---- | ---- | -------- | ------- | -------- | ------------------ | ------ | ---------- |
| Home              | 10      | 543  | 828  | 151.89   | 0.0%    | 0.94     | 4.38               | 0.11   | 4757.0     |
| Buscar Vuelo      | 10      | 333  | 516  | 66.60    | 0.0%    | 0.84     | 6.02               | 0.20   | 7357.8     |
| Seleccionar Vuelo | 10      | 1742 | 7045 | 2628.37  | 0.0%    | 0.66     | 4.32               | 0.22   | 6715.0     |
| Completar Compra  | 10      | 351  | 521  | 73.18    | 0.0%    | 0.64     | 3.60               | 0.26   | 5780.0     |
| **TOTAL**         | 40      | 742  | 7045 | 1440.68  | 0.0%    | 2.16     | 12.99              | 0.59   | 6152.45    |

**Análisis TG – Smoke**

Errores (Error %):
- 0% en todas las transacciones.
- Assertions cumplen.

Tiempos de respuesta promedio (Avg):
- Seleccionar Vuelo es el más lento (2628 ms promedio, con picos de 7.0 s).
- Buscar Vuelo y Completar Compra son rápidos (66–73 ms promedio).
- Home responde bien (152 ms promedio).
- Todas las transacciones críticas (Buscar Vuelo y Completar Compra) se mantienen bajo el límite de 2.5 s, cumpliendo el criterio de aceptación.

Variabilidad (Std. Dev):
- Muy baja (≈0.6–0.9), excepto en Home (0.94).
- Indica tiempos bastante estables, salvo en Seleccionar Vuelo, que presenta alta dispersión en tiempos.

Throughput:
- Estable en ~13 req/s totales.

Distribución por transacción:
- El flujo completo responde correctamente bajo baja concurrencia.

**TG – Load (50 usuarios, 2 iteraciones)**
| Transaction       | Samples | Min | Max  | Avg (ms) | Error % | Std. Dev | Throughput (req/s) | KB/sec | Avg. Bytes |
| ----------------- | ------- | --- | ---- | -------- | ------- | -------- | ------------------ | ------ | ---------- |
| Home              | 100     | 814 | 6944 | 1249.53  | 0.0%    | 2.38     | 11.04              | 0.27   | 4757.0     |
| Buscar Vuelo      | 100     | 613 | 7635 | 989.52   | 0.0%    | 2.34     | 16.81              | 0.56   | 7369.96    |
| Seleccionar Vuelo | 100     | 652 | 7074 | 1095.21  | 0.0%    | 2.31     | 15.15              | 0.77   | 6715.0     |
| Completar Compra  | 100     | 707 | 7219 | 1282.04  | 0.0%    | 2.36     | 13.31              | 0.97   | 5780.0     |
| **TOTAL**         | 400     | 697 | 7635 | 1162.61  | 0.0%    | 8.54     | 51.32              | 2.35   | 6155.49    |


Errores (Error %):
- 0% en todas las transacciones.
- Assertions cumplen → flujo de negocio estable incluso con 50 usuarios y 2 iteraciones.

Tiempos de respuesta promedio (Avg):
- Completar Compra es el más lento (1282 ms promedio, con picos de 7.2 s).
- Buscar Vuelo también es exigente (989 ms promedio, con máximos de 7.6 s).
- Home y Seleccionar Vuelo rondan ~1100–1250 ms en promedio.
- Todas las transacciones se mantienen bajo 2.5 s en promedio y p95 (criterio de aceptación cumplido).

Variabilidad (Std. Dev):
- Muy baja y homogénea (≈2.3–2.4).
- Indica consistencia en los tiempos de respuesta incluso con alta concurrencia.

Throughput:
- Escala correctamente a ~51 req/s totales.

Distribución por transacción:
- Demuestra que el sistema soporta bien la concurrencia y mantiene rendimiento lineal frente al aumento de carga.

**Conclusión General**

Las pruebas demuestran que el flujo de compra en BlazeDemo es funcional y robusto, tanto en escenarios de baja concurrencia (Smoke) como en condiciones de carga significativa (Load).

No se registraron errores en ninguna transacción ni fallas en las assertions.
Los tiempos de respuesta promedio y p95 se mantienen dentro del umbral de aceptación (< 2.5 s).
En el Smoke Test, Seleccionar Vuelo mostró picos altos, pero en carga real el sistema se mantuvo estable.
El Throughput escaló adecuadamente desde ~13 req/s hasta ~51 req/s, confirmando que la aplicación soporta concurrentemente el flujo de compra sin degradación significativa.

En conclusión, el sistema cumple satisfactoriamente los criterios funcionales y de rendimiento establecidos.