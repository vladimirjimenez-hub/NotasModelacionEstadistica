# Guía para Colaboradores — Modelación Estadística CIMAT

Guía de referencia para catedráticos que contribuyen al libro
**Modelación Estadística** de la Maestría en Optimización y Modelación
de Procesos (OMP), CIMAT Aguascalientes.

Repositorio: https://github.com/mop-cimat-ags/NotasModelacionEstadistica  
Libro en línea: https://mop-cimat-ags.github.io/NotasModelacionEstadistica

---

## Contenido

1. [Herramientas necesarias](#1-herramientas-necesarias)
2. [Configuración inicial (solo la primera vez)](#2-configuración-inicial-solo-la-primera-vez)
3. [Estructura del proyecto](#3-estructura-del-proyecto)
4. [Cómo editar un capítulo](#4-cómo-editar-un-capítulo)
5. [Cómo crear un capítulo nuevo](#5-cómo-crear-un-capítulo-nuevo)
6. [Sintaxis básica de Quarto](#6-sintaxis-básica-de-quarto)
7. [Usar la librería modelEstCIMAT](#7-usar-la-librería-modelestcimat)
8. [Agregar funciones y datos a la librería](#8-agregar-funciones-y-datos-a-la-librería)
9. [Flujo de trabajo con Git](#9-flujo-de-trabajo-con-git)
10. [Trabajo con ramas (branches)](#10-trabajo-con-ramas-branches)
11. [Subir cambios a GitHub](#11-subir-cambios-a-github)
12. [Preguntas frecuentes](#12-preguntas-frecuentes)

---

## 1. Herramientas necesarias

Instala lo siguiente antes de empezar:

| Herramienta | Descarga | Para qué sirve |
|---|---|---|
| **R** (≥ 4.1) | https://cran.r-project.org | Ejecutar código del libro |
| **Quarto** | https://quarto.org/docs/get-started | Renderizar el libro |
| **Git** | https://git-scm.com/download/win | Control de versiones |
| **VS Code** | https://code.visualstudio.com | Editor principal |
| **RStudio** (opcional) | https://posit.co/download/rstudio-desktop | Alternativa a VS Code para R |

### Extensiones de VS Code recomendadas

Abre VS Code, ve a Extensiones (`Ctrl+Shift+X`) e instala:

- **Quarto** — soporte para archivos `.qmd`
- **R** — soporte para código R
- **GitLens** — visualización de cambios en Git

### Paquetes de R necesarios

Abre R o RStudio y ejecuta:

```r
install.packages(c("devtools", "knitr", "rmarkdown"),
                 repos = "https://cloud.r-project.org")
```

---

## 2. Configuración inicial (solo la primera vez)

### 2.1 Crear cuenta en GitHub

Ve a https://github.com y crea una cuenta si no tienes una.
Comparte tu usuario de GitHub con el administrador del repositorio para
que te den acceso.

### 2.2 Configurar Git con tu identidad

Abre la terminal de VS Code (`Ctrl+ñ`) y ejecuta:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu.correo@cimat.mx"
```

### 2.3 Clonar el repositorio

```bash
git clone https://github.com/mop-cimat-ags/NotasModelacionEstadistica.git
```

Esto descarga el proyecto completo a tu computadora. Solo se hace una vez.

### 2.4 Abrir el proyecto en VS Code

```bash
cd NotasModelacionEstadistica
code .
```

---

## 3. Estructura del proyecto

```
NotasModelacionEstadistica/
├── _quarto.yml                  # Configuración del libro (no modificar sin avisar)
├── index.qmd                    # Página de inicio del libro
├── referencias.qmd              # Bibliografía
├── referencias.bib              # Archivo de referencias BibTeX
├── estilos-cimat.css            # Estilos visuales (no modificar)
├── imagenes/                    # Logos e imágenes generales
├── capitulos/
│   ├── parte1/                  # Parte I — Probabilidad y Distribuciones
│   │   ├── cap01-intro-estadistica.qmd
│   │   ├── cap02-distribuciones.qmd
│   │   └── cap03-distribucion-conjunta.qmd
│   └── parte2/                  # Parte II — Inferencia Estadística
│       └── cap04-inferencia.qmd
├── libreria/                    # Paquete R modelEstCIMAT
│   ├── R/                       # Funciones del paquete
│   └── data/                    # Datasets del curso
├── latex/                       # Archivos para el PDF (no modificar)
└── .github/workflows/           # Automatización de publicación (no modificar)
```

**Regla:** edita únicamente los archivos `.qmd` dentro de `capitulos/`
y los archivos de la `libreria/`. El resto lo administra el coordinador.

---

## 4. Cómo editar un capítulo

### 4.1 Antes de empezar, trae los cambios más recientes

```bash
git pull
```

Hazlo **siempre** antes de editar para evitar conflictos.

### 4.2 Abre el archivo .qmd correspondiente

Por ejemplo, para editar el capítulo 2:

```
capitulos/parte1/cap02-distribuciones.qmd
```

### 4.3 Previsualiza el libro mientras editas

En la terminal:

```bash
quarto preview
```

Se abrirá el libro en tu navegador y se actualizará automáticamente
cada vez que guardes un archivo.

### 4.4 Renderiza el libro completo

Cuando termines:

```bash
quarto render
```

Esto genera la versión HTML, PDF y Word en la carpeta `_book/`.

---

## 5. Cómo crear un capítulo nuevo

### 5.1 Crea el archivo .qmd

Dentro de la carpeta correspondiente, crea un archivo nuevo.
Ejemplo: `capitulos/parte2/cap05-regresion.qmd`

Todo capítulo debe empezar con un encabezado YAML:

```yaml
---
title: "Regresión Lineal"
---
```

### 5.2 Regístralo en `_quarto.yml`

Avisa al coordinador para que agregue el capítulo al índice del libro
en `_quarto.yml`, bajo la parte correspondiente:

```yaml
- part: "Parte II - Inferencia Estadistica"
  chapters:
    - capitulos/parte2/cap04-inferencia.qmd
    - capitulos/parte2/cap05-regresion.qmd   # <-- nuevo
```

---

## 6. Sintaxis básica de Quarto

### Encabezados

```markdown
# Título del capítulo (no usar, ya viene del YAML)

## Sección

### Subsección
```

### Texto con formato

```markdown
**negrita**   *cursiva*   `codigo en línea`
```

### Listas

```markdown
- elemento 1
- elemento 2
  - subelemento
```

### Código R

````markdown
```{r}
x <- c(1, 2, 3, 4, 5)
mean(x)
```
````

Opciones útiles para el chunk:

````markdown
```{r}
#| echo: false       # oculta el código, muestra solo el resultado
#| fig-cap: "Mi figura"
#| fig-width: 6
plot(x)
```
````

### Figuras

```markdown
![Descripción de la imagen](ruta/imagen.png){width=70%}
```

### Ecuaciones

```markdown
Ecuación en línea: $\mu = \frac{1}{n}\sum x_i$

Ecuación centrada:
$$
f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$
```

### Teoremas y definiciones

```markdown
::: {#thm-nombre}
## Nombre del Teorema
Enunciado del teorema.
:::

::: {#def-nombre}
## Nombre de la Definición
Texto de la definición.
:::
```

### Referencias cruzadas

```markdown
Ver @thm-nombre o la @def-nombre.
```

### Notas al pie

```markdown
Texto con nota al pie.[^1]

[^1]: Contenido de la nota.
```

### Citas bibliográficas

Agrega la referencia en `referencias.bib` y cítala así:

```markdown
Como demuestra @casella2002statistical...
```

---

## 7. Usar la librería modelEstCIMAT

Al inicio de cada capítulo que use funciones de la librería, agrega
este chunk de configuración:

````markdown
```{r}
#| include: false
devtools::load_all(here::here("libreria"), quiet = TRUE)
```
````

### Funciones disponibles

```r
# Estadística descriptiva
resumen_estadistico(x)
tabla_frecuencias(x, k = 6)
curtosis(x)
asimetria(x)

# Inferencia
ic_media(x, nivel = 0.95)
ic_proporcion(x = 30, n = 100)
ic_varianza(x)
prueba_z(x, mu0 = 0, sigma = 1)
emv_normal(x)
emv_exponencial(x)
emv_poisson(x)

# Simulación
simular_distribucion("normal", n = 500, mean = 0, sd = 1)
simular_bootstrap(x, FUN = mean, B = 1000)
monte_carlo_integral(function(x) x^2, a = 0, b = 1)
graficar_densidad("t", df = 10, cola = "bilateral", alpha = 0.05)
graficar_ic(ic_media(x))
```

### Datasets disponibles

```r
data(alturas_estudiantes)   # n=80, altura/peso de estudiantes
data(tiempos_falla)         # n=60, tiempos exponenciales
data(calificaciones_curso)  # n=35, tres examenes correlacionados
data(conteos_defectos)      # n=50, conteos Poisson
data(temperaturas_mensual)  # n=365, temperaturas diarias
```

### Agregar funciones nuevas

1. Crea o edita un archivo en `libreria/R/`
2. Escribe tu función con `@export` en el comentario
3. Recarga: `devtools::load_all("libreria")`

---

## 8. Agregar funciones y datos a la librería

La librería `modelEstCIMAT` está en la carpeta `libreria/` y cualquier
colaborador puede extenderla con nuevas funciones o datasets.

### 8.1 Agregar una función nueva

**Paso 1 — Abre o crea un archivo en `libreria/R/`**

Puedes agregar tu función al archivo temático que corresponda:

- `estadisticas.R` — estadística descriptiva
- `inferencia.R` — intervalos de confianza, pruebas, EMV
- `simulacion.R` — bootstrap, Monte Carlo, simulación

O crear un archivo nuevo, por ejemplo `libreria/R/regresion.R`.

**Paso 2 — Escribe tu función con documentación**

La documentación empieza con `#'` y es lo que aparece en `?mi_funcion`:

```r
#' Título breve de la función
#'
#' Descripción más detallada de qué hace.
#'
#' @param x Vector numérico de entrada.
#' @param nivel Nivel de confianza entre 0 y 1 (default: 0.95).
#'
#' @return Descripción de lo que devuelve.
#'
#' @examples
#' mi_funcion(c(1, 2, 3, 4, 5))
#'
#' @export
mi_funcion <- function(x, nivel = 0.95) {
  # tu código aquí
  mean(x) * nivel
}
```

La línea `@export` es obligatoria para que la función esté disponible
al cargar la librería.

**Paso 3 — Agrega el nombre al NAMESPACE**

Abre `libreria/NAMESPACE` y agrega una línea:

```
export(mi_funcion)
```

**Paso 4 — Recarga la librería y prueba**

```r
devtools::load_all("libreria")
mi_funcion(c(10, 20, 30))
```

---

### 8.2 Agregar datos que ya tienes

#### Desde un archivo CSV

1. Copia tu archivo a `libreria/data-raw/mis_datos.csv`

2. Agrega estas líneas al final de `libreria/data-raw/generar_datos.R`:

```r
mis_datos <- read.csv("data-raw/mis_datos.csv")
save(mis_datos, file = "data/mis_datos.rda")
```

3. Ejecuta el script (con el working directory en `libreria/`):

```r
setwd("libreria")
source("data-raw/generar_datos.R")
setwd("..")
```

#### Desde un archivo Excel

```r
# Instala readxl si no lo tienes
install.packages("readxl", repos = "https://cloud.r-project.org")

# En generar_datos.R agrega:
mis_datos <- readxl::read_excel("data-raw/mis_datos.xlsx")
save(mis_datos, file = "data/mis_datos.rda")
```

#### Desde un objeto que ya tienes en R

Si ya tienes el objeto cargado en tu sesión:

```r
save(mis_datos, file = "libreria/data/mis_datos.rda")
```

---

### 8.3 Documentar el dataset (recomendado)

Abre `libreria/R/datos.R` y agrega al final una entrada como esta:

```r
#' Nombre descriptivo del dataset
#'
#' Descripción breve: qué son los datos, de dónde vienen,
#' para qué ejercicios del curso son útiles.
#'
#' @format Data frame con N filas y M columnas:
#' \describe{
#'   \item{columna1}{Descripción de la primera columna.}
#'   \item{columna2}{Descripción de la segunda columna.}
#' }
#' @source Origen de los datos.
#' @examples
#' data(mis_datos)
#' head(mis_datos)
"mis_datos"
```

---

### 8.4 Verificar que todo funciona

```r
devtools::load_all("libreria")

# Probar la función
mi_funcion(c(1, 2, 3))

# Probar el dataset
data(mis_datos)
head(mis_datos)
str(mis_datos)
```

---

### 8.5 Usar en un capítulo del libro

Una vez que cargues la librería al inicio del capítulo, tus nuevas
funciones y datos están disponibles exactamente igual que los demás:

````markdown
```{r}
#| include: false
devtools::load_all(here::here("libreria"), quiet = TRUE)
```

```{r}
# Usar la función nueva
resultado <- mi_funcion(x)

# Usar el dataset nuevo
data(mis_datos)
summary(mis_datos)
```
````

---

## 9. Flujo de trabajo con Git

Git registra todos los cambios del proyecto. Los comandos esenciales son:

| Comando | Qué hace |
|---|---|
| `git pull` | Trae los cambios más recientes de GitHub |
| `git status` | Muestra qué archivos has modificado |
| `git add archivo.qmd` | Marca un archivo para guardar |
| `git add .` | Marca todos los archivos modificados |
| `git commit -m "mensaje"` | Guarda los cambios con una descripción |
| `git push` | Sube los cambios a GitHub |
| `git log --oneline` | Muestra el historial de cambios |

### Mensajes de commit

Escribe mensajes descriptivos en español:

```bash
git commit -m "agrego seccion de distribuciones discretas en cap02"
git commit -m "corrijo ejemplo de intervalo de confianza en cap04"
git commit -m "agrego dataset de precios en libreria"
```

---

## 10. Trabajo con ramas (branches)

Una rama es una copia independiente del proyecto donde puedes trabajar
sin afectar la versión principal (`main`). Es la forma recomendada de
colaborar cuando varias personas editan al mismo tiempo.

### ¿Por qué usar ramas?

- Evitas sobrescribir el trabajo de otros
- Tus cambios se revisan antes de integrarse al libro publicado
- Si algo sale mal, `main` sigue intacto

### Flujo recomendado

```
main ─────────────────────────────────────► (libro publicado)
         │                        ▲
         └── tu-rama ─── commits ─┘
                                 (Pull Request → revisión → merge)
```

### Comandos de ramas

| Comando | Qué hace |
|---|---|
| `git branch` | Lista todas las ramas locales |
| `git branch nombre-rama` | Crea una rama nueva |
| `git checkout nombre-rama` | Cambia a esa rama |
| `git checkout -b nombre-rama` | Crea y cambia en un solo paso |
| `git merge nombre-rama` | Fusiona una rama con la actual |
| `git branch -d nombre-rama` | Elimina una rama local |
| `git push origin nombre-rama` | Sube la rama a GitHub |

### Ejemplo completo paso a paso

**1. Asegúrate de estar en `main` y tener lo más reciente:**

```bash
git checkout main
git pull
```

**2. Crea tu rama con un nombre descriptivo:**

```bash
git checkout -b cap05-regresion-lineal
```

El nombre debe describir qué estás haciendo. Ejemplos:
- `cap05-regresion-lineal`
- `correccion-ejemplos-cap02`
- `nuevo-dataset-precios`

**3. Trabaja normalmente — edita archivos, guarda, etc.**

**4. Guarda tus avances con commits:**

```bash
git add .
git commit -m "agrego introduccion de regresion lineal"
```

Puedes hacer varios commits mientras trabajas en la misma rama.

**5. Sube tu rama a GitHub:**

```bash
git push origin cap05-regresion-lineal
```

**6. Abre un Pull Request en GitHub:**

1. Ve al repositorio en GitHub
2. Aparecerá un aviso amarillo con tu rama → clic en **Compare & pull request**
3. Escribe un título y descripción de tus cambios
4. Clic en **Create pull request**

El coordinador revisará los cambios y los integrará a `main`.
Cuando se apruebe, el libro se publicará automáticamente.

**7. Después del merge, limpia tu rama:**

```bash
git checkout main
git pull
git branch -d cap05-regresion-lineal
```

### Revisar en qué rama estás

```bash
git branch
```

La rama activa tiene un `*` al inicio:

```
* cap05-regresion-lineal
  main
```

También puedes verlo en la esquina inferior izquierda de VS Code.

### Ver todas las ramas (incluidas las de otros)

```bash
git branch -a
```

### Cambiar entre ramas sin perder cambios

Si empezaste a editar y necesitas cambiar de rama sin hacer commit:

```bash
git stash          # guarda temporalmente tus cambios
git checkout main  # cambia de rama
git stash pop      # recupera tus cambios cuando vuelvas
```

---

## 11. Subir cambios a GitHub

### Flujo normal (cambios propios sin conflictos)

```bash
# 1. Trae los últimos cambios
git pull

# 2. Revisa qué modificaste
git status

# 3. Marca los archivos
git add .

# 4. Guarda con descripción
git commit -m "descripcion de mis cambios"

# 5. Sube a GitHub
git push
```

Al hacer `git push`, GitHub Actions compilará y publicará el libro
automáticamente en 2-3 minutos.

### Si hay conflicto

Un conflicto ocurre cuando dos personas modificaron el mismo archivo.
Git te avisará con un mensaje como:

```
CONFLICT (content): Merge conflict in capitulos/parte1/cap02.qmd
```

Abre el archivo en VS Code — verás algo así:

```
<<<<<<< HEAD
Tu versión del texto
=======
La versión de la otra persona
>>>>>>> origin/main
```

Edita el archivo dejando la versión correcta, elimina las marcas
`<<<<<<<`, `=======`, `>>>>>>>`, guarda y luego:

```bash
git add capitulos/parte1/cap02.qmd
git commit -m "resuelvo conflicto en cap02"
git push
```

Si el conflicto es complicado, contacta al coordinador antes de resolverlo.

---

## 12. Preguntas frecuentes

**¿Cómo veo el libro publicado?**  
En https://mop-cimat-ags.github.io/NotasModelacionEstadistica

**¿Cuánto tarda en publicarse después de un push?**  
2 a 3 minutos. Puedes ver el progreso en:
https://github.com/mop-cimat-ags/NotasModelacionEstadistica/actions

**¿Puedo renderizar solo un capítulo?**  
Sí, desde la terminal de VS Code:
```bash
quarto render capitulos/parte1/cap02-distribuciones.qmd
```

**¿Por qué me pide usuario y contraseña al hacer push?**  
GitHub ya no acepta contraseñas normales. Debes usar un
**Personal Access Token**. Créalo en:
GitHub → Settings → Developer settings → Personal access tokens → Generate new token  
Selecciona el permiso `repo` y usa ese token como contraseña.

**¿Puedo editar directamente en GitHub sin clonar?**  
Sí, para cambios pequeños. Ve al archivo en GitHub y haz clic en el
ícono del lápiz (Edit). Esto crea un commit directo. No recomendado
para cambios grandes.

**¿Cómo agrego una imagen al capítulo?**  
1. Guarda la imagen en `imagenes/` o en una carpeta dentro de `capitulos/`
2. Refiérela en el `.qmd`:
```markdown
![Descripcion](imagenes/mi-imagen.png){width=60%}
```

**¿Qué hago si rompí algo y quiero deshacer mis cambios?**  
Si aún no hiciste commit:
```bash
git restore nombre-del-archivo.qmd
```
Si ya hiciste commit, contacta al coordinador.

---

*Guía elaborada para el proyecto Modelación Estadística — CIMAT Aguascalientes, 2024.*
