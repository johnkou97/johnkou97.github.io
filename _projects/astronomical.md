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
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/detection_synthetic_data.png" title="Detection of synthetic data" class="img-fluid rounded z-depth-1" %}
    </div>
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/contour_synthetic_data.png" title="Contour plot of synthetic data" class="img-fluid rounded z-depth-1" %}
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


## Stellar Evolution



## Exoplanets



## Interstellar Medium



## Numerical Analysis



## References

{% bibliography --cited --file external %}
