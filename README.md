# Simulación de Sistemas Híbridos con un Modelo Unificado (Modelo-κ)

Este repositorio contiene el código y los resultados de un Trabajo de Fin de Grado que explora la dinámica de sistemas híbridos clásico-cuánticos. El proyecto se centra en el uso de un marco teórico unificado, basado en el formalismo de Koopman y el Modelado Dinámico Operacional (ODM), para analizar la transición entre los regímenes clásico y cuántico.

## Resumen del Proyecto

El principal desafío en la física de sistemas híbridos es formular una dinámica que sea matemáticamente consistente y físicamente significativa. Este trabajo aborda este problema mediante un **modelo dinámico unificado** que depende de un parámetro de deformación continuo, $\kappa \in [0,1]$. Este parámetro interpola suavemente entre:
- **$\kappa = 0$**: El límite clásico, correspondiente al formalismo de **Koopman-von Neumann (KvN)**.
- **$\kappa = 1$**: El límite cuántico, correspondiente a la mecánica cuántica de Heisenberg.

A través de la implementación numérica de un sistema de dos osciladores armónicos acoplados, se investigan fenómenos clave como la **retro-reacción (back-reaction)**, la **covarianza** entre subsistemas, el **entrelazamiento** y la validez de las relaciones de conmutación en todo el espectro de la transición.

## Marco Teórico

El formalismo se basa en una representación de la mecánica clásica en un espacio de Hilbert, generalizando el enfoque de Koopman. Los elementos clave son:
- **Álgebra Extendida:** Para el subsistema clásico, se utilizan cuatro operadores fundamentales: los observables de posición y momento ($\hat{x}, \hat{p}$) y sus momentos conjugados ($\hat{\lambda}_x, \hat{\lambda}_p$), que actúan como generadores de traslaciones.
- **Operadores Mixtos:** Se define un isomorfismo entre el álgebra cuántica y la clásica extendida mediante los **operadores mixtos**, que dependen de $\kappa$:
  
  $$\hat{x}_q = \hat{x} - \frac{\hbar\kappa}{2}\hat{\lambda}_p \quad , \quad \hat{p}_q = \hat{p} + \frac{\hbar\kappa}{2}\hat{\lambda}_x$$
- **Relación de Conmutación Unificada:** Estos operadores obedecen una relación de conmutación deformada que es el núcleo del modelo:

  $$[\hat{x}_q, \hat{p}_q] = i\hbar\kappa$$

## Análisis Realizados

El código de este repositorio realiza los siguientes análisis numéricos:
1.  **Validación del Modelo:** Se verifica que la dinámica, la retro-reacción y el espectro del generador son independientes de $\kappa$ para $\kappa > 0$ en el caso sin acoplo, y convergen al límite de KvN ($\kappa=0$).
2.  **Análisis del Conmutador Mixto:** Se demuestra numéricamente que el valor esperado del conmutador unificado satisface $\langle[ X_{mix}, P_{mix}]\rangle = i\hbar\kappa$, y se analiza cómo la validez de esta relación depende del tamaño de la base de Hilbert truncada.
3.  **Análisis de Retro-reacción:** Se estudia la retro-reacción como un artefacto numérico del truncamiento de la base en el límite clásico ($\kappa=0$), mostrando su convergencia a cero al aumentar el tamaño de la base.
4.  **Estudio de Observables y Correlaciones:** Se analiza la evolución de diversos valores esperados (posiciones, momentos, operadores cuadráticos) y de la **covarianza** $Cov(\hat{X}_{mix}, \hat{X}_Q)$ en función del tiempo y de $\kappa$.
5.  **Cuantificación del Entrelazamiento:** Se mide el entrelazamiento entre los subsistemas clásico y cuántico a través de la pureza de la matriz densidad reducida, $\mathcal{P} = \text{Tr}(\rho_C^2)$.
6.  **Visualizaciones Dinámicas:** Se incluyen animaciones que muestran la evolución de la densidad de probabilidad en la base de Fock y en el espacio de posiciones/fases (mediante la función de Husimi).

## Estructura del Repositorio

-   `OsciladorMixtoCuantico.ipynb`: El cuaderno de Jupyter principal que contiene todo el código, los análisis y las visualizaciones.
-   `fig_config.py`: Módulo auxiliar con funciones para la configuración de los gráficos de Matplotlib.
-   `/Output/`: Directorio donde se guardan las figuras y animaciones generadas (creado automáticamente).

## Instalación y Uso

Para ejecutar este proyecto, se recomienda crear un entorno virtual de Python y instalar las dependencias.

1.  **Clonar el repositorio:**
    ```bash
    git clone https://github.com/tu-usuario/tu-repositorio.git
    cd tu-repositorio
    ```

2.  **Crear un entorno e instalar dependencias:**
    ```bash
    python -m venv env
    source env/bin/activate  # En Windows: env\Scripts\activate
    pip install -r requirements.txt
    ```

    **`requirements.txt`:**
    ```
    numpy
    matplotlib
    scipy
    tqdm
    ipykernel
    pillow
    ```

3.  **Ejecutar el Cuaderno:**
    Inicia Jupyter Lab o Jupyter Notebook y abre el archivo `OsciladorMixtoCuantico.ipynb`.
    ```bash
    jupyter lab
    ```
    Puedes ejecutar las celdas en orden. Los parámetros principales del modelo (tipo de potencial, tipo de acoplo, `epsilon`, `kappa`, etc.) se pueden modificar en la celda de "Configuración del Sistema" para explorar diferentes escenarios. **IMPORTANTE:** Por defecto, el guardado de animaciones y figuras está desactivado. Para activarlo, cambiar los bools `SAVE_ANIMS` y `SAVE_FIGS` en la celda de configuración. 

## Citación

Si utilizas este trabajo, por favor, cita la memoria de TFG correspondiente:

```bibtex
@thesis{Puyol2024,
  author  = {Puyol Miano, Santiago},
  title   = {Aplicaciones del formalismo de Koopman en la dinámica de sistemas estadísticos híbridos clásico-cuánticos},
  school  = {Universidad de Zaragoza},
  year    = {2025},
  type    = {Trabajo de Fin de Grado en Física},
  address = {Zaragoza, España},
  supervisor = {Clemente Gallardo, Jesús}
}
```
