# Cmin-Based popPK/PD Retro-Dosimetry Simulation


## Overview

This repository contains an end-to-end synthetic simulation workflow
demonstrating:

**Dose → Population PK → Cmin → Cytokine Inhibition → Translational
Survival Rule → PTA → Dose Selection**

🔗 HTML Overview:
(https://tjmb03.github.io/Retro-Dosimetry/)

The goal is to illustrate how retro-dosimetry and popPK modeling can be
integrated to support rational dose selection based on a mechanistic
biomarker threshold.

------------------------------------------------------------------------

## Scientific Objective

We assume:

-   ≥70% cytokine inhibition is required
-   That level supports ≥80% probability of achieving ≥80% retinal
    ganglion cell (RGC) survival
-   We want ≥80% of patients to achieve that inhibition threshold

This framework allows us to:

1.  Convert a biological inhibition requirement into a **Cmin target**
    (retro-dosimetry)
2.  Simulate population PK variability
3.  Estimate **PTA = P(Cmin ≥ Cmin_target)**
4.  Identify the minimal dose meeting the program criterion

------------------------------------------------------------------------

## Model Components

### 1. Population PK

-   1-compartment model
-   First-order absorption
-   Log-normal inter-individual variability on CL, V, and KA

### 2. PD Model

Inhibitory Imax model:

I(C) = Imax \* C\^γ / (IC50\^γ + C\^γ)

### 3. Retro-Dosimetry

Solve for Cmin such that:

I(Cmin) ≥ 0.70

This gives:

Cmin_target = IC50 \* (0.70 / (Imax − 0.70))\^(1/γ)

### 4. Dose Selection

We compute:

PTA = P(Cmin ≥ Cmin_target)

Minimal dose achieving:

PTA ≥ 0.80

is selected.

------------------------------------------------------------------------

## Key Outputs

The R Markdown file generates:

-   Dose → PTA tables
-   Cmin distribution summaries
-   PTA vs Dose plots
-   Automatic selection of minimal dose meeting target

<img width="849" height="544" alt="Screenshot 2026-02-15 at 1 09 18 PM" src="https://github.com/user-attachments/assets/39b3ef8d-92e8-4815-82bd-8d294d6327fb" />


------------------------------------------------------------------------

## How to Run

1.  Open the `.Rmd` file in RStudio.
2.  Install required packages if needed:

``` r
install.packages(c("rxode2", "dplyr", "tibble", "purrr", "ggplot2"))
```

3.  Click **Knit** to generate the HTML report.

------------------------------------------------------------------------

## File Structure

-   `Cmin_popPKPD_retro_dosimetry_simulation.Rmd`\
    Main simulation workflow

-   `README.md`\
    This documentation file

------------------------------------------------------------------------

## Intended Use

This example is suitable for:

-   Translational PK/PD strategy discussions
-   Biomarker-driven dose selection frameworks
-   Demonstrating retro-dosimetry concepts
-   Teaching popPK simulation workflows

------------------------------------------------------------------------

## Notes

-   All parameters are synthetic and for demonstration purposes only.
-   Simulation assumes steady-state conditions.
-   For regulatory use, incorporate uncertainty propagation and
    parameter estimation.

------------------------------------------------------------------------

## License

This project is provided for educational and methodological
demonstration purposes.
