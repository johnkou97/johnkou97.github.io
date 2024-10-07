---
layout: page
title: Other Astronomical Projects
description: projects from various astronomical, astrophysical, and mathematical courses
img: assets/img/astronomy.jpg #Photo by <a href="https://unsplash.com/@grakozy?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Greg Rakozy</a> on <a href="https://unsplash.com/photos/silhouette-photography-of-person-oMpAz-DN-9I?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
importance: 4
category: courses
related_publications: false
giscus_comments: false
redirect:
pretty_table: true
---

As part of my graduate and undergraduate studies, I have completed various projects as part of my coursework. In this page, I present some of the projects that I have completed in the fields of astronomy, astrophysics, and mathematics. These projects include the analysis of astronomical data, the development of computational models, and the application of mathematical techniques to solve astrophysical problems.

## Matched Filtering in Gravitational Wave Data Analysis

This small project was part of the course "Astrostastistics" at the Leiden Observatory. The project consisted of implementing a matched filtering algorithm to detect gravitational wave signals in noisy data. The data used in this project were synthetic, and the templates used the approximations described by the VIRGO and LIGO collaborations {% cite 2017AnP...52900209A --file external %}. 

The equation of the gravitational wave signal from a binary merger was given by
\begin{equation}
    h(t) = \frac{4A\eta M}{D} \left( \pi M f(t) \right)^{2/3} \cos\left[ \phi(t) + \phi_c \right],
    \label{eq:gw_signal} 
\end{equation}
where $$A$$ is a geometric prefactor (averaged over all angles making $$A = 2/5$$), $$\eta = \frac{m_1 m_2}{M^2}$$ is the reduced mass, $$D$$ is the luminosity distance, $$M = m_1 + m_2$$ is the total mass, $$f(t)$$ is the time-dependent frequency of the wave, $$\phi(t)$$ is the phase of the wave, and $$\phi_c$$ is a constant phase. The frequency of the wave increases with time, a phenomenon known as "chirping". The chirp mass $$M_c$$ is defined as $$M_c = \frac{(m_1 m_2)^{3/5}}{(m_1 + m_2)^{1/5}}$$, and the chirpline is given by
\begin{equation}
    f_{\text{GW}}(t) = B x^{-5/8} (t_c - t)^{-3/8}, 
    \label{eq:chirpline}
\end{equation}
where $$B = 16.6 \, \text{s}^{-5/8}$$, $x$ is the chirp mass in solar masses, and $$t_c$$ is the moment of merger. The phase of the wave is given by
\begin{equation}
    \phi(t) = 2\pi B x^{-5/8} (t_c - t)^{5/8}.
    \label{eq:phase}
\end{equation}
The signal shape is then given by
\begin{equation}
    h(t) = \frac{4A\eta M \left( \pi M \right)^{2/3}}{D} \left( 16.6 x^{-\frac{5}{8}} (t_c - t)^{-\frac{3}{8}} \right)^{2/3} \cos\left[ -39.11 x^{-\frac{5}{8}} (t_c - t)^{\frac{5}{8}} + \phi_c \right]. 
    \label{eq:gw_signal_final}
\end{equation}

Equation \eqref{eq:gw_signal_final} has many parameters, some of which are degenerate. To reduce the dimensionality of the template bank, we replaced degenerate parameters with effective parameters. We can reduce the dimensionality of the template bank by considering the scale and shift symmetries of the parameters. Our model can be reduced to 
\begin{equation}
    h(t)\sim (t_c-t)^{-\frac{1}{4}}cos(-39.11x^{-\frac{5}{8}}(t_c-t)^{\frac{5}{8}}+\phi_c)
    \label{eq:gw_signal_final_simple}
\end{equation}
where $$t_c$$, $$x$$, and $$\phi_c$$ are the only real signal parameters. In practice, when we employ matched filtering, we will shift the signal in time to match the data by varying $$t_c$$, so we can argue that only $$x$$ and $$\phi_c$$ are the real signal parameters. The amplitude of the signal does not determine which signal is detected, but only how significantly it is detected in relation to the background noise, that is why the above equation has no amplitude parameter.

First we test the matched filtering algorithm on our own synthetic data. We create a signal, using equation \eqref{eq:gw_signal_final_simple}, and add Gaussian noise to it. We then filter the data and look for a spike in the filter output, which indicates a correlation with the signal. The results of the detection are shown in the figures below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/synthetic_data.png" title="Synthetic data" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/detection_synthetic_data.png" title="Detection of synthetic data" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/contour_plot_synthetic_data.png" title="Contour plot of synthetic data" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Synthetic data with a gravitational wave signal from our model and added Gaussian noise. Middle: Filter output as a function of time. Right: Contour plot of the filter output as a function of the chirp mass and the phase.
</div>

As we can see from the figures, the matched filtering algorithm is able to detect the gravitational wave signal in the synthetic data and recover the parameters we used to create the signal. Now we can tet the algorithm on the data of the exercise, which may or may not contain synthetic gravitational wave signals. We have three data streams that we need to test for gravitational wave signals. The results of the detection are shown in the figures below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/raw_1.png" title="Raw data stream 1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/time_merger_1.png" title="Time to merger for data stream 1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/contourf_1.png" title="Contour plot of data stream 1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Results of the matched filtering algorithm on data stream 1. From left to right: raw data stream, detection of the time of merger, and the contour plot of the filter output as a function of the chirp mass and the phase.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/raw_2.png" title="Raw data stream 2" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/time_merger_2.png" title="Time to merger for data stream 2" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/contourf_2.png" title="Contour plot of data stream 2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    As above, but for data stream 2.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/raw_3.png" title="Raw data stream 3" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/time_merger_3.png" title="Time to merger for data stream 3" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/contourf_3.png" title="Contour plot of data stream 3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    As above, but for data stream 3.
</div>


The matched filtering algorithm was able to detect the gravitational wave signals in two of the three data streams. For the third data stream, the algorithm detected a very weak signal, which was not significant enough to be considered a detection.The detected waves are shown in the figures below. The algorithm was able to recover the parameters of the signals, such as the chirp mass and the phase. The results of the detection are consistent with the parameters used to create the signals. The algorithm was not able to detect a gravitational wave signal in the third data stream, which did not contain a signal. The final results are summarized in the table below, for the code as well as instructions on how to run it, please visit the [GitHub repository](https://github.com/johnkou97/matched-filtering).

| Data Stream | Time of Merger | Chirp Mass | Phase | Detected |
|-------------|----------------|------------|-------|----------|
| 1           | 299.0          | 90.0       | 6.2   | Yes      |
| 2           | 1000.0         | 31.0       | 3.2   | Yes      |
| 3           | -              | -          | -     | No       |

<p></p>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/wave_1.png" title="Detected wave in data stream 1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/wave_2.png" title="Detected wave in data stream 2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Detected gravitational wave signals in data streams 1 and 2 plotted against the raw data.
</div>


## Stellar Structure and Evolution Lab Assignment


For the course "Stellar Structure and Evolution" at the Leiden Observatory, I completed a project on the evolution of a star from the protostar phase to the white dwarf phase. The project used the Modules for Experiments in Stellar Astrophysics (MESA) code to simulate the evolution of a 1 solar mass star and a 2 solar mass star of solar composition. The project aimed to study the differences in the evolution of the two stars and to understand the physical processes that drive the evolution of stars.

For the star evolution simulation, we used the MESA code {% cite 2011ApJS..192....3P 2013ApJS..208....4P 2015ApJS..220...15P 2018ApJS..234...34P 2019ApJS..243...10P 2023ApJS..265...15J --file external %}. For more information on the MESA code, please visit the documentation on the [MESA website](https://docs.mesastar.org/en/23.05.1/).

The evolution of the stars was studied by plotting the density as a function of the central temperature in a log-log plot. The different regions where each equation of state dominates were identified. We have four different equations of state: 

$$P_{\text{gas}} = \frac{R}{\mu} T \rho \quad \text{(ideal gas)}, \quad P_{\text{e}} = K_{\text{NR}} \left( \frac{\rho}{\mu_e} \right)^{5/3} \quad \text{(non-relativistic degenerate electron gas)},$$
$$ P_{\text{e}} = K_{\text{ER}} \left( \frac{\rho}{\mu_e} \right)^{4/3} \quad \text{(extreme relativistic degenerate electron gas)}, \quad P_{\text{rad}} = \frac{a T^4}{3} \quad \text{(radiation pressure)},$$

for the different phases that a gas can have. We denote with $$P_{\text{gas}}$$ the gas pressure, $$P_{\text{e}}$$ the electron pressure, $$P_{\text{rad}}$$ the radiation pressure, $$R$$ the gas constant, $$\mu$$ the mean molecular weight, $$\mu_e$$ the mean molecular weight per electron, $$K_{\text{NR}}$$ the non-relativistic degeneracy constant, $$K_{\text{ER}}$$ the extreme relativistic degeneracy constant, $$a$$ the radiation constant, and $$T$$ the temperature. While stars evolve, they can go through different phases where different equations of state dominate. In the plots below, we can see the evolution of the 1 solar mass star and the 2 solar mass star and the different regions that they go through.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/loglog_1.0.png" title="Log-log plot for the 1 solar mass star" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/loglog_2.0.png" title="Log-log plot for the 2 solar mass star" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The evolution of the 1 solar mass star (left) and the 2 solar mass star (right) in a log-log plot of the density as a function of the central temperature. In the plot, we can see the different regions where each equation of state dominates. The different evolutionary stages of the star are plotted with different colors. The color of the points shows their age. The relative position of the Sun is also depicted.
</div>

We can also see the evolution of the stars in a Hertzsprung-Russell diagram, which is a log-log plot of the luminosity as a function of the effective temperature. In a typical Hertzsprung-Russell diagram there are different regions where stars are located depending on their evolutionary stage. As stars evolve, they move through these regions, starting from the protostar phase, then the main sequence, where they spend most of their lives, and finally they go through the red giant phase, the horizontal branch and the asymptotic giant branch, to end up as white dwarfs. The Hertzsprung-Russell diagrams for the 1 solar mass star and the 2 solar mass star are shown below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/HR_1.0.png" title="Hertzsprung-Russell diagram for the 1 solar mass star" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/HR_2.0.png" title="Hertzsprung-Russell diagram for the 2 solar mass star" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Hertzsprung-Russell diagrams (log-log plots of the luminosity as a function of the effective temperature) for the 1 solar mass star (left) and the 2 solar mass star (right) showing the evolution of the stars from the protostar phase to the white dwarf phase. As above, the different evolutionary stages of the star are plotted with different colors. The color of the points shows their age. 
</div>

Finally, we can study the gradients of the stars as a function of the radius of the star. The gradients are important because they determine the energy transport mechanism in the star. When the adiabatic gradient is larger than the radiative gradient, the star is convective. The gradients of the 1 solar mass star and the 2 solar mass star for the pre-main sequence phase and the main sequence phase are shown below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/gradients_1.0.png" title="Gradients for the 1 solar mass star" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/gradients_2.0.png" title="Gradients for the 2 solar mass star" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The gradients of the 1 solar mass star (left) and the 2 solar mass star (right) as a function of the radius of the star. Each plot contains two panels, one for the pre-main sequence phase and one for the main sequence phase. Each time we plot the adiabatic and the radiative gradients. When the adiabatic gradient is larger than the radiative gradient, the star is convective, which is shown by the grey area in the plot.
</div>

This project was a great opportunity to learn about the physical processes that drive the evolution of stars and to understand the different regions that stars go through as they evolve. The MESA code is a powerful tool that allows us to simulate the evolution of stars and to study the physical processes that drive their evolution. For the code as well as instructions on how to run it, please visit the [GitHub repository](https://github.com/johnkou97/stellar_evolution) or you can check the final report [here](/assets/pdf/stellar_evolution.pdf).


## MODELLING SUB-NEPTUNE MASS PLANETS INTERIOR


As part of the course "Exo-planets" at the Leiden University, I completed a project on the evolution of low-mass planets with an envelope made mostly of hydrogen and helium. The project aimed to simulate the interiors and evolution of these planets and to study how irradiation from a central star affects their structure and evolution. The project followed previous work {% cite 2016ApJ...831..180C --file external %} and used the Modules for Experiments in Stellar Astrophysics (MESA) {% cite 2011ApJS..192....3P 2013ApJS..208....4P 2015ApJS..220...15P 2018ApJS..234...34P 2019ApJS..243...10P 2023ApJS..265...15J --file external %} code to simulate the evolution of the planets.

<!-- Methods
The way we work with the code starts by creating a single planet, which we then
modify in order to give it the parameters we desire. In the first step we create a
single planet with M = 30Mearth. This is our initial planet and it is coreless and
also has no heavy elements, which means it only consists of a mix of H and He gas.
In the next step we create a core for the planet. The core will have the same
composition as that of the Earth which means that we can use the equation from
[2]:
R
R⊕
=

M
M⊕
!0.27
⇒ ρ = ρ⊕

M
M⊕
!0.19
(1)
We want to create 5 different planets with different mass cores. We can see all
the different values with the calculated density in the Table 1.
Core Mass density (gr/cm3
)
3M⊕ 6.801
5M⊕ 7.494
7M⊕ 7.989
10M⊕ 8.549
12M⊕ 8.851
Table 1: The core mass of the different planets and the mean density of the core.
The next step is to reduce the mass of our planets from the 30M⊕ that they are
now. In order to do that we reduce the mass of the gaseous envelope, that surrounds
the core. For each planet we will create 2 different planets for different values of the
ratio between the mass of the envelope and the total mass of the planet.
fenv =
Menv
Mp
where Mp = Menv + Mcore (2)
which leads to:
Mp =
Mcore
1 − fenv
(3)
After that we can create 2 planets for each core mass, by using 2 different values
for the fenv. The final masses are shown in the Table 2:
After that we want to add an artificial luminosity that will deposit some energy
inside the planets. The result of this process is the inflation of the planets which
will affect the initial entropy at the base of the gaseous envelope of each planet. The
artificial luminosity that we implement is Lcenter = 2 · 1027erg/sec .
1
Core Mass fenv Total Mass
3M⊕
0.1 1.001 · 10−5M⊙
0.01 9.104 · 10−6M⊙
5M⊕
0.1 1.669 · 10−5M⊙
0.01 1.517 · 10−5M⊙
7M⊕
0.1 2.337 · 10−5M⊙
0.01 2.124 · 10−5M⊙
10M⊕
0.1 3.338 · 10−5M⊙
0.01 3.035 · 10−5M⊙
12M⊕
0.1 4.006 · 10−5M⊙
0.01 3.642 · 10−5M⊙
Table 2: The total mass of the planet for the different values of the core mass and
fenv. Note that the final mass is in solar masses while the core mass is in units of
earth masses.
The final step is to see how the planets evolve. During the evolution we set a
new more realistic luminosity:
Lcenter = 5Mcore · 10−8
erg/sec (4)
where Mcore is in units of gr
We can see the results in Table 3
Core Mass Luminosity (erg/sec)
3M⊕ 8.965 · 1020
5M⊕ 1.494 · 1021
7M⊕ 2.092 · 1021
10M⊕ 2.988 · 1021
12M⊕ 3.586 · 1021
Table 3: The core mass of the different planets and the artificial core luminosity.
Note that we only have 5 cases for the different core masses because the pairs of
the planets that share the same core mass will have the same artificial luminosity
added.
We then let the system evolve for a timescale of 5 · 109
yr and we get our final
results. -->

The project started by creating a single planet with a mass of 30 Earth masses. The planet was coreless and consisted only of a mix of hydrogen and helium gas. The next step was to create a core for the planet. The core had the same composition as the Earth, which allowed us to calculate the density of the core. We created five different planets with different core masses and densities, 3, 5, 7, 10, and 12 Earth masses. After creating the core, we reduced the mass of the planets by reducing the mass of the gaseous envelope that surrounded the core. For each core mass, we created two different planets with different values for the ratio between the mass of the envelope and the total mass of the planet. The final masses of the planets are shown in the table below.

| Core Mass | fenv | Total Mass |
|-----------|------|------------|
| 3M⊕      | 0.1  | 1.001 · 10⁻⁵M⊙ |
|           | 0.01 | 9.104 · 10⁻⁶M⊙ |
| 5M⊕      | 0.1  | 1.669 · 10⁻⁵M⊙ |
|           | 0.01 | 1.517 · 10⁻⁵M⊙ |
| 7M⊕      | 0.1  | 2.337 · 10⁻⁵M⊙ |
|           | 0.01 | 2.124 · 10⁻⁵M⊙ |
| 10M⊕     | 0.1  | 3.338 · 10⁻⁵M⊙ |
|           | 0.01 | 3.035 · 10⁻⁵M⊙ |
| 12M⊕     | 0.1  | 4.006 · 10⁻⁵M⊙ |
|           | 0.01 | 3.642 · 10⁻⁵M⊙ |

<p></p>

The next step was to add an artificial luminosity that would deposit some energy inside the planets. The result of this process was the inflation of the planets, which affected the initial entropy at the base of the gaseous envelope of each planet. The artificial luminosity that was implemented was $$L_{\text{center}} = 2 \times 10^{27} \, \text{erg/sec}$$. The final step was to see how the planets evolved. During the evolution, a new more realistic luminosity was set, $$L_{\text{center}} = 5M_{\text{core}} \times 10^{-8} \, \text{erg/sec}$$, where $$M_{\text{core}}$$ is in units of grams. The planets were allowed to evolve for a timescale of $$5 \times 10^9$$ years. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/M-t.png" title="Mass as a function of time" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/M-R.png" title="Mass as a function of radius" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: The radius of the planets as a function of time (right panel focuses more on the smaller radii). Right: The evolved exoplanets plotted in a mass-radius diagram with real exoplanets for comparison (on the left we have noted the real exoplanets that most closely resemble our models).
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/gradients.png" title="Gradients as a function of radius" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/T-P.png" title="Temperature as a function of pressure" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: The gradients of the planets as a function of the radius of the planet. Right: The temperature as a function of the pressure in the planets. Each panel is for a different planet.

## Interstellar Medium



## Numerical Analysis



## References

{% bibliography --cited --file external %}
