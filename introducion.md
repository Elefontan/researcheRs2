Reproducibilidade en ciencia con R: da minaría de datos á publicación
---------------------------------------------------------------------

### Introdución

#### Que é iso da reprodubibilidade?

Un aspecto fundamental do [método científico](https://gl.wikipedia.org/wiki/Método_científico) é comprobar que a partir dun procedemento ou método para comprobar unha hipótese se obteñen os mesmos resultados seguindo o mesmo protocolo, ou resultados consistentes con esta. Porén, moita da literatura científica carece ou ben dos métodos ou ben dos datos como para que [outros grupos científicos os poidan repetir](http://arstechnica.com/science/2016/03/social-science-reproducibility-not-great-but-not-as-bad-as-reported/) e comprobar.

[R](https://gl.wikipedia.org/wiki/R_(linguaxe_de_programación)) conta actualmente con múltiples paquetes orientados aos diferentes puntos que van dende a obtención e análise de datos, á publicacións destes. Con isto, R conta xa con recursos sufientes [como para realizar análises de datos completamente reproducibles](https://methodsblog.wordpress.com/2016/08/02/reproducibility/). En [CRAN Task View: Reproducible Research](https://cran.r-project.org/) hai un listado dos paquetes que cobren estes aspectos.

#### Fontes de datos

Existen proxectos de escala global, por estaren implicados neles diferentes laboratorios ou ser de obxectivos desta escala, e [xornais científicos](http://journals.plos.org/plosone/s/data-availability) nos que están solicitando os datos (por obriga ou de xeito voluntario) que se empregaron para elaborar as publicacións. Os repositorios onde se publican supoñen unha interesante fonte de datos para replicar eses estudos ou crear outros novos proxectos científicos coa mesma base. En case todos, o formato e [as licenzas dos datos](https://wiki.creativecommons.org/wiki/Data) permiten a súa reutilización.

Arestora, algunhas das principais bases de almacenamento de datos científicos son:

1.	[Figshare](https://figshare.com/) repositorio dixital aberto.
2.	[Dryad](http://datadryad.org/) repositorio dixital aberto que ten por obxectivo servir de lugar de publición de datos publicados en revistas.
3.	[GeneBank](https://www.ncbi.nlm.nih.gov/genbank/) dase de datos de secuencias xenéticas da *National Center for Biotechnology Information*.
4.	[EMBL-The European Bioinformatics Institute ](https://www.ebi.ac.uk/) base de datos europea de xenes, proteínas, compostos químicos...
5.	[Nature. Scientific Data](http://www.nature.com/sdata/) : arquivado de datos científicos baseado en 'peer-review'
6.	[DataCite](https://www.datacite.org/) organización altruísta internacional que pretende mellorar que se citen datos, que se visibilicen e arquiven.
7.	[ITIS- Integrated Taxonomic Information System ](https://www.itis.gov/) Sistema de integración da información taxonómica.
8.	[Neuromorpho](http://neuromorpho.org/) inventario de neuronas reconstruídas dixitalmente.
9.	[BioModels DB](http://www.ebi.ac.uk/biomodels-main/) Repositorio de modelos computacionais de procesos biolóxicos.
10.	[Pangea](https://www.pangaea.de/) base de datos de rexistros en xeofísica, océanos, litosfera, superficie terrestre, atmosfera, criosfera...
11.	[Marine Geocience Data System](http://www.marine-geo.org/index.php)
12.	[SEOANE](Sea scientific open data publication) base de datos aberta de datos científicos
13.	[Archaeological Data Service](http://archaeologydataservice.ac.uk/) Base de datos de rexistros arqueolóxicos.

e un longo etcétera!. Nas suxestións do xornal PLOS temos [unha lista máis detallada e completa](http://journals.plos.org/plosone/s/data-availability#loc-recommended-repositories) de repositorios interesantes para publicar/obter datos.

#### Recursos para a minería e tratamento de datos

Un proxecto que aglutina a xente da ciencia involucrada nos *datos abertos* é [rOpenSci](https://ropensci.org/). Desenvolven paquetes de R coa intención de cubrir as funcionalidades de obtención, tratamento, visualización e publicación de datos. En [rOpenSci](https://ropensci.org/packages/) podemos atopar unha lista de paquetes de R que crearon no proxecto. Algúns a destacar:

-	Publicación de datos: *rFigshare* - interface de [Figshare](https://figshare.com/)
-	Obtención de datos: *rdryad* - interface de [Dryad](http://datadryad.org/)
-	Acceso a literatura: *aRxiv* - interface de [arXiv](https://arxiv.org/)
-	Acceso a bases de datos: *nodbi* - interface para interacción con bases de datos NoSQL [MongoDB](https://www.mongodb.com/) ou [CouchDB](http://couchdb.apache.org/)


### I. Obtención de datos

Para a obtención de datos científicos a través de R e a importación ao entorno de traballo, temos [múltiples](https://www.datacamp.com/community/tutorials/r-data-import-tutorial) e [múltiples opcións](https://www.datacamp.com/community/tutorials/importing-data-r-part-two).

Para o acceso a datos remotos, `read.csv()` e `read.table()` traballan do mesmo xeito ca en local. Como exemplo, [ITIS](https://www.itis.gov/) (*Integrated Taxonomic Information System*) permite a busca e descarga de de información taxonómica de especies.

```
Giraffa_tippelskirchi <-
read.csv("https://www.itis.gov/FilesToBeDownloaded/5234.csv")
# str(Giraffa_tippelskirchi)
# 'data.frame':   228 obs. of  1 variable:
# $ X.TU..1012247..Giraffa..tippelskirchi.....N.valid..TWG.standards.met...0.2016.09.27.15.10.48.898184..71024..0.5.220.No.: Factor w/ 219 levels " 1758|5|"," 1762 has been conserved (Opinion 1894",..: 173 174 175 176 177 178 179 180 181 182 ...
```

Unha opción interesante é a obtención directa de datos de **[Dryad](http://datadryad.org/)** con rDryad, que está actualmente en continuo desenvolvemento. Para unha información completa e actualizada, ide a [CRAN](https://cran.r-project.org/web/packages/rdryad/README.html) e [github](https://github.com/ropensci/rdryad).

```
# Obter rDryad, versión de desenvolvemento
devtools::install_git("git://github.com/ropensci/rdryad.git")
library(rdryad)

# En Dryad facer a busca dos datos de interese

# Unha busca por un termo xenérico:
d_solr_search(q="plankton")
#     SolrIndexer.lastIndexed search.resourcetype search.resourceid             handle DSpaceStatus
# 1   2016-07-12T21:06:42.33Z                   2              7496   10255/dryad.7089     Archived
# 2  2016-07-12T21:13:30.318Z                   2             12342  10255/dryad.10933     Archived
# 3  2016-07-12T21:20:13.633Z                   2             21746  10255/dryad.20312     Archived
# 4  2016-07-13T03:46:42.381Z                   2             30792  10255/dryad.29358     Archived
# 5  2016-07-12T19:34:52.229Z                   2            155886 10255/dryad.114037     Workflow
# [...]

# Unha busca termo na definición dos datos:
d_solr_highlight(q="phytoplankton", hl.fl="dc.description")
# $`10255/dryad.125410`
# $`10255/dryad.125410`$dc.description
# [1] "1. we analysed the functional composition of coastal <em>phytoplankton</em> communities (n=7941) along"
# $`10255/dryad.17442`
# list()
# [...]

# Cada publicación en Dryad ten un identificador `dc.identifier.uri`
# Este valor pódese ver premendo en "Show Full Metadata"
# Pódense facer captura de datos con este ID:
url <- download_url("10255/dryad.10933")
# e descargar nun cartafol local os datos desa ID
dryad_fetch(url)
# saving to: /home/eu/10255_dryad.10933/oai
# trying URL 'http://datadryad.org/bitstream/handle/10255/dryad.10933/oai_dc.xml?sequence=1'
# Content type 'unknown' length 2073 bytes
# ==================================================
# downloaded 2073 bytes
> cd /home/eu && ls
# drwxr-xr-x   2 miguel users      20 Out 17 18:00 10255_dryad.10933

# Busca dos datos en base a DOI da publicación:
d_solr_search(q="dc.relation.isreferencedby:10.1038/nature04863",
fl="dc.identifier,dc.title_ac")
# dc.identifier
# 1 doi:10.5061/dryad.8426,doi:10.5061/dryad.8426/1,doi:10.5061/dryad.8426/2
```

### II. Edición con R Markdown

#### Markdown

**[Markdown](https://daringfireball.net/projects/markdown/)** é unha [linguaxe de marcas](https://gl.wikipedia.org/wiki/Linguaxe_de_marcas) en formato de [texto simple](https://en.wikipedia.org/wiki/Plain_text). Deseñouse para se converter a [HTML](https://gl.wikipedia.org/wiki/HTML) dun xeito sinxelo.

A vista de edición en markdown faise sinxela xa que non se usan máis que texto, con poucos caracteres non alfabéticos, como o son o `*` e `#`. Os ficheiros de markdown teñen unha extensión `.md` ou `.markdown`.

O [esencial de Markdown](http://rmarkdown.rstudio.com/authoring_basics.html) apréndese axiña!. Aquí temos os exemplos esenciais.

Os **parágrafos** en Markdown son o texto consecutivo. Cando ese texto vai seguido dun *espazo en branco*, o texto salta a unha nova liña e aparece un novo parágrafo. Pódense declarar novas liñas a man usando dous espazos ou máis.

O **estilo de texto** dáselle así:

```
 *texto en cursiva* ou **negra**
 _texto en cursiva_ ou __negra__
```

Nun texto podemos introducir bloques de código, que se declaran cun ">"

```
 r-users.gal infórmanos de que:
 > "A III Xornada de Usuarios de R en Galicia terá lugar na Facultade de Matemáticas da USC [...]"
```

Para darlle unha **ligazóns** ao texto úsase `[texto](ligazón)`:

```
 > "A [III Xornada de Usuarios de R en Galicia](https://www.r-users.gal) [...]""
```

As **imaxes** pódense introducir no texto ligándoas con ficheiros locais ou cunha ligazón á páxina onde estean aloxadas:

```
 ![alt text](http://r-users.gal/rgal15.png) # local
 ![alt text](figures/rgal15.png)            # web
```

O texto pódese ordenar en **listas**:

```
 En listas sen ordenar:

 * Elemento 1
 * Elemento 2
     + Elemento 2.1
     + Elemento 2.2

 E en listas ordenadas:

 1. Elemento 1
 2. Elemento 2
 3. Elemento 3
     + Elemento 3.1
     + Elemento 3.2
```

O texto escrito estruturase en bloques de contido coas **cabeceiras**. Emprégase `#` para as declarar.

```
 # Sección 1
 ## Subsección 2
 ### Subsubsección 3
```

Amais das seccións, pódense establecer **regras e saltos de páxina**:

```
 Isto crea unha liña horizontal:
 ******
 e isto un salto de páxina:
 ------
```

#### Ecuacións

R Markdown acepta a incrustación de fórmulas escritas en [LaTeX](https://en.wikibooks.org/wiki/LaTeX/Mathematics) e [MathML](http://www.w3.org/Math/).

As ecuacións poden ir dos seguintes xeitos: - `$ecuación$` para ecuacións LaTeX en liña. Aquí non pode haber espazos entre os `$` e o texto; - `$$ ecuación $$` para ecuacións LaTeX na súa propia liña, - e `<math ...> </math>` para ecuacións MathML

Para obter as fórmulas editadas, hai [asistentes en liña](http://mathstat.uohyd.ernet.in/equationeditor/equationeditor.php)

#### R Markdown

**R Markdown** é a implementación de Markdown para R. Está baseado na libraría **[knitr](http://yihui.name/knitr/)** e no conversor universal de documentos **[pandoc](http://pandoc.org/)** e integrado coa [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment) **[RStudio](https://www.rstudio.com/)**.

Con R Markdown xéranse documentos, informes ou presentacións de xeito dinámico. Grazas a iso, pódense xerar informes con resultados xerados dinamicamente. Cando xa están creados, os documentos poden conter todo o contido resultante (análises estatísticas, gráficos,...) e/ou o **código fonte de R** que se empregou para obtelos.

Os informes en R xéranse cos ficheiros de extensión *.Rmd*, a extensión de R Markdown. A creación destes ficheiros depende de tres motores. O primeiro é **Markdown**, que é o que se encarga da produción do formato de texto (Véxase a sección anterior). As libraría **[knitr](http://yihui.name/knitr/)** ocúpanse de interpretar e incrustar o código fonte e o seu resultado. Finalmente, **YAML** que é o cabezallo do ficheiro Markdown é que contén claves do formato e saída final do documento. YAML indica que tipo de ficheiro ten que se xerar a partir do ficheiro *.Rmd*, R Markdown. Unha alternativa a *Knitr* é **[Sweave](http://www.statistik.lmu.de/~leisch/Sweave/)**. A **sintaxe de Markdown** está ao completo en [Markdown: Syntax (by John Gruber)](http://daringfireball.net/projects/markdown/syntax). A implementación de Markdown para R está en [Rmarkdown para RStudio](http://rmarkdown.rstudio.com/html_document_format.html#overview) (Véxase *p.ex* a guía para a saída a *html*\)

YAML é a sección inicial do cabezallo do documento `.Rmd`. Nesta parte están declaradas propiedades do formato. Así, os valores de `output` no cabezallo YAML determina cal ha de ser o formato de saída do documento final. Cun cabezallo así xeraríase un ficheiro final de formato *html*:

```
 ---------------------
 output: html_document
 ---------------------
```

Actualmente, o tipo de formato dos ficheiros finais que se pode crear a partir dos *.Rmd* son `html`, `odf` <sup>\([formato libre](https://en.wikipedia.org/wiki/OpenDocument)\)</sup>, `docx` <sup>\([privativo](https://en.wikipedia.org/wiki/Proprietary_format)\)</sup>, `pdf`, ou presentacións `beamer`, [entre outras](http://rmarkdown.rstudio.com/formats.html).

O resto do documento, fóra xa da cabeceira de YAML, levará sempre unha sintaxe de Markdown.

Dentro do texto, pódense incluír `bloques de código`. Todo bloque de código declárase con **\`\`\`** . Como exemplo:

> *\`\`\`* if (eSinxelo){ return "é sinxelo aprender R!" }*\`\`\`*

O anterior éra un bloque de código xenérico. Arestora, coa [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment) [RStudio](https://www.rstudio.com/) pódense introducir bloques de código de R, [Python](https://gl.wikipedia.org/wiki/Python), [SQL](https://gl.wikipedia.org/wiki/SQL), [Bash](https://gl.wikipedia.org/wiki/Bash), [Rcpp](http://dirk.eddelbuettel.com/code/rcpp.html), [Stan](https://en.wikipedia.org/wiki/Stan_(software)), [JavaScript](https://gl.wikipedia.org/wiki/JavaScript) e [CSS](https://gl.wikipedia.org/wiki/CSS) <sup>(véxase [knitr Language Engines](http://rmarkdown.rstudio.com/authoring_knitr_engines.html)\)</sup>\.

Os bloques de código de **R** decláranse cun **\`\`\`{r} o_meu_código \`\`\`**. Todo o código que aí vaia irá interpretado no documento de saída final.

No texto en Markdown, pódese introducir código dentro das liñas e o resultante no documento final sexa a interpretación dese código. Declárase así:

```
 A taxa de crecemento da poboación foi de `r round(log(10)^pi*3, digits=2)` individuos/día
```

Esta frase aparecerá no documento final como *' A taxa de crecemento da poboación foi de 41.22 individuos/día'*.

Na cabeceira dos bloques de código pódense declarar propiedades de como interpretar o bloque e da saída final.

> \`\`\` {r fig.width=8, fig.height=3} plot(resultado) \`\`\`

As principais opcións para os cabezallos de código de R son estes:

| Opción     | Predefinido | Efecto                                      |
|------------|-------------|---------------------------------------------|
| eval       | TRUE        | Avaliar o código e incluír o seu resultado? |
| echo       | TRUE        | Mostrar código e resultados xuntos?         |
| warning    | TRUE        | Mostrar as advertencias (*warnings*)?       |
| error      | FALSE       | Mostrar os erros                            |
| message    | TRUE        | Mostrar as mensaxes?                        |
| tidy       | FALSE       | Aliñar e limpar o formato de código?        |
| results    | "markup"    | "markup", "asis", "hold", ou "hide"         |
| cache      | FALSE       | Gardar os resultados no caché?              |
| comment    | "##"        | Caracter para mostrar código comentado      |
| fig.width  | 7           | Ancho das imaxes de resultado, en polgadas  |
| fig.height | 7           | Alto das imaxes de resultado, en polgadas   |

#### YAML

O cabezallo YAML controla o renderizado dos ficheiros `.rmd` de R Markdown. Un exemplo completo de YAML é este:

```
---
title: "Da Lei potencial á logseries"
author: "[Eu Mesmo](www.eumesmo.gal)"
date: "20 de outubro de 2016"
output: html_document
---
```

Cada entrada declara unha propiedade do ficheiro final. YAML acepta código de R, así que a data pódese indicar con "date: `r Sys.Date()`"

As `outputs` que arestora acepta a IDE RStudio son `html_output` (saída en `html`), `pdf_document` (saída en `pdf`) e `word_document` (saída no formato privativo `.docx`). A información de como xerar `.pdf` está na sección de [Formato PDF para RMarkdown](http://rmarkdown.rstudio.com/pdf_document_format.html)).

Na YAML tamén se poden definir propiedades das figuras, como o seu tamaño final ou se levan rodapés.

```
---
output: html_document:
  fig_width: 8
  fig_height: 4
  fig_caption: true
---
```

Ao ficheiro final de `html` que xera R Markdown pódenselle declarar propiedades de estilo empregando un ficheiro [CSS](https://www.w3.org/Style/CSS/).

```
---
output: html_document: css: styles.css
---
```

Nese ficheiro CSS pódense declarar estilos de cada elemento da páxina `html` final. Unha sección do `.css`, como exemplo, define o estilo dos títulos principais (`h1`\):

```
h1 { font-weight: 400;
  margin-top: 4rem;
  margin-bottom: 1.5rem;
  font-size: 3.2rem;
  line-height: 1; }
```
##### Creación de táboas

Librarías como [`xtable`](https://cran.r-project.org/web/packages/xtable) permiten a visualización de táboas, a creación de táboas de resultados e informes estatísticos para documentos HTML e LaTeX.

Con datos de mostraxes en dunas neerlandesas e `xtable`:
```
library(xtable)
data(dune.env) # de vegan()
str(dune.env)
# 'data.frame':	20 obs. of  5 variables:
#  $ A1        : num  2.8 3.5 4.3 4.2 6.3 4.3 2.8 4.2 3.7 3.3 ...
# $ Moisture  : Ord.factor w/ 4 levels "1"<"2"<"4"<"5": 1 1 2 2 1 1 1 4 3 2 ...
# $ Management: Factor w/ 4 levels "BF","HF","NM",..: 4 1 4 4 2 2 2 2 2 1 ...
# $ Use       : Ord.factor w/ 3 levels "Hayfield"<"Haypastu"<..: 2 2 2 2 1 2 3 3 1 1 ...
# $ Manure    : Ord.factor w/ 5 levels "0"<"1"<"2"<"3"<..: 5 3 5 5 3 3 4 4 2 2 ...
```

Pódense obter informes dos resultados de regresión lineal, modelos xerais linearizados ou de análise de varianza. Como exemplo, cos datos de `dune.env` aplícase unha `lm()` e `ANOVA()` e obtense directamente unha táboa de datos en formato `html`:

```
# Obter o resumo dunha regresión lineal.
fml <- lm(A1 ~ Management * Use, data = dune.env)
print(xtable(anova(fml)), type="html")
# <!-- html table generated in R 3.3.1 by xtable 1.8-2 package -->
#   <table border=1>
#   <tr> <th>  </th> <th> Df </th> <th> Sum Sq </th> <th> Mean Sq </th> <th> F value </th> <th> Pr(&gt;F) </th>  </tr>
#   <tr> <td> Management </td> <td align="right"> 3 </td> <td align="right"> 17.15 </td> <td align="right"> 5.72 </td> <td align="right"> 4.31 </td> <td align="right"> 0.0383 </td> </tr>
#   <tr> <td> Use </td> <td align="right"> 2 </td> <td align="right"> 17.26 </td> <td align="right"> 8.63 </td> <td align="right"> 6.50 </td> <td align="right"> 0.0179 </td> </tr>
#   <tr> <td> Management:Use </td> <td align="right"> 5 </td> <td align="right"> 43.88 </td> <td align="right"> 8.78 </td> <td align="right"> 6.62 </td> <td align="right"> 0.0075 </td> </tr>
#   <tr> <td> Residuals </td> <td align="right"> 9 </td> <td align="right"> 11.94 </td> <td align="right"> 1.33 </td> <td align="right">  </td> <td align="right">  </td> </tr>
#   </table>

# Obter o resumo dunha ANOVA
print(xtable(anova(fml)), type="html", include.rownames = TRUE)
# <!-- html table generated in R 3.3.1 by xtable 1.8-2 package -->
# <table border=1>
# <tr> <th>  </th> <th> Df </th> <th> Sum Sq </th> <th> Mean Sq </th> <th> F value </th> <th> Pr(&gt;F) # </th>  </tr>
#  <tr> <td> Management </td> <td align="right"> 3 </td> <td align="right"> 17.15 </td> <td align="right"> 5.72 </td> <td align="right"> 4.31 </td> <td align="right"> 0.0383 </td> </tr>
#  <tr> <td> Use </td> <td align="right"> 2 </td> <td align="right"> 17.26 </td> <td align="right"> 8.63 </td> <td align="right"> 6.50 </td> <td align="right"> 0.0179 </td> </tr>
#  <tr> <td> Management:Use </td> <td align="right"> 5 </td> <td align="right"> 43.88 </td> <td align="right"> 8.78 </td> <td align="right"> 6.62 </td> <td align="right"> 0.0075 </td> </tr>
#  <tr> <td> Residuals </td> <td align="right"> 9 </td> <td align="right"> 11.94 </td> <td align="right"> 1.33 </td> <td align="right">  </td> <td align="right">  </td> </tr>
#   </table>
```

Outra librería é `[pander](http://rapporter.github.io/pander/)`. Esta crea directamente resumos no formato Markdown.

```
# Táboas de datos
pandoc.table(head(dune.env))

# ----------------------------------------------
#  A1   Moisture   Management    Use     Manure
# ---- ---------- ------------ -------- --------
# 2.8      1           SF      Haypastu    4    
#
# 3.5      1           BF      Haypastu    2    
#
# 4.3      2           SF      Haypastu    4    
#
# 4.2      2           SF      Haypastu    4    
#
# 6.3      1           HF      Hayfield    2    
#
# 4.3      1           HF      Haypastu    2    
# ----------------------------------------------

# Defindo o estilo da táboa
pandoc.table(head(dune.env), style = "grid", caption = "Dunas neerlandesas")

# +------+------------+--------------+----------+----------+
# |  A1  |  Moisture  |  Management  |   Use    |  Manure  |
# +======+============+==============+==========+==========+
# | 2.8  |     1      |      SF      | Haypastu |    4     |
# +------+------------+--------------+----------+----------+
# | 3.5  |     1      |      BF      | Haypastu |    2     |
# +------+------------+--------------+----------+----------+
# | 4.3  |     2      |      SF      | Haypastu |    4     |
# +------+------------+--------------+----------+----------+
# | 4.2  |     2      |      SF      | Haypastu |    4     |
# +------+------------+--------------+----------+----------+
# | 6.3  |     1      |      HF      | Hayfield |    2     |
# +------+------------+--------------+----------+----------+
# | 4.3  |     1      |      HF      | Haypastu |    2     |
# +------+------------+--------------+----------+----------+
#
# Title: Dunas neerlandesas
```
Aquí vemos os mesmos informes de `lm()` e `ANOVA()` mais con saída para `md` con pander:

```
# fml <- lm(A1 ~ Management * Use, data = dune.env)
# Resultados da regresión lineal:
pander(fml, caption = attr(x, "caption"),
+ add.significance.stars = TRUE)

# ---------------------------------------------------------------------------
#          &nbsp;           Estimate   Std. Error   t value   Pr(>|t|)       
# ------------------------ ---------- ------------ --------- ---------- -----
#    **ManagementHF**        0.83        0.86       0.97       0.36         
#
#    **ManagementNM**        4.8         0.88        5.5     0.00039   * * *
#
#    **ManagementSF**        1.1         1.3        0.89       0.4          
#
#       **Use.L**            0.14        1.2        0.12       0.9          
#
#       **Use.Q**           -0.082       1.2       -0.071      0.95         
#
# **ManagementHF:Use.L**     -1.2        1.4        -0.85      0.42         
#
# **ManagementNM:Use.L**     3.6         1.5         2.5      0.035      *  
#
# **ManagementSF:Use.L**     1.5         2.9        0.52       0.61         
#
# **ManagementHF:Use.Q**    0.041        1.6        0.026      0.98         
#
# **ManagementNM:Use.Q**     -3.9        1.6        -2.5      0.035      *  
#
#    **(Intercept)**         3.4         0.66        5.2     0.00059   * * *
# ---------------------------------------------------------------------------
#
# Table: Fitting linear model: A1 ~ Management * Use

# ANOVA
pander(anova(fml))

# ---------------------------------------------------------------
#        &nbsp;         Df   Sum Sq   Mean Sq   F value   Pr(>F)
# -------------------- ---- -------- --------- --------- --------
#    **Management**     3      17       5.7       4.3     0.038  
#
#       **Use**         2      17       8.6       6.5     0.018  
#
#  **Management:Use**   5      44       8.8       6.6     0.0075
#
#    **Residuals**      9      12       1.3       NA        NA   
# ---------------------------------------------------------------
#
# Table: Analysis of Variance Table
```

#### Procesado dos ficheiros R Markdown

##### rmarkdown

Con Markdown conséguese eliminar todo o etiquetado de HTML. Con iso conséguese unha edición e lectura fácil. Con R Markdown conséguese incrustar código e producir informes dinámicos. Un esquema do proceso que temos feito até o de agora é o seguinte:

```
R markdown:
    - Markdown + con código R incrustado
    - .Rmd --> .md --> html (odf, pdf...)
```

O último proceso, unha vez completada a análide de datos e a edición do informe ou artigo, é a conversión ao formato de publicación.

RStudio ten implementado na súa interface a totalidade do precesado de documentos `Rmd` para obter `html`, `pdf` e `docx`. Dende o botón `Knit output` ou `Configuración -> Output Options` pódese establecer todas as opcións de renderizado do documento final: o seu formato, tamaño das imaxes, ubicación do ficheiro CSS... Até o de agora, editamos para obter un `html`.

O renderizado pódese efectuar tanto con RStudio como desde o terminal de R:

```
> rmarkdown::render("rgal16.Rmd")
```

A función `render()` de `rmarkdown` precisa dun documento de orixe e admite establecer os formatos de saída.

```
> rmarkdown::render("rgal16.Rmd", html_document())
> rmarkdown::render("rgal16.Rmd", pdf_document())
```

A cada un destes fórmatos de saída pódenselle declarar certas opcións. Segundo iso, `pandoc` interpretará a conversión dun xeito ou doutro. Como exemplo, unha saída con `html_document` permite incluir formatos de saída ou modelos de resalte de código:

```
rmarkdown::render("rgal16.Rmd", html_document(
  dev = "png",           # formato de saída de imaxes
  highlight = "tango",   # estilo de resalte de código, "default" ou espresso"
  template = "default",  # modelo de renderizado de pandoc
  pandoc_args = NULL)    #
  )
```

##### Pandoc

[Pandoc](http://pandoc.org/) é unha navalla suíza: converte documentos de markdown, HTML, DocBook, LaTeX ou ODF a outros tantos formatos como HTML, Markdown, epub ou PDF. Como vimos, é o xestor de `rmarkdown` para a conversión.

Unha alternativa a facer a chamada de conversión de formato desde R, é facer uso directo de `pandoc`. Un primeiro exemplo do seu uso, desde o terminal, é esta conversion de `markdown` a `html`:

```
#!bash
# Conversión de markdown a HTML
pandoc rgal16.md -f markdown -t html -s -o rgal16.html
```

Inda que temos moitas máis conversións que poderíamos facer. Temos unha [guía de introdución](http://pandoc.org/getting-started.html) e exemplos [demostracións](http://pandoc.org/demos.html) na web oficial de pandoc.

Máis exemplos de conversións:

```
#!bash
# Conversión a documento de LaTeX:
pandoc rgal16.md -f markdown -t latex -s -o rgal16.tex
```

```
#!bash
# Conversión a OpenDocument Format
pandoc rgal16 -o rgal16.odt
```

```
#!bash
# Conversión de Markdown a Docx
# Lembra que o formato Microsoft Office docx non é un formato libre!
pandoc rgal16.md -f markdown -t docx -s -o rgal16.docx
```

##### Pandoc e a bibliografía

`pandoc` co seu complemento [`pandoc-citeproc`](http://pandoc.org/installing.html) facilita que os documentos convertidos procesen referencias biliográficas. Isto é, que se poden converter documentos `.md`, Markdown, a un `html`, `pdf`... incluíndo as citas na posición correcta, sen ter que o facer a man. As citas procésaas `pandoc-citeproc`, e faino para calquera tipo de formato de saída.

Primeiro, a xestión dos recursos bibliográficos pódese realizar con [Zotero Reference Manager](https://www.zotero.org/). É xestor de bliografía libre completo, que nos permite compilar, almacenar en local e na nube a nosa bibliografía e exportala. As referencias bibliográficas que nos interesen pódense [exportar](https://www.zotero.org/support/quick_start_guide) a un ficheiro `.bib`, Bibtex, desde Zotero.


As referencias exportadas nos ficheiros `bib` teñen un identificador que se pódese ver abrindo o ficheiro `.bib` e vendo o nome.

```
@article{margalef_1955,
    title = {El fitoplancton de la ría de {Vigo} de enero de 1953 a marzo de 1954},
    issn = {0020-9953},
    url = {http://digital.csic.es/handle/10261/87372},
    abstract = {45 páginas, 11 tablas, 11 figuras},
    language = {spa},
    urldate = {2015-09-29},
    author = {Margalef, Ramón and Durán, Miguel and Saiz, Fernando},
    year = {1955},
    file = {}
}
```

Esta referencia ten o identificador `margalef_1955`. Para citalas, nos ficheiros Markdown emprégase a súa identificación como `[@RefKey]`. No caso do artigo anterior, teríamos que identificalo con `[@margalef_1955]`.

As citas pódense concatenar así `[@margalef_1953; @margalef_1955]`, ou incluír así `[-@margalef_1953]` para que só aparezan nas bibliografía final pero non no texto. Se é o caso de que se quere citar dentro do no texto pero si que apareza ao final na lista de bibliografía, hase de usar un campo "dummy" `nocite`:

```
---
nocite: |
  @margalef_1955, @margalef_1953
...
```
A localización da bibliografía hai que especificala en YAML:

```
---
output:
  html_document:
    fig_caption: yes
    number_sections: yes
    toc: yes
csl: apa.csl
bibliography: margalef.bib
---
```
Ha de ser no final do texto onde se cree a lista de referencias bibliográficas:

```
## Bibliografía {-}
<!-- espazo no que se xerará a bibliografía --!>
```

Outra opción para a xestión de bibliografía é con `knitcitations`. Debemos chamar á importación da bibliografía:

```
require(knitcitations)
cleanbib() # limpeza de citas anteriores
options("citation_format" = "pandoc")
refs <- read.bibtex("margalef.bib")
```
No texto chamarase á estas bibliografía importada con:
```
`r citep(refs[2])`
# refs[2]
# [1] R. Margalef, M. Duran, F. Saiz, et al. “El fitoplancton de la ria de Vigo de enero de 1953 a
marzo de 1954”. Spanish. In: _Invest. Pesq._ (1955). <URL:
http://digital.csic.es/handle/10261/87372>.
```

No caso de xerar `pdf` precisaremos de ter un entorno de LaTeX instalado. YAML haberá de especificar a librería de xestión de referencias bibliográficas e o compilador de LaTeX, entre outros:

```
---
output: pdf_document:
  citation_package: natbib
  latex_engine: xelatex
  template: modelo_de_formato.tex
  bibliography: ~/cartafol/referencias.bib
  biblio-style: apsr
---
```
Para os documentos finais `pdf` e de obriga empregar paquetes de LaTeX, como `natbib` or `biblatex`, que procesen as referencias bibliográficas. Os ficheiros finais `pdf` coa bibliografía incorporada deste xeito:

```
#!bash
# Un ficheiro .md de entrada que se converterá a un pdf final
# con todas as referencias obtidas de refs.bib
pandoc documento_inicial.md -t latex --filter pandoc-citeproc --bibliography=refs.bib -o documento_final.pdf
```
### III. Publicación
Toda vez que elaboramos unha análise de datos ou publicación rematada podemos empregar [Git](https://git-scm.com/) e publicar en [GitHub](https://github.com/).

Outra posibilidade é publicalos en [figshare](https://figshare.com/). Ademais de para almacenar ou atopar datos, serve como lugar para depositar resultados. A libraría [rfigshare](https://cran.r-project.org/web/packages/rfigshare/) facilítanos iso.

```
# install.packages("rfigshare")
require(rfigshare)
# Busca de ti como autor
fs_author_search("Boettiger")
## list()

# Creación de contido propio
id <- fs_create("Título", "descrición")
## Your article has been created! Your id number is 19830929
# Con isto, crouse un espazo propio cos datos esenciais
# Agora, para subir novos datos ao noso espazo, creamos primeiro o ficheiro:
write.csv(rgal16, "rgal16.csv")
# e logo lígase cos datos da conta de figshare
fs_upload(id, "rgal16.csv")
# Engádenselle metadatos ao ficheiro
fs_add_tags(id, "rstats")
# Finalmente, pódese publicar como datos privados:
fs_make_private(id)
# ou públicos
fs_make_public(id)
```
### IV. Instalación
<!---
Información de sistema operativo libre
--->
<!---
rstudio; rmarkdown
rkward
--->

<!---
http://pandoc.org/installing.html
--->

<!---
Zotero
--->

<!---
info sobre LaTeX en linux, windows
--->

### V. Recursos xerais e de R para ciencia


1.	[R for Data Science. Garrett Grolemund & Hadley Wickham. O'Reilly 2016](http://r4ds.had.co.nz/)
2.	[Advanced R. Hadley Wickham](http://adv-r.had.co.nz/)
3.	[Github for Scientists](https://rawgit.com/nazrug/Quickstart/master/GithubQuickstart.html)
4.	[Software-Carprentry. Teaching basic lab skills for research computing](http://software-carpentry.org/)
5.	[Data Carpentry](http://www.datacarpentry.org/)
