# Análisis RFM de clientes · comercio electrónico

**Juan Luis León Rodríguez · Proyecto TechAcces · datos sintéticos**

[Español](#español) · [English](#english)

## Español

> Los datos son **sintéticos** y los genera el propio repositorio (`Script_Datos_Sinteticos.ipynb`).
> Las cifras de retorno de la última tabla ilustran cómo se presenta un caso de negocio. No son
> resultados de ninguna empresa.

### El problema

Tienes 946 clientes y 7.741 pedidos del último año. El lunes por la mañana hay que decidir a quién
llama el equipo comercial. Llamar a todos no cabe en la semana. ¿Por dónde empiezas? Casi todo el
mundo ordena por facturación y baja por la lista. Ese orden esconde justo lo que más caro sale.

En estos datos vive el cliente 1029. Compró veintidós veces y dejó 20.637 dólares, así que aparece
arriba en cualquier informe anual de ventas. Lleva dos meses sin volver. El acumulado de doce meses
no lo dice en ninguna parte. Ese acumulado mete en un solo número lo que pasó en junio y lo que pasó
la semana pasada; una vez sumado, las dos cosas ya no se distinguen. Cuando alguien se da cuenta,
ese cliente ya compra en otro sitio. El aviso llevaba meses escrito en las fechas de sus pedidos.
Nadie las lee. Recorrerlas una a una para 946 clientes no es trabajo de una persona.

Este repositorio toma esa lista de pedidos y la resume en tres números por cliente. Después reparte
la cartera en cinco grupos y propone una acción comercial para cada uno. El método se llama RFM. Lo
usa cualquier equipo de marketing con una base de clientes delante.

### Las tres letras

**RFM** son las iniciales inglesas de *recency*, *frequency* y *monetary*, o sea recencia,
frecuencia e importe. Son tres preguntas sobre cada cliente. Las tres se contestan con la lista de
pedidos que ya tienes.

| Número | La pregunta que contesta | Lo que sale en estos datos |
|---|---|---|
| **Recencia** | ¿Cuántos días hace que compró por última vez? | De 1 a 372 días, y menos días es mejor |
| **Frecuencia** | ¿Cuántas veces ha comprado? | Entre 1 y 30 pedidos, con una media de 8,2 |
| **Importe** | ¿Cuánto ha dejado en total? | Desde 77 hasta 41.889 dólares, con la mitad de la cartera por debajo de 1.870 |

Ninguna de las tres vale por su cuenta. Mirando la frecuencia sin la recencia sale un cliente fiel
que ya se fue. Mirando el importe sin las otras dos sale el que hizo una compra grande y nunca
volvió. Juntas cuentan la historia entera: cuánto vale cada cliente, cada cuánto viene y si sigue
viniendo.

### Por qué el corte lo pone la cartera

**Segmentar** es partir la cartera en unos pocos grupos. Dentro de un grupo los clientes se parecen
entre sí y a los de fuera no. Así se puede tratar a cada grupo de una manera. Nadie diseña una
campaña para 946 personas distintas, sino cuatro o cinco. Entonces toda la pregunta pasa a ser en
qué saco cae cada cliente.

¿Merece la pena partirla? En estos datos los 246 Champions son el 26 % de la cartera y el 66,5 % de
las ventas. Los 401 clientes de Nuevos y Otros juntos son el 42,4 % de la cartera. Entre todos se
quedan en el 3,8 % de las ventas. Repartir el mismo esfuerzo comercial por igual entre esos dos
bloques rinde de forma muy distinta.

Falta decidir dónde va la raya de cada grupo. Ahí se usan quintiles. **Quintil** se llama a cada una
de las cinco partes iguales en que se corta una lista ordenada. El quinto de clientes que más gasta
recibe un 5, el siguiente un 4, y así hasta el 1. Casi todo el mundo lo haría a ojo: cliente bueno
el que pasa de 5.000 dólares, cliente dormido el que lleva más de tres meses sin comprar. El
problema de esos números está en su origen, porque los pone alguien de memoria y valen para un
sector y no para otro. Y envejecen solos en cuanto suben los precios o cambia la estación.

Con quintiles el corte no se inventa, se lee de tu propia cartera. Los que salen en estos datos son
los siguientes:

| Corte | Recencia | Frecuencia | Importe |
|---|---|---|---|
| p20 | 13 días | 2 compras | 405 $ |
| p40 | 28 días | 4 compras | 1.246 $ |
| p60 | 59 días | 7 compras | 3.537 $ |
| p80 | 121 días | 13 compras | 8.489 $ |

Fíjate en la columna del importe. Esos 5.000 dólares que parecían el listón del buen cliente caen
entre 3.537 y 8.489. Queda en mitad del cuarto grupo de cinco, ni el mejor ni la media. Puesto a
mano, ese umbral habría llamado excelente a un cliente del montón.

### El código de tres cifras

Al pegar las tres puntuaciones sale un **código RFM**. El cliente 1108 tiene un `455`: compró hace
veintiséis días, veintinueve veces, y lleva gastados 41.889 dólares. Esa cifra es el máximo de toda
la cartera. Ese código se lee de un vistazo. Un `511` es alguien que acaba de estrenarse. Un `155`
es un cliente valioso que se está enfriando. Un `111` es alguien que se fue hace mucho y nunca
compró gran cosa.

El código decide el grupo con estas reglas, escritas en el propio cuaderno:

```
Champions → R>=4, F>=4, M>=4
Leales    → R>=3, F>=3, M>=3
Nuevos    → R>=4, F<=2
En riesgo → R<=2, F>=3, M>=3
Otros     → el resto
```

Ese orden importa. Cada cliente se queda en la primera regla que cumple.

### Los cinco grupos

| Segmento | Clientes | % | Valor promedio | Recencia | Frecuencia |
|----------|----------|---|----------------|---------|-----------|
| Champions | 246 | 26% | $15.447 | 12 días | 16,8 |
| Leales | 197 | 21% | $6.212 | 33 días | 9,3 |
| En riesgo | 102 | 11% | $4.587 | 96 días | 8,1 |
| Nuevos | 59 | 6% | $528 | 13 días | 2,5 |
| Otros | 342 | 36% | $550 | 144 días | 2,3 |

![Segmentación](01_segmentacion_barras.png)

El grupo más numeroso es Otros, con 342 clientes. El que sostiene el negocio es Champions. Medida
sobre estos datos, la diferencia de valor entre los dos es de 29,28 veces.

![Mapa RFM](02_rfm_scatter.png)

El mapa cruza los días que lleva sin comprar cada cliente con el dinero que ha dejado. Arriba a la
derecha, en amarillo, están los Champions, recientes y de alto gasto; en el centro, en gris, los
Leales; a la izquierda, en rojo, los que llevan meses callados. Abajo, en verde y azul, quedan
Nuevos y Otros.

### El cuaderno se comprueba a sí mismo

![Correlación](03_correlacion_heatmap.png)

El cuaderno pasa nueve verificaciones sobre su propio trabajo antes de dibujar nada. Que los
Champions tengan de media menos de treinta días sin comprar, que los Nuevos compren poco, que la
puntuación de recencia baje cuando los días suben. Las nueve salen en verde con los datos de hoy.

Tres de esas comprobaciones son correlaciones entre cada puntuación y el número del que sale. Una
**correlación** mide si dos cantidades se mueven a la vez, con un valor entre −1 y 1. El signo dice
en qué dirección y el tamaño dice cuánto.

- R_Score frente a recencia: −0,83, negativa porque a más días sin comprar, menor puntuación.
- F_Score frente a frecuencia: 0,87.
- M_Score frente a importe: 0,76.

### Qué está medido

Estas cifras salen de ejecutar el repositorio el 22 de julio de 2026. Se usaron Python 3.14.6 y
pandas 3.0.3. Las dos son bastante más nuevas que las versiones de su publicación.

| Comprobación | Resultado |
|---|---|
| El cuaderno de análisis se ejecuta entero | sí, 12,4 segundos, sin errores |
| Sus nueve verificaciones internas | las nueve en verde |
| Los tres gráficos regenerados | idénticos byte a byte a los publicados |
| El generador reproduce el fichero de datos | idéntico byte a byte |

Todas las cifras de esta portada se recalcularon además por una vía distinta. Un programa propio lee
el fichero de pedidos sin usar pandas. Coinciden los 946 clientes, los 7.741 pedidos y los cinco
grupos. Coinciden también sus medias y las tres correlaciones, hasta el último decimal.

### Lo que falla

**El generador de datos no arranca al clonarlo.** Pide un entorno de Python privado del ordenador de
su autor, llamado `conda-env-accident_agent-py`. Ese entorno es encima el de otro proyecto distinto.
Un cambio de julio arregló ese mismo defecto en el cuaderno de análisis. Al generador lo dejó como
estaba. Forzándole el intérprete a mano funciona y reproduce el fichero exacto, así que el fallo
está en la etiqueta y no en el programa.

**Una cuenta mal copiada dentro del cuaderno.** Su resumen afirma que los Champions gastan «3x más
que Leales, 28x más que Nuevos». Lo medido da 2,49 y 29,28. Ese 28 existe, pero contra el grupo
Otros. Se coló al pasarlo de un sitio a otro.

**La frontera del quintil es frágil por construcción.** El quintil compara a cada cliente contra los
demás, así que el corte se mueve cuando cambia la cartera. Dos clientes casi idénticos pueden caer a
lados distintos de la raya. Con sesenta días sin comprar, el cliente 1029 sale En riesgo; el 1120,
con cincuenta y nueve días y las mismas veintidós compras, sale Leal. Por un día de diferencia uno
recibe campaña de recuperación y el otro no.

**El cuaderno recalcula los cortes de quintil una vez por cada cliente** en lugar de una vez para
todos. Ese derroche se paga en cuanto la cartera crece.

| Clientes | Tiempo de puntuar cada columna |
|---|---|
| 946 | 0,7 segundos |
| 12.217 | 20 segundos |
| 64.000 | 232 segundos |

Esta portada prometía que el método aguanta más de 100.000 transacciones. A esa escala la promesa se
cumple, porque sale en poco más de un minuto. Donde falla es en una cartera de cientos de miles de
clientes. Cada vez que se dobla el número de clientes el tiempo se multiplica por tres. Pandas trae
una función que hace ese mismo reparto en dos milésimas de segundo a cualquier tamaño. El cuaderno
la ignora.

### Las acciones propuestas

Las tres acciones de abajo son un ejercicio. Enseñan cómo se presenta un caso de negocio a partir de
la segmentación. Antes de leerlas, conviene mirar su tamaño. Las ventas de los doce meses suman 5,71
millones de dólares. El impacto que se propone son 2,3 millones, o sea el 40 % de toda la
facturación. Solo el programa VIP promete subir un 55 % lo que gastan unos clientes. Esos clientes
ya son los que más gastan. Leerlas como una previsión de lo que va a pasar sería un error.

**Programa VIP para los 246 Champions.** Acceso anticipado de 48 horas, gestor de cuenta dedicado y
eventos por invitación. La devolución es del 5 % por encima de 5.000 dólares.

**Campaña de recuperación para los 102 clientes en riesgo.** Secuencia de correos de 30 días,
descuento del 25 % y retargeting. Retargeting es volver a mostrarle anuncios a quien ya visitó la
tienda.

**Primeros 90 días para los 59 clientes nuevos.** Correos automáticos, descuento creciente y
gamificación, o sea añadir mecánicas de juego a la relación con la marca.

| Acción | Inversión | Retorno | ROI |
|--------|-----------|---------|-----|
| VIP Champions | $50K | $2,1M | 42:1 |
| Reactivación | $5K | $160K | 32:1 |
| Onboarding | $10K | $42,5K | 4:1 |
| **TOTAL** | **$65K** | **$2,3M** | **35:1** |

### Cuándo no sirve

Aquí el dinero no es dinero. Los datos están inventados y los genera el propio repositorio. Sirven
para enseñar el método sin publicar clientes reales. Las cifras de retorno de la tabla anterior
ilustran una forma de presentar en vez de un resultado.

Tampoco el método lo explica todo, porque RFM mira ventas y nada más. Del margen de cada producto y
del coste de servir a cada cliente no sabe nada. El que más factura puede no ser el que más deja.
Tampoco dice por qué alguien se fue. Las incidencias, el trato recibido y lo que ofrece la
competencia no dejan rastro en una lista de pedidos.

### Estructura del proyecto

```
RFM-Customer-Analytics/
├── 01_Analisis_RFM_Completo.ipynb   # El análisis entero: RFM, segmentación y gráficos
├── Script_Datos_Sinteticos.ipynb    # El generador del dataset sintético
├── raw_data_12meses.csv             # Los 7.741 pedidos de 12 meses
├── raw_data.csv                     # Dataset auxiliar
├── 01_segmentacion_barras.png
├── 02_rfm_scatter.png
└── 03_correlacion_heatmap.png
```

Con abrir el cuaderno de análisis basta para entenderlo todo. Tarda doce segundos en ejecutarse.

### Cómo reproducirlo

Hacen falta Python 3.9 o superior y Jupyter. Estas son las dos órdenes que abren el cuaderno.

```bash
pip install pandas matplotlib seaborn
jupyter notebook 01_Analisis_RFM_Completo.ipynb
```

El cuaderno se ejecuta de arriba abajo. La primera celda carga los datos. Las siguientes calculan
los tres números y las puntuaciones. Después vienen las nueve verificaciones y al final los tres
gráficos.

### Repos relacionados

Este análisis es una pieza de un portfolio de casos de analítica. Estas son las piezas hermanas:

- [lead-scoring-ml](https://github.com/jleonceo/lead-scoring-ml): predecir qué lead acaba comprando, con modelos de clasificación.
- [accident-intelligent-agent](https://github.com/jleonceo/accident-intelligent-agent): ETL, exploración y modelo para predecir la gravedad de un accidente de tráfico.
- [analisis-contable](https://github.com/jleonceo/analisis-contable): análisis financiero de una empresa con Python, del libro diario a las conclusiones.

*Parte del portfolio de [Juan Luis León](https://github.com/jleonceo) · [juanluisleon.vercel.app](https://juanluisleon.vercel.app) · Licencia [MIT](LICENSE)*

## English

> The data is **synthetic** and generated by the repository itself (`Script_Datos_Sinteticos.ipynb`).
> The return figures in the last table illustrate how a business case is presented. They are not the
> results of any company.

### The problem

You have 946 customers and 7,741 orders from the last twelve months. On Monday morning someone has
to decide who the sales team calls. Calling everyone does not fit in the week. Where do you start?
Most people sort by revenue and work down the list. That order hides exactly what costs the most.

Customer 1029 lives in this data. They bought twenty-two times and left 20,637 dollars, so they show
up near the top of any annual sales report. They have not been back for two months. The twelve-month
total says that nowhere. That total puts what happened in June and what happened last week into one
number; once added up, the two are no longer distinguishable. By the time anyone notices, that
customer is buying elsewhere. The warning had been written in the dates of their orders for months.
Nobody reads those dates. Going through them one by one for 946 customers is not a job for a person.

This repository takes that order list, boils each customer down to three numbers, splits the base
into five groups and proposes a commercial action for each one. The method is called RFM. Any
marketing team with a customer base can use it.

### The three letters

**RFM** stands for recency, frequency and monetary value. They are three questions about each
customer, and all three are answered with the order list you already have.

| Number | The question it answers | What comes out in this data |
|---|---|---|
| **Recency** | How many days since the last purchase? | From 1 to 372 days, and fewer is better |
| **Frequency** | How many times have they bought? | Between 1 and 30 orders, averaging 8.2 |
| **Monetary** | How much have they spent in total? | From 77 to 41,889 dollars, with half the base below 1,870 |

None of the three is worth much on its own. Frequency without recency gives you a loyal customer who
already left. Monetary value without the other two gives you the one who made a big purchase and
never came back. Together they tell the whole story: how much a customer is worth, how often they
come and whether they still come.

### Why the cut-off comes from the data

**Segmenting** means splitting the customer base into a few groups. Members of a group resemble each
other and differ from those outside. That way each group can be handled its own way. Nobody designs
a campaign for 946 different people, they design four or five. The whole question becomes which
bucket each customer falls into.

Is splitting worth it? In this data the 246 Champions are 26% of the base and 66.5% of sales, while
the 401 customers in New and Others together account for 42.4% of the base and 3.8% of sales.
Spreading the same commercial effort evenly across those two blocks pays off very differently.

What remains is deciding where each group's line goes. That is the job of quintiles. A **quintile**
is each of the five equal parts an ordered list is cut into. The fifth of customers who spend most
get a 5, the next one a 4, and so on down to 1. Most people would do it by eye: a good customer
spends over 5,000 dollars, a dormant one has been quiet for more than three months. The trouble with
those numbers is where they come from, because somebody sets them from memory and they suit one
sector and not another. And they age on their own as soon as prices rise or the season turns.

With quintiles the cut-off is not invented, it is read off your own customer base. The ones that
come out in this data are the following:

| Cut-off | Recency | Frequency | Monetary |
|---|---|---|---|
| p20 | 13 days | 2 purchases | $405 |
| p40 | 28 days | 4 purchases | $1,246 |
| p60 | 59 days | 7 purchases | $3,537 |
| p80 | 121 days | 13 purchases | $8,489 |

Look at the monetary column. Those 5,000 dollars that looked like the bar for a good customer fall
between 3,537 and 8,489, that is, in the middle of the fourth group out of five, neither the best
nor the average. Set by hand, that threshold would have called an ordinary customer excellent.

### The three-digit code

Joining the three scores gives an **RFM code**. Customer 1108 has a `455`: they bought twenty-six
days ago, twenty-nine times, and have spent 41,889 dollars. That figure is the highest in the whole
base. The code reads at a glance. A `511` is somebody who has just started. A `155` is a valuable
customer going cold. A `111` is somebody who left long ago and never bought much.

The code decides the group with these rules, written in the notebook itself:

```
Champions → R>=4, F>=4, M>=4
Loyal     → R>=3, F>=3, M>=3
New       → R>=4, F<=2
At Risk   → R<=2, F>=3, M>=3
Others    → everything else
```

The order matters. Each customer stays in the first rule they satisfy.

### The five groups

| Segment | Customers | % | Average value | Recency | Frequency |
|---------|-----------|---|---------------|---------|-----------|
| Champions | 246 | 26% | $15,447 | 12 days | 16.8 |
| Loyal | 197 | 21% | $6,212 | 33 days | 9.3 |
| At Risk | 102 | 11% | $4,587 | 96 days | 8.1 |
| New | 59 | 6% | $528 | 13 days | 2.5 |
| Others | 342 | 36% | $550 | 144 days | 2.3 |

![Segments](01_segmentacion_barras.png)

The largest group is Others, with 342 customers. The one holding up the business is Champions.
Measured on this data, the gap in value between the two is 29.28 times.

![RFM map](02_rfm_scatter.png)

The map places each customer by days since the last purchase against money spent. Top right, in
yellow, sit the Champions, recent and high-spending. In the middle, in grey, the Loyal ones. On the
left, in red, those who have been quiet for months. At the bottom, in green and blue, New and
Others.

### The notebook checks its own work

![Correlation](03_correlacion_heatmap.png)

The notebook runs nine checks over its own output before drawing anything. That Champions average
fewer than thirty days since their last purchase. That New customers buy little. That the recency
score falls as the days rise. All nine of them come out green on today's data.

Three of those checks are correlations between each score and the number it derives from. A
**correlation** measures whether two quantities move together, with a value between −1 and 1. The
sign says in which direction and the size says how strongly.

- R_Score against recency: −0.83, negative because more days without buying means a lower score.
- F_Score against frequency: 0.87.
- M_Score against monetary value: 0.76.

### What has been measured

These figures come from running the repository on 22 July 2026. Python 3.14.6 and pandas 3.0.3 were
used. Both are considerably newer than the versions it was published with.

| Check | Result |
|---|---|
| The analysis notebook runs end to end | yes, 12.4 seconds, no errors |
| Its nine internal checks | all nine green |
| The three charts, regenerated | byte for byte identical to the published ones |
| The generator reproduces the data file | byte for byte identical |

Every figure on this page was also recomputed by a different route. A purpose-built program reads
the order file without using pandas. The 946 customers, the 7,741 orders and the five groups match.
So do their averages and the three correlations, to the last decimal.

### What is broken

**The data generator does not start on a fresh clone.** It asks for a private Python environment
from its author's machine, named `conda-env-accident_agent-py`. That environment belongs to a
different project on top of that. A July commit fixed the same defect in the analysis notebook. It
left the generator as it was. Forcing the interpreter by hand it works and reproduces the exact
file. The fault is in the label rather than in the program.

**A ratio copied wrong inside the notebook.** Its summary claims Champions spend "3x more than
Loyal, 28x more than New". The measurement gives 2.49 and 29.28. That 28 does exist, but against the
Others group. It slipped while being moved from one place to another.

**The quintile boundary is fragile by construction.** A quintile compares each customer against the
rest, so the cut-off moves when the base changes, and two nearly identical customers can land on
opposite sides of the line. At sixty days without buying, customer 1029 comes out At Risk. Customer
1120, at fifty-nine days and with the same twenty-two purchases, comes out Loyal. One day apart, one
gets a win-back campaign and the other does not.

**The notebook recomputes the quintile cut-offs once per customer** instead of once for everyone.
That waste is paid for as soon as the base grows.

| Customers | Time to score each column |
|---|---|
| 946 | 0.7 seconds |
| 12,217 | 20 seconds |
| 64,000 | 232 seconds |

This page used to promise that the method holds up beyond 100,000 transactions. At that scale the
promise holds, because it finishes in a little over a minute. Where it fails is on a base of
hundreds of thousands of customers. Every doubling of the customer count multiplies the time by
three. Pandas ships a function that does the same split in two thousandths of a second at any size.
The notebook ignores it.

### The proposed actions

The three actions below are an exercise. They show how a business case is presented on top of the
segmentation. Before reading them, it is worth looking at their size. Sales over the twelve months
add up to 5.71 million dollars and the impact proposed here is 2.3 million, that is, 40% of the
entire turnover. The VIP programme alone promises to raise spending by 55% among customers who already
spend the most. Reading these as a forecast of what will happen would be a mistake.

**A VIP programme for the 246 Champions.** Forty-eight hour early access, a dedicated account
manager and invitation-only events. The cashback is 5% above 5,000 dollars.

**A win-back campaign for the 102 at-risk customers.** A 30-day email sequence, a 25% discount and
retargeting. Retargeting means showing ads again to someone who already visited the shop.

**First 90 days for the 59 new customers.** Automated emails, an escalating discount and
gamification, that is, adding game mechanics to the relationship with the brand.

| Action | Spend | Return | ROI |
|--------|-------|--------|-----|
| VIP Champions | $50K | $2.1M | 42:1 |
| Win-back | $5K | $160K | 32:1 |
| Onboarding | $10K | $42.5K | 4:1 |
| **TOTAL** | **$65K** | **$2.3M** | **35:1** |

### When it does not apply

Here the money is not money. The data is invented and generated by the repository itself. That way
the method can be taught without publishing real customers. The return figures in the table above
illustrate a format rather than a result.

The method does not explain everything either, because RFM looks at sales and nothing else. It knows
nothing about the margin on each product or the cost of serving each customer, so the one who bills
most may not be the one who leaves most behind. It does not say why somebody left either. Support
incidents, the treatment they got and what the competition offers leave no trace whatsoever in an
order list.

### Project layout

```
RFM-Customer-Analytics/
├── 01_Analisis_RFM_Completo.ipynb   # The whole analysis: RFM, segmentation and charts
├── Script_Datos_Sinteticos.ipynb    # The generator for the synthetic dataset
├── raw_data_12meses.csv             # The 7,741 orders across 12 months
├── raw_data.csv                     # Secondary dataset
├── 01_segmentacion_barras.png
├── 02_rfm_scatter.png
└── 03_correlacion_heatmap.png
```

Opening the analysis notebook is enough to understand the whole thing. Running it takes twelve
seconds.

### Reproducing it

You need Python 3.9 or later and Jupyter. These two commands open the notebook.

```bash
pip install pandas matplotlib seaborn
jupyter notebook 01_Analisis_RFM_Completo.ipynb
```

The notebook runs from top to bottom. The first cell loads the data. The next ones compute the three
numbers and the scores. Then come the nine checks. The three charts close it.

### Related repositories

This analysis is one piece of an analytics portfolio. These are the sibling projects:

- [lead-scoring-ml](https://github.com/jleonceo/lead-scoring-ml): predicting which lead ends up buying, with classification models.
- [accident-intelligent-agent](https://github.com/jleonceo/accident-intelligent-agent): ETL, exploration and a model to predict how severe a road accident is.
- [analisis-contable](https://github.com/jleonceo/analisis-contable): financial analysis of a company with Python, from the ledger to the conclusions.

*Part of [Juan Luis León](https://github.com/jleonceo)'s portfolio · [juanluisleon.vercel.app](https://juanluisleon.vercel.app) · [MIT](LICENSE) licence*
