
<!-- README.md is generated from README.Rmd. Please edit that file -->

# facilityepimath

<!-- badges: start -->
<!-- badges: end -->

The goal of facilityepimath is to provide functions to calculate useful
quantities for a user-defined differential equation model of infectious
disease transmission among individuals in a healthcare facility,
including the basic facility reproduction number and model equilibrium.

## Installation

You can install the development version of facilityepimath from
[GitHub](https://github.com/) with:

``` r
# install.packages("pak")
pak::pak("damontoth/facilityepimath")
```

## Example

The functions in this package analyze compartmental differential
equation models, where the compartments are states of individuals who
are co-located in a healthcare facility, for example, patients in a
hospital or patients/residents of long-term care facility.

Our example here is a hospital model with four compartments: two
compartments $C_1$ and $C_2$ representing patients who are colonized
with an infectious organism, and two compartments $S_1$ and $S_2$
representing patients who are susceptible to acquiring colonization with
that same organism. The two colonized and susceptible states are
distinguished by having potentially different infectivity to other
patients and vulnerability to acquisition from other patients,
respectively.

A system of differential equations with those 4 compartments may take
the following general form:

$$\frac{dS_1}{dt} = -(s_{21}+(a_{11}+a_{21})\alpha+\omega_1+h(t))S_1 + s_{12}S_2 + r_{11}C_1 + r_{12}C_2$$

$$\frac{dS_2}{dt} = s_{21}S_1 - (s_{12}+(a_{12}+a_{22})\alpha+\omega_2+h(t))S_2 + r_{21}C_1 + r_{22}C_2 $$

$$\frac{dC_1}{dt} = a_{11}\alpha S_1 + a_{12}\alpha S_2 - (c_{21}+r_{11}+r_{21}+\omega_3+h(t))C_1 + c_{12}C_2 $$

$$\frac{dC_2}{dt} = a_{21}\alpha S_1 + a_{22}\alpha S_2 + c_{21}C_1 - (c_{12}+r_{12}+r_{22}+\omega_4+h(t))C_2 $$

The acquisition rate $\alpha$ appearing in each equation, and governing
the transition rates between the S compartments and the C compartments,
is assumed to depend on the number of colonized patients in the
facility, as follows:

$$ \alpha = \beta_1 C_1 + \beta_2 C_2 $$

We will demonstrate how to calculate the basic reproduction number $R_0$
of this system using the `facilityR0` function. The following components
of the system are required as inputs to the function call below.

A matrix `S` governing the transitions between, and out of, the states
$S_1$ and $S_2$ in the absence of any colonized patients:

$$S = \left(
\begin{matrix}
    -s_{21}-\omega_1 & s_{12} \\
    s_{21} & -s_{12}-\omega_2
\end{matrix}\right)
$$

A matrix `C` governing the transitions between, and out of, the states
$C_1$ and $C_2$:

$$C = \left(
\begin{matrix}
    - (c_{21}+r_{11}+r_{21}+\omega_3) & c_{12} \\
    c_{21} & - (c_{12}+r_{12}+r_{22}+\omega_4)
\end{matrix}\right)
$$

``` r
library(facilityepimath)
## basic example code will go here
```
