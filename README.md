# Axía MAUT

Aplicación web académica para tomar decisiones con la **Teoría de la Utilidad Multiatributo (MAUT)** de Keeney y Raiffa, con modelo aditivo: convierta el desempeño de cada alternativa en una utilidad entre 0 y 1, pondere los criterios y obtenga la utilidad global de cada alternativa.

**Abrir la aplicación:** https://mgomezr1.github.io/axia-MAUT/

No requiere instalación ni registro. Funciona en cualquier navegador moderno, en computador, tableta o teléfono.

## Qué permite hacer

- Definir el objetivo, los criterios y las alternativas, en la cantidad que necesite.
- Registrar en una sola tabla el sentido (Maximizar o Minimizar), el peso y el tipo de función de cada criterio.
- Construir funciones de utilidad lineales, exponenciales (con cálculo de c desde el punto medio de valor), por tramos o discretas por niveles, con la curva a la vista.
- Registrar el desempeño en la unidad original de cada criterio y ver su utilidad por color.
- Obtener utilidades, aportes ponderados, utilidad global, clasificación, dominancia e indicadores de robustez.
- Hacer análisis de sensibilidad y ver con qué pesos cambiaría la recomendación.
- Descargar un libro Excel con fórmulas reales y un informe ejecutivo en PDF.

## Cómo usarla

1. Lea «Cómo funciona MAUT» y juegue con el explorador de la portada.
2. En **Configuración**, escriba el objetivo, el número de criterios y de alternativas, y los nombres de las alternativas.
3. En **Criterios y pesos**, complete la tabla y confirme. Los pesos deben sumar 1.
4. En **Funciones de utilidad**, defina cada función; en **Desempeño**, digite los valores.
5. Pulse **Calcular resultados**, revise la robustez en **Sensibilidad** y descargue el **Excel** o el **PDF**.

En **Acerca de Axía** puede ejecutar la verificación automática y cargar escenarios de prueba con datos ficticios.

## Privacidad

Todos los cálculos se hacen en su navegador. Los datos no se envían a ningún servidor ni se guardan: al cerrar o recargar la página se pierden, así que descargue el Excel o el PDF antes de salir.

## Requisitos

- Navegador actualizado (Chrome, Edge, Firefox o Safari) con JavaScript activo.
- Conexión a internet para exportar a Excel, porque la aplicación descarga la biblioteca SheetJS. El informe PDF funciona sin conexión.

## Documentación

La guía completa (método, fórmulas, funciones, exportaciones, pruebas y limitaciones) está en [docs/Guia_Axia_MAUT.md](docs/Guia_Axia_MAUT.md). En [ejemplos](ejemplos) hay un libro Excel y un informe PDF generados con datos de prueba.

## Cómo citar

Gómez Rueda, M. S. (2026). *Axía MAUT* (Versión 1.0) [Software]. https://mgomezr1.github.io/axia-maut/

## Autoría y uso

Este aplicativo fue desarrollado por Mario Sergio Gómez Rueda. Su uso es de carácter académico y cualquier otro uso se regirá por el derecho de la propiedad intelectual. Consulte los términos en [LICENSE.md](LICENSE.md). Sugerencias o dudas: mgomezr1@gmail.com

## Fundamento metodológico

- Keeney, R. L., & Raiffa, H. (1976). *Decisions with multiple objectives: Preferences and value tradeoffs*. John Wiley & Sons.
- Kirkwood, C. W. (1997). *Strategic decision making: Multiobjective decision analysis with spreadsheets*. Duxbury Press.
- von Winterfeldt, D., & Edwards, W. (1986). *Decision analysis and behavioral research*. Cambridge University Press.
- Belton, V., & Stewart, T. J. (2002). *Multiple criteria decision analysis: An integrated approach*. Kluwer Academic Publishers. https://doi.org/10.1007/978-1-4615-1495-4

## Componentes de terceros

La exportación a Excel usa [SheetJS Community Edition](https://sheetjs.com), distribuida bajo la licencia Apache 2.0 y cargada desde cdn.sheetjs.com.
