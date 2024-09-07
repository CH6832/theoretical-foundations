# Summary of Physics III: Experiments

**Authors:** Erhan Gülmez & Zuhal Kaplan  
**Date:** \today

## Table of Contents

- [Part I: Basic Methods](#part-i-basic-methods)
  - [Introduction](#introduction)
  - [Data Taking and Analysis](#data-taking-and-analysis)
    - [Dimensions and Units](#dimensions-and-units)
    - [Measurement and Instruments](#measurement-and-instruments)
      - [Reading Analog Scales](#reading-analog-scales)
      - [Data Logger](#data-logger)
    - [Basics of Statistics and Data Analysis](#basics-of-statistics-and-data-analysis)
      - [Sample and Parent Population](#sample-and-parent-population)
      - [Mean and Standard Deviation](#mean-and-standard-deviation)
      - [Distributions](#distributions)
    - [Errors](#errors)
      - [Errors in Measurements: Statistical and Systematic Errors](#errors-in-measurements-statistical-and-systematic-errors)
      - [Reporting Errors: Significant Figures and Error Values](#reporting-errors-significant-figures-and-error-values)
      - [Rounding Off](#rounding-off)
      - [Weighted Averages](#weighted-averages)
      - [Error Propagation](#error-propagation)
      - [Multivariable Measurements: Fitting Procedures](#multivariable-measurements-fitting-procedures)
    - [Reports](#reports)
- [Part II: Experiments](#part-ii-experiments)
  - [Measurement of Resistance - Ohm’s Law](#measurement-of-resistance---ohms-law)
  - [Ammeters and Voltmeters](#ammeters-and-voltmeters)
  - [Wheatstone Bridge](#wheatstone-bridge)
  - [Force Between Charged Plates](#force-between-charged-plates)
  - [The Cathode Ray Oscilloscope (CRO)](#the-cathode-ray-oscilloscope-cro)
  - [Characteristics of a Capacitor](#characteristics-of-a-capacitor)
  - [Force Between Current-Carrying Wires](#force-between-current-carrying-wires)
- [Appendices](#appendices)
  - [Physical Constants](#physical-constants)
  - [Conversion Tables](#conversion-tables)
  - [References](#references)

## Part I: Basic Methods

### Introduction

This section provides an overview of the fundamental concepts and methods used in experimental physics. It sets the stage for understanding how to collect and analyze experimental data effectively.

### Data Taking and Analysis

#### Dimensions and Units

**Units** are standard quantities used to measure physical properties. Common units include meters (m) for length, kilograms (kg) for mass, and seconds (s) for time. 

**Dimensions** refer to the physical nature of a quantity. For example:
- Length: \([L]\)
- Mass: \([M]\)
- Time: \([T]\)

#### Measurement and Instruments

Accurate measurements rely on understanding and using various instruments properly. Some key instruments include:
- **Rulers and Calipers:** Used to measure length with precision.
- **Multimeters:** Measure electrical quantities such as voltage, current, and resistance.

##### Reading Analog Scales

Analog scales require interpretation of the needle's position, which involves understanding the scale's resolution and the smallest division.

##### Data Logger

A data logger is an electronic device that records data over time. It is useful for capturing continuous measurements and analyzing trends in data.

#### Basics of Statistics and Data Analysis

##### Sample and Parent Population

- **Sample:** A subset of a population used for measurement purposes.
- **Parent Population:** The entire group from which the sample is drawn.

##### Mean and Standard Deviation

- **Mean** (\(\bar{x}\)): The average of a set of values.
  
  $\bar{x} = \frac{1}{N} \sum_{i=1}^N x_i
 $ 
  where \( \bar{x} \) is the mean, \( x_i \) are the individual data points, and \( N \) is the number of data points.

- **Standard Deviation** (\(\sigma\)): Measures the dispersion of data points around the mean.
  
  $\sigma = \sqrt{\frac{1}{N-1} \sum_{i=1}^N (x_i - \bar{x})^2}
 $ 
  where \( \sigma \) is the standard deviation.

##### Distributions

The **Normal Distribution** is a common probability distribution described by the Gaussian function:

$f(x) = \frac{1}{\sigma \sqrt{2 \pi}} \exp \left( -\frac{(x - \bar{x})^2}{2 \sigma^2} \right)$

where \( \sigma \) is the standard deviation and \( \bar{x} \) is the mean.

#### Errors

##### Errors in Measurements: Statistical and Systematic Errors

- **Statistical Errors:** Random variations that occur due to fluctuations in measurements.
- **Systematic Errors:** Consistent inaccuracies resulting from flaws in the measurement process.

##### Statistical Errors

These are typically quantified by the standard deviation, which reflects the precision of the measurements.

##### Systematic Errors

These errors are identified and corrected to improve accuracy and reliability in measurements.

##### Reporting Errors: Significant Figures and Error Values

- **Significant Figures:** The digits in a number that are important in determining its precision.
- **Error Values:** Represent the uncertainty in measurements, which should be reported along with the data.

##### Rounding Off

Use standard rules for rounding numbers based on the number of significant figures required.

##### Weighted Averages

The weighted average is calculated as:

$\bar{x}_{w} = \frac{\sum_{i=1}^N w_i x_i}{\sum_{i=1}^N w_i}$

where \( w_i \) are the weights and \( x_i \) are the measured values.

##### Error Propagation

When dealing with multiple variables, the propagated error is given by:

$\sigma_f = \sqrt{\left(\frac{\partial f}{\partial x_1} \sigma_{x_1}\right)^2 + \left(\frac{\partial f}{\partial x_2} \sigma_{x_2}\right)^2 + \cdots + \left(\frac{\partial f}{\partial x_n} \sigma_{x_n}\right)^2}$

where \( \sigma_f \) is the propagated error in the function \( f \), and \( \frac{\partial f}{\partial x_i} \) are the partial derivatives of \( f \) with respect to each variable \( x_i \), with \( \sigma_{x_i} \) being the error in \( x_i \).

##### Multivariable Measurements: Fitting Procedures

Techniques like least-squares fitting are used to analyze data involving multiple variables and find the best fit for the data.

#### Reports

This section covers how to structure scientific reports, including sections for methodology, results, and conclusions.

## Part II: Experiments

### Measurement of Resistance - Ohm’s Law

Ohm's Law describes the relationship between voltage (\(V\)), current (\(I\)), and resistance (\(R\)):

$V = IR$

where \( V \) is the voltage across a component, \( I \) is the current through it, and \( R \) is the resistance. This experiment involves measuring \( V \) and \( I \) to determine \( R \).

### Ammeters and Voltmeters

- **Ammeters:** Measure current and should be connected in series with the circuit.
- **Voltmeters:** Measure voltage and should be connected in parallel across the component.

### Wheatstone Bridge

The Wheatstone Bridge is a circuit used to measure unknown resistances. The bridge is balanced when:

$\frac{R_1}{R_2} = \frac{R_3}{R_x}$

where \( R_x \) is the unknown resistance.

### Force Between Charged Plates

The electrostatic force \( F \) between two parallel charged plates separated by a distance \( d \) is given by:

$F = \frac{Q^2}{4 \pi \epsilon_0 d^2}$

where \( Q \) is the charge on each plate and \( \epsilon_0 \) is the permittivity of free space.

### The Cathode Ray Oscilloscope (CRO)

A Cathode Ray Oscilloscope (CRO) is used to visualize electrical signals. Key features include:
- **Trace:** The graphical representation of the signal on the oscilloscope screen.
- **Time Base:** Controls the horizontal sweep of the trace.

### Characteristics of a Capacitor

Capacitors are components that store and release electrical energy. The relationship between charge \( Q \), voltage \( V \), and capacitance \( C \) is:

$Q = CV$

The time constant \( \tau \) for charging and discharging a capacitor is given by:

$\tau = RC$

where \( R \) is the resistance in the circuit.

### Force Between Current-Carrying Wires

The force \( F \) between two parallel wires carrying currents \( I_1 \) and \( I_2 \) is described by:

$F = \frac{\mu_0 I_1 I_2 L}{2 \pi d}$

where \( \mu_0 \) is the permeability of free space, \( L \) is the length of

 the wires, and \( d \) is the distance between them.

## Appendices

### Physical Constants

This appendix includes a list of physical constants relevant to the experiments, such as the speed of light, gravitational constant, and fundamental charge.

### Conversion Tables

Tables for converting between different units of measurement, such as length, mass, and time.
