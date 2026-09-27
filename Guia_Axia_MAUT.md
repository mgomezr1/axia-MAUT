# Axía MAUT

Guía de instalación, uso y documentación técnica de la aplicación `index.html` para aplicar la Teoría de la Utilidad Multiatributo (MAUT) con modelo aditivo. Versión 1.0.

Este aplicativo fue desarrollado por Mario Sergio Gómez Rueda. Su uso es de carácter académico y cualquier otro uso se regirá por el derecho de la propiedad intelectual. Sugerencias o dudas: mgomezr1@gmail.com

## 1. Descripción general

`index.html` es una aplicación web de un solo archivo construida con HTML5, CSS3 y JavaScript. Todos los cálculos ocurren en el navegador y los datos nunca salen del equipo del usuario. La única dependencia externa es SheetJS (`https://cdn.sheetjs.com/xlsx-0.20.3/package/dist/xlsx.full.min.js`), que se usa solo para generar el libro Excel. El informe PDF se genera con código propio y no necesita librerías ni conexión.

El número de criterios (k) y de alternativas (m) lo define el usuario. Tablas, pestañas, curvas, hojas de Excel y páginas del PDF se construyen con ciclos a partir de k y m.

Configuración del método:

| Elemento | Opción implementada |
|---|---|
| Modelo de agregación | Aditivo: U(a) = Σ w_j · u_j(x_aj) |
| Funciones de utilidad | Lineal, exponencial, por tramos y discreta por niveles |
| Pesos | Digitados por el usuario; deben sumar 1 (hay un botón para normalizarlos) |
| Sentido de cada criterio | Maximizar o Minimizar (en los criterios discretos no aplica) |
| Rango de cada función | Automático (peor y mejor desempeño observados) o manual |
| Robustez | Sensibilidad de un peso a la vez, intervalos de estabilidad exactos y dominancia |

La aplicación distingue dos orígenes de datos, visibles en la portada, en los resultados, en el Excel y en el PDF: «Datos digitados por el usuario» y «Datos de prueba generados por la aplicación». Los archivos exportados con datos de prueba llevan el prefijo `PRUEBA_`.

El nombre, la versión, el autor, el correo y la nota de uso están en una sola constante (`APLICATIVO`, al inicio del JavaScript). Si se cambian allí, se actualizan la interfaz, la cita, el Excel y el PDF.

**El nombre.** ἀξία (axía) significa valor en griego: lo que algo vale para quien decide. Mantiene la línea de nombres griegos del portafolio (Kairós AHP, Áristos ELECTRE, Éngista TOPSIS, Métron, Kíndynos VaR, Seismos).

## 2. Cómo guardar el archivo

1. Descargue `index.html`.
2. Guárdelo en una carpeta de su equipo, por ejemplo `Documentos/Axia_MAUT/`.
3. Conserve la extensión `.html`. Si lo edita, use un editor de texto plano y guarde con codificación UTF 8.

## 3. Cómo ejecutarlo

1. Haga doble clic en `index.html` o arrástrelo a una ventana de Chrome, Edge, Firefox o Safari recientes. También funciona publicado en GitHub Pages.
2. Para exportar a Excel se necesita conexión a internet la primera vez, porque el navegador descarga SheetJS. Sin conexión funcionan la configuración, los cálculos, la sensibilidad, la verificación y el informe PDF.
3. No requiere instalar nada ni ejecutar un servidor.

Uso sin conexión (opcional): descargue una vez `xlsx.full.min.js` de la dirección anterior, guárdelo junto a `index.html` y cambie la etiqueta del encabezado por `<script src="xlsx.full.min.js"></script>`.

## 4. Estructura de la interfaz

| Sección | Contenido |
|---|---|
| Riel lateral | Nombre, siete pasos y «Acerca de Axía», con un punto verde cuando el paso está listo o naranja cuando requiere atención. En tabletas y teléfonos se convierte en barra superior |
| Portada | Nombre, lema, origen de los datos, botón «Limpiar aplicación» y el explorador de utilidad |
| Cómo funciona MAUT | Cuatro pasos, diagrama del flujo desempeño → utilidad → peso → suma, y los supuestos del método |
| 1. Configuración | Objetivo, número de criterios y de alternativas, y nombres de las alternativas |
| 2. Criterios, sentido y pesos | Tabla única con nombre, unidad, sentido, peso y tipo de función; suma de pesos en vivo; botón para normalizar; guía para elegir la función |
| 3. Funciones de utilidad | Una pestaña por criterio con sus parámetros y la curva en vivo, donde se marcan las alternativas |
| 4. Matriz de desempeño | Valores en unidad original (o nivel, en los discretos); cada celda se tiñe según su utilidad |
| 5. Resultados | Ocho bloques: configuración, criterios, desempeño, utilidades, aportes, gráfico de composición, clasificación y calidad del análisis |
| 6. Sensibilidad | Escenario puntual o barrido del peso de un criterio, intervalos exactos, gráfico interactivo y tabla de escenarios |
| 7. Exportación | Excel y PDF |
| Acerca de Axía | El nombre, versión y autoría; validación con botón «Ejecutar verificación», estado y desplegables «Ver pruebas técnicas» y «Escenarios de prueba»; debajo, «Referencias» y «Cómo citar» |

### Explorador de la portada

Muestra la función de utilidad de la TIR de un proyecto entre 5 % (peor nivel) y 25 % (mejor nivel). Un control cambia la forma de la curva (coeficiente c) y otro la TIR. La aplicación dice qué utilidad tiene esa TIR y compara lo que aporta pasar de 5 % a 10 % frente a pasar de 20 % a 25 %. Se maneja con ratón o con las flechas del teclado y no afecta los datos del modelo.

### Identidad visual

Modo oscuro sobre un índigo profundo, sin bordes visibles: las superficies se separan por contraste de tono y sombras suaves. El par de colores tiene significado: **coral** es el peor nivel de un criterio (utilidad 0) y **lima** el mejor (utilidad 1). Ese par tiñe la curva de la portada, las curvas de cada criterio, las celdas de desempeño y la matriz de utilidades. Toda la paleta y las medidas están en variables de `:root`. No se enlaza ninguna fuente externa; el bloque `@font-face` comentado permite cargar fuentes propias desde una carpeta `fuentes`.

### Validación restaurable

«Ejecutar verificación» corre las pruebas con escenarios internos. Antes de empezar guarda una instantánea de la pantalla (formulario, criterios, desempeño, resultados y sensibilidad) y al terminar la restaura, de modo que el usuario encuentra su trabajo como lo dejó.

## 5. Exportación a Excel

| Hoja | Contenido |
|---|---|
| `Menu` | Datos del análisis, índice con enlace a cada hoja, software, autor, contacto, nota de uso y advertencia si los datos son de prueba |
| `Criterios` | Sentido, peso (con fórmula de suma), función, peor y mejor nivel, parámetros y enlace a su hoja |
| `Desempeno` | Matriz de desempeño en unidades originales |
| `U01_<criterio>`, `U02_<criterio>`, … | Una hoja por función de utilidad |
| `Agregacion` | Utilidades, pesos, utilidad global con `SUMPRODUCT` y aportes ponderados |
| `Resultado` | Clasificación, estabilidad de la recomendación y dominancia |

Cada hoja de utilidad tiene los parámetros y una tabla por alternativa con fórmulas reales:

| Función | Fórmula de la utilidad en Excel |
|---|---|
| Lineal | `=MAX(0,MIN(1,z))` con `z = (x − peor)/(mejor − peor)` |
| Exponencial | `=IF(ABS(c)<1E-9, z, (1-EXP(-c*z))/(1-EXP(-c)))` sobre z acotado |
| Por tramos | Interpolación lineal entre los dos nodos del tramo que contiene z, con los nodos en la misma hoja |
| Discreta | `=VLOOKUP(nivel, tabla de niveles, 2, FALSE)` |

El desempeño de cada hoja se toma con una referencia a `Desempeno`, las utilidades de `Agregacion` refieren a cada hoja U y los pesos a `Criterios`, de modo que el estudiante puede seguir el cálculo celda por celda. Las fórmulas guardan también su valor.

## 6. Informe ejecutivo en PDF

Documento tamaño carta con:

1. **Objetivo y recomendación:** alternativa recomendada y su utilidad, diferencia con la segunda, criterio de mayor peso, criterio que más aporta a la ganadora, robustez y dominancia.
2. **Clasificación** con barras.
3. **Criterios, pesos y funciones.**
4. **Funciones de utilidad:** una gráfica por criterio con la curva, la referencia lineal y las alternativas.
5. **Aportes a la utilidad global.**
6. **Calidad y robustez:** diferencia entre primero y segundo, dominadas, valores recortados, menor cambio de peso que altera la ganadora e intervalos de estabilidad.
7. **Nota metodológica, referencias y recuadro de autoría.**

Cada página lleva pie con «Axía MAUT versión 1.0 | Desarrollado por Mario Sergio Gómez Rueda | Uso académico | mgomezr1@gmail.com», la frase de propiedad intelectual y «Página x de n», y una marca de agua diagonal translúcida «USO ACADÉMICO».

## 7. Fundamento de cálculo

**Normalización.** Para cada criterio numérico, z = (x − x⁰)/(x¹ − x⁰), donde x⁰ es el peor nivel y x¹ el mejor. Al minimizar, x⁰ > x¹ y la fórmula sigue valiendo 0 en el peor nivel y 1 en el mejor. Si el rango es manual y un desempeño queda fuera, z se acota a [0, 1] y se avisa.

**Rango automático.** Al maximizar, x⁰ = mínimo observado y x¹ = máximo; al minimizar, al revés. Si todos los valores son iguales el criterio no discrimina y se pide un rango manual.

**Lineal.** u(z) = z.

**Exponencial** (Kirkwood, 1997): u(z) = (1 − e^(−c·z)) / (1 − e^(−c)), con u(z) = z si c = 0. Con c > 0 la curva es cóncava (las primeras mejoras valen más); con c < 0, convexa. Equivale a la forma de Kirkwood con constante exponencial ρ = (x¹ − x⁰)/c. Se limita |c| ≤ 50 para evitar desbordes.

**Punto medio de valor.** Si el usuario indica el desempeño x_m que vale 0,5, se calcula z_m y se resuelve u(z_m; c) = 0,5 por bisección (u es creciente en c). Si z_m = 0,5 entonces c = 0.

**Por tramos.** Nodos (0, 0), (z_i, u_i) y (1, 1), con z estrictamente creciente y u no decreciente; la utilidad se interpola linealmente entre nodos. Así se representa el método de bisección de von Winterfeldt y Edwards (1986).

**Discreta.** Cada nivel tiene una utilidad entre 0 y 1. Si el peor nivel no vale 0 o el mejor no vale 1, la aplicación advierte que el peso pierde su significado de «valor de ir del peor al mejor nivel».

**Pesos.** No negativos, con |Σw − 1| ≤ 0,0001; se usan divididos por su suma. Un peso cero se advierte.

**Agregación.** U(a) = Σ_j w_j · u_j(x_aj); aporte_aj = w_j · u_aj. Las alternativas se ordenan de mayor a menor U y los empates (diferencia menor que 10⁻⁹) comparten posición.

**Dominancia.** a domina a b si u_aj ≥ u_bj en todos los criterios con peso positivo y es estrictamente mejor en al menos uno.

**Sensibilidad.** Al fijar en x el peso del criterio c, los demás se ajustan como w_j · (1 − x)/Σ_{i≠c} w_i (reparto igual si todos eran 0). Como U_a(x) es lineal en x, los puntos donde cambia la ganadora se calculan de forma exacta. El «menor cambio de peso» es la distancia desde el peso actual al punto crítico más cercano, sobre todos los criterios.

## 8. Explicación de las funciones

| Función | Qué hace |
|---|---|
| `interpretarNumero` | Convierte texto en número (punto o coma decimal); rechaza separadores mezclados |
| `normalizarDesempeno` | Calcula z |
| `utilidadExponencial`, `utilidadTramos`, `segmentoTramos`, `nodosTramos` | Funciones de utilidad y apoyo para tramos |
| `resolverCoeficienteExponencial` | c a partir del punto medio de valor |
| `evaluarUtilidad` | Utilidad de un desempeño según la función; informa si se recortó |
| `construirFuncion` | Valida la definición de un criterio y devuelve la función numérica, errores y advertencias |
| `validarPesos` | Suma, signos y ceros de los pesos |
| `calcularModelo` | Utilidades, aportes, utilidad global, ranking, dominancia, brecha y recortes |
| `calcularDominancia`, `ordenarAlternativas`, `agregarUtilidades` | Piezas del cálculo |
| `ajustarPesos`, `calcularIntervalosSensibilidad`, `realizarAnalisisSensibilidad`, `resumirEstabilidad` | Sensibilidad y robustez |
| `solicitarConfiguracion`, `confirmarConfiguracion`, `renderizarTablaCriterios`, `normalizarPesosInterfaz` | Pasos 1 y 2 |
| `renderizarFunciones`, `renderizarPanelFuncion`, `actualizarVistaFuncion`, `dibujarCurvaUtilidad`, `calcularCoeficienteDesdeMedio` | Paso 3 |
| `renderizarMatrizDesempeno`, `actualizarColumnaDesempeno`, `tinteUtilidad` | Paso 4 |
| `construirModeloDesdeEstado`, `calcularResultados`, `renderizarResultados`, `renderizarGraficoAportes` | Cálculo y resultados |
| `renderizarSensibilidad`, `renderizarGraficoSensibilidad` | Paso 6 |
| `crearHojaMenu`, `crearHojaCriterios`, `crearHojaDesempeno`, `crearHojaUtilidad`, `crearHojaAgregacion`, `crearHojaResultado`, `crearLibroResultados` | Libro Excel |
| `DocumentoPDF`, `dibujarCurvasPDF`, `generarInformePDF` | Informe PDF |
| `obtenerEscenarioPrueba`, `cargarEscenarioPrueba`, `tomarInstantanea`, `restaurarInstantanea`, `ejecutarPruebas` | Escenarios y verificación |

## 9. Ejemplo de uso con resultados verificados

Datos ficticios, disponibles como «Prueba 3» en «Escenarios de prueba». Objetivo: seleccionar el proyecto de inversión más conveniente.

| Criterio | Sentido | Peso | Función | Rango |
|---|---|---|---|---|
| TIR (%) | Maximizar | 0,35 | Exponencial, c = 1,5 | 5 a 25 |
| Inversión inicial (millones COP) | Minimizar | 0,25 | Lineal | 1.200 a 400 |
| Riesgo | Por niveles | 0,25 | Discreta: Alto 0; Medio 0,55; Bajo 1 | No aplica |
| Plazo de recuperación (años) | Minimizar | 0,15 | Por tramos: (6,5; 0,45), (5; 0,75), (3,5; 0,92) | 8 a 2 |

| Alternativa | TIR | Inversión | Riesgo | Plazo |
|---|---|---|---|---|
| Proyecto Solar | 18 | 950 | Medio | 6 |
| Proyecto Logístico | 14 | 600 | Bajo | 4,5 |
| Proyecto Digital | 23 | 1.100 | Alto | 3 |
| Proyecto Inmobiliario | 11 | 500 | Bajo | 7 |

Utilidades y resultado:

| Alternativa | u TIR | u Inversión | u Riesgo | u Plazo | U global | Posición |
|---|---|---|---|---|---|---|
| Proyecto Logístico | 0,6318 | 0,7500 | 1,0000 | 0,8067 | **0,7796** | 1 |
| Proyecto Inmobiliario | 0,4665 | 0,8750 | 1,0000 | 0,3000 | 0,6770 | 2 |
| Proyecto Solar | 0,8017 | 0,3125 | 0,5500 | 0,5500 | 0,5787 | 3 |
| Proyecto Digital | 0,9535 | 0,1250 | 0,0000 | 0,9467 | 0,5070 | 4 |

Diferencia entre el primero y el segundo: 0,1026. La ganadora se mantiene con cualquier peso de Riesgo; cambia a Proyecto Digital si el peso de TIR supera 0,648 o el de Plazo supera 0,712, y a Proyecto Inmobiliario si el de Inversión supera 0,588. El menor cambio de peso que altera la ganadora es 0,298, en TIR.

Estos valores se verificaron de forma independiente con NumPy y recalculando el libro Excel con LibreOffice.

## 10. Pruebas automáticas

«Ejecutar verificación» corre 17 pruebas:

1. Interpretación de números con punto, coma, signo y errores.
2. Función lineal al maximizar y minimizar, y recorte fuera de rango.
3. Función exponencial: u(0,5; c = 1) = 0,622459, límite lineal, concavidad, convexidad y simetría.
4. Punto medio de valor en cinco casos y rechazo fuera de (0, 1).
5. Función por tramos: nodos, interpolación y validación del orden y del rango.
6. Función discreta: búsqueda del nivel, límites, niveles repetidos y aviso de escala.
7. Pesos y rango automático: suma, negativos, ceros, coherencia con el sentido.
8. Prueba 1 contra la solución analítica: U = 0,72 y 0,66.
9. Prueba 2 con funciones mezcladas contra fórmulas escritas aparte.
10. Prueba 3 con las cuatro funciones contra fórmulas escritas aparte.
11. 54 modelos aleatorios con k de 2 a 12 y m de 2 a 10.
12. Dominancia, recorte y ranking con empates.
13. Sensibilidad: pesos que suman 1 y puntos críticos confirmados numéricamente.
14. Excel: número y orden de hojas, enlaces válidos del menú, SUMPRODUCT, EXP, BUSCARV y ranking.
15. PDF: xref, longitudes de flujos, páginas, pie, numeración y marca de agua en todas las páginas.
16. Formatos: coma decimal, colores de utilidad y conversión de texto para el PDF.
17. Interfaz: el escenario cargado en pantalla coincide con el cálculo directo.

Escenarios de prueba (ficticios): 2 × 2 lineal, 3 × 4 mixto, proyecto de inversión 4 × 4, dominancia con recorte y un modelo de 8 criterios y 10 alternativas generado con semilla fija.

## 11. Verificación realizada

| Verificación | Resultado |
|---|---|
| Pruebas automáticas | 17 de 17 aprobadas en Chromium, sin errores ni advertencias en la consola |
| Flujo manual en navegador | Configuración, criterios, cálculo de c por punto medio, desempeño, resultados, sensibilidad, Excel y PDF |
| Restauración tras la verificación | La pantalla vuelve al estado previo |
| Cálculo independiente | NumPy reproduce las utilidades globales del ejemplo con 6 decimales |
| Excel | 117 fórmulas recalculadas con LibreOffice, sin diferencias con los valores guardados |
| PDF | qpdf sin errores; 4 páginas revisadas visualmente |
| Diseño adaptable | Sin desplazamiento horizontal a 390 y 400 px |

Nota: el entorno de verificación no tenía acceso a `cdn.sheetjs.com`, por lo que el Excel se probó con SheetJS 0.18.5, que expone las mismas funciones. El archivo entregado carga la versión 0.20.3.

## 12. Limitaciones y supuestos discutibles

1. Solo modelo aditivo. Si las preferencias entre criterios no son independientes, la suma ponderada no las representa; el modelo multiplicativo de Keeney y Raiffa no está implementado.
2. Los desempeños son ciertos. Las funciones son, en rigor, funciones de valor; la lectura de c como aversión al riesgo solo aplica con loterías, que la aplicación no maneja.
3. Los pesos se digitan directamente. No se incluyen métodos de elicitación como swing o compensaciones; el usuario debe cuidar que cada peso refleje el valor de ir del peor al mejor nivel de su rango.
4. Con rango automático, agregar o quitar alternativas cambia las utilidades y puede invertir el orden de otras alternativas.
5. La sensibilidad mueve un peso a la vez y deja fijas las funciones de utilidad.
6. Una sola persona decide; no hay agregación de grupo.
7. Los datos viven en la memoria del navegador y se pierden al recargar; conserve el trabajo exportando.
8. El PDF usa fuentes estándar: algunos símbolos se escriben con letras (Σ como «suma»).
9. Por rendimiento se admiten hasta 60 criterios o alternativas; se recomienda no superar unos 10 criterios.

## 13. Referencias

Belton, V., & Stewart, T. J. (2002). *Multiple criteria decision analysis: An integrated approach*. Kluwer Academic Publishers. https://doi.org/10.1007/978-1-4615-1495-4

Keeney, R. L., & Raiffa, H. (1976). *Decisions with multiple objectives: Preferences and value tradeoffs*. John Wiley & Sons.

Kirkwood, C. W. (1997). *Strategic decision making: Multiobjective decision analysis with spreadsheets*. Duxbury Press.

von Winterfeldt, D., & Edwards, W. (1986). *Decision analysis and behavioral research*. Cambridge University Press.
