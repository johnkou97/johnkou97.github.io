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

<!-- Tutorial on the essentials of gravitational wave detection (2020)
This tutorial focuses on an idealized detection of gravitational waves emitted during the inspiral
and merger of compact binary objects. The used data are synthetic, and the templates use the
approximations described by VIRGO and LIGO in Ann. Phys. 529 (2017).
Exercise 1: Gravitational wave signals . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
We focus on the inspiral and merger of two compact objects, e.g. two black holes or two neutron stars. From
the masses m1 and m2 , we define the total mass M = m1 + m2 and the reduced mass,
η=
m1 m2
.
M2
(1)
Let then D be the (luminosity-)distance of the event, and let A be a geometric prefactor which depends on
the relative orientation between the merging system and the interferometric detector. (Averaging over all
angles, one has A = 2/5.)
The natural data domain of gravitational wave interferometers is the time domain: The interferometers de-
tect a strain h, as a function of time t1 . A gravitational wave signal from a binary merger can be represented
in the time domain as
2
4AηM
h(t) =
(2)
[πM f (t)] 3 cos[φ(t) + φc ].
D
The function f (t) describes how the wave frequency increases with time. Gravitational waves are quadrupo-
lar, and the quadrupole moment of a binary system has spin-2. Consequently, the wave frequency is twice
the orbital frequency of the inspiralling objects. The function
Z t
φ(t) = 2π
f (t0 )dt0 ,
(3)
tracks the progress of the objects on their orbits; hence the integral.
1) Scaling relations: Explain why the amplitude of the strain increases proportional to η, M and A, and
why it decreases inversely with D.
2) Chirping: Employ Keplerian dynamics to explain how the ‘chirping’ of gravitational waves arises.
Chirping describes the increase of frequency f as a function of time.
3) Computing the chirpline: We introduce the ‘chirp mass’ as
M=
1
(m1 m2 )3/5
.
(m1 + m2 )1/5
The t here used, is calendar time on Earth.
Page 1 of 3
(4)Advanced Astrostatistics
Lecturer: Dr. Elena Sellentin
Fig. 1: Left: Chirpline (red overlay), as computed from f (t) given in Eq. (5). The background is the original plot
from Abbott et al., Phys Rev. Lett. 116 (2016).
Right: Exemplary templates of gravitational wave forms resulting from our approximations. The ringdown is
missing, but the acceleration of the phase during the inspiral is included. The legend indicates the chirp mass
M, and merger takes place at tc = 10s.
This leads to the ‘chirpline’ which relates chirp mass and timevolution of the frequency


1
GM −5/8
fGW (t) =
(tc − t)−3/8 ,
40π
c3
(5)
where tc is the moment of merger. Expressing the chirp mass in multiples of solar masses, M = xM , and
plugging in G and c, the chirpline facilitates to
fGW (t) = B x−5/8 (tc − t)−3/8 ,
B = 16.6 s−5/8 .
(6)
The units of B are seconds to the −5/8, such that the units of f are correctly in Hertz. Typical values for x
are 20-40 (solar masses). For the phase of the cosine, we require the integral of Eq. (6) which is
 
3
−5/8
φ(t) = 2πBx
−
(tc − t)5/8 .
(7)
8
• Plot the chirplines Eq. (6) for different masses x and merger times tc . You will recognize the typical
upsweep in frequency prior to merger, as also visible in the original LIGO data, see Fig. 1.
• Plug the chirpline (Eq. 6), and the phase (Eq. 7) into the strain equation (Eq. 2). Ignore the prefactor.
Plot strains h(t) for different values of x. You should get waves similar to the right panel of Fig. 1.
Outcome of the exercise: you have understood the essentials of Gravitational Wave scaling
relations. You are able to compute chirplines f (t) and detector strains h(t) for different chirp
masses.
Exercise 2: Creating a template bank for gravitational waves . . . . . . . . . . . .
Gravitational wave detection employs matched filtering, for which a template bank needs to be created
first. This bank hosts the variety of potential signal shapes and in this exercise we will learn the essentials
of how to create one.
In Exercise 1 we saw that the signal shape is given by
h(t) =
2
2
h
i
5
3
5
5
4AηM [πM ] 3 
3
16.6 x− 8 (tc − t)− 8
cos −39.11 x− 8 (tc − t) 8 + φc .
D
Page 2 of 3
(8)Advanced Astrostatistics
Lecturer: Dr. Elena Sellentin
1) Parameter study: Keeping all other parameters fixed, which effect does φc have? Keeping all other
parameters fixed, which effect does tc have, and which does x have?
2) Prior ranges: Which natural prior range does φc have? Given the LIGO and VIRGO sensitivities, which
sensible prior range can you introduce for x?
3) Scale and shift symmetries: Parameters which simply scale an amplitude, and parameters which
introduce mere shifts of the signal, are not regarded as real signal parameters in matched filtering. This
is because in matched filtering, the amplitude does not determine which signal is detected, but only how
significantly it is detected, in relation to the background noise. Shift parameters simply determine where
in the data stream a signal is found, but not which signal is found. For the gravitational waves, which
parameters are shift and scale parameters?
4) Dimensionality reduction: Efficient template banks sweep through as few parameters as possible.
Currently, Eq. (8) employs six parameters: m1 , m2 , A, D, tc , φc . These are too many. Investigate Eq. (8), and
find out which parameters are degenerate. Show that by replacing degenerate parameters with effective
parameters, you can reduce the dimensionality of your template bank from 6 to 22 . If you succeed to reduce
the dimensionality to 4 or 3 only, reconsider step (3).
5) Template spacing: Template spacing describes at which grid points between the prior boundaries tem-
plates are (pre-)computed. If the spacing is too large, the templates vary too rapidly and the detection
significance will decrease due to template mismatch. If the spacing is too small, the template bank will
be slow. Find sensible template spacings for your two parameters, by plotting how rapidly the templates
change as you vary the parameters.
Outcome of the exercise: you have created a template bank for gravitational waves. In the next
exercise, you can apply it to synthetic data.
Exercise 3: Filtering data streams for gravitational waves . . . . . . . . . . . . . . . .
The file ‘AllWithNoise.dat’ may or may not contain synthetic gravitational wave signals. These file sample
the time τ regularly (first column), but the initial time has been subtracted. This means the first column
is a time-window, where the original human-time starting point is irrelevant for this exercise. The second,
third and fourth columns store the strain h(τ ). The collapse time tc from Exercise 1 and 2 may take place
at any τ , so you will need to shift your signals as a function of tc .
1. Program up the matched-filter equations and sift through the three signals.
2. Plot the filter output as a function of time. A large spike in the filter output indicates a correlation
with the signal.
3. Find out how many gravitational waves are hidden in the three data streams. What are the parameters
(mass, collapse time, amplitude) of these gravitational waves? Give a best-fit and handwavy error
bars. (The full error bars would be determined in the follow-up analysis).
If you wish to restore the original amplitude of the signal, then the noise here added was uncorrelated
Gaussian noise of standard deviation σ = 0.2.
2
After detection, the in-depth analysis then uses the original physical parameters. -->

This small project was part of the course "Astrostastistics" at the Leiden Observatory. The project consisted of implementing a matched filtering algorithm to detect gravitational wave signals in noisy data. The data used in this project were synthetic, and the templates used the approximations described by the VIRGO and LIGO collaborations {% cite 2017AnP...52900209A --file external %}. 

The equation of the gravitational wave signal from a binary merger was given by
$$ h(t) = \frac{4A\eta M}{D} \left( \pi M f(t) \right)^{2/3} \cos\left[ \phi(t) + \phi_c \right], $$
where $A$ is a geometric prefactor (averaged over all angles making $A = 2/5$), $\eta = \frac{m_1 m_2}{M^2}$ is the reduced mass, $D$ is the luminosity distance, $M = m_1 + m_2$ is the total mass, $f(t)$ is the time-dependent frequency of the wave, $\phi(t)$ is the phase of the wave, and $\phi_c$ is a constant phase. The frequency of the wave increases with time, a phenomenon known as "chirping". The chirp mass $M_c$ is defined as $M_c = \frac{(m_1 m_2)^{3/5}}{(m_1 + m_2)^{1/5}}$, and the chirpline is given by
$$ f_{\text{GW}}(t) = B x^{-5/8} (t_c - t)^{-3/8}, $$
where $B = 16.6 \, \text{s}^{-5/8}$, $x$ is the chirp mass in solar masses, and $t_c$ is the moment of merger. The phase of the wave is given by
$$ \phi(t) = 2\pi B x^{-5/8} (t_c - t)^{5/8}. $$
The signal shape is then given by
$$ h(t) = \frac{4A\eta M \left( \pi M \right)^{2/3}}{D} \left( 16.6 x^{-\frac{5}{8}} (t_c - t)^{-\frac{3}{8}} \right)^{2/3} \cos\left[ -39.11 x^{-\frac{5}{8}} (t_c - t)^{\frac{5}{8}} + \phi_c \right]. $$

This equation has many parameters, some of which are degenerate. To reduce the dimensionality of the template bank, we replaced degenerate parameters with effective parameters. We can reduce the dimensionality of the template bank by considering the scale and shift symmetries of the parameters. Our model can be reduced to 
$$h(t)\sim (t_c-t)^{-\frac{1}{4}}cos(-39.11x^{-\frac{5}{8}}(t_c-t)^{\frac{5}{8}}+\phi_c)$$
where $t_c$, $x$, and $\phi_c$ are the only real signal parameters. In practice, when we employ matched filtering, we will shift the signal in time to match the data by varying $t_c$, so we can argue that only $x$ and $\phi_c$ are the real signal parameters. The amplitude of the signal does not determine which signal is detected, but only how significantly it is detected in relation to the background noise, that is why the above equation has no amplitude parameter.

First we test the matched filtering algorithm on our own synthetic data. We create a signal, using the above equation, and add Gaussian noise to it. We then filter the data and look for a spike in the filter output, which indicates a correlation with the signal. The results of the detection are shown in the figures below.

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
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/time_merger_1.png" title="Time to merger for data stream 1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/contourf_1.png" title="Contour plot of data stream 1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/wave_1.png" title="Detected wave in data stream 1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Results of the matched filtering algorithm on data stream 1. From left to right: raw data stream, detection of the time of merger, contour plot of the filter output as a function of the chirp mass and the phase, and the detected wave in the data stream.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/raw_2.png" title="Raw data stream 2" class="img-fluid rounded z-depth-1" %}
    </div>
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/time_merger_2.png" title="Time to merger for data stream 2" class="img-fluid rounded z-depth-1" %}
    </div>
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/contourf_2.png" title="Contour plot of data stream 2" class="img-fluid rounded z-depth-1" %}
    </div>
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/wave_2.png" title="Detected wave in data stream 2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    As above, but for data stream 2.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/raw_3.png" title="Raw data stream 3" class="img-fluid rounded z-depth-1" %}
    </div>
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/time_merger_3.png" title="Time to merger for data stream 3" class="img-fluid rounded z-depth-1" %}
    </div>
    <div>
        {% include figure.liquid loading="eager" path="assets/img/courses/astronomical/contourf_3.png" title="Contour plot of data stream 3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    As above, but for data stream 3. This time, the detected wave is not shown, as no gravitational wave signal was detected in this data stream.
</div>

The matched filtering algorithm was able to detect the gravitational wave signals in two of the three data streams. The detected waves are shown in the figures above. The algorithm was able to recover the parameters of the signals, such as the chirp mass and the phase. The results of the detection are consistent with the parameters used to create the signals. The algorithm was not able to detect a gravitational wave signal in the third data stream, which did not contain a signal. The final results are summarized in the table below:

| Data Stream | Time of Merger | Chirp Mass | Phase | Detected |
|-------------|----------------|------------|-------|----------|
| 1           | 299.0          | 90.0       | 6.2   | Yes      |
| 2           | 1000.0         | 31.0       | 3.2   | Yes      |
| 3           | -              | -          | -     | No       |


## Stellar Evolution



## Exoplanets



## Interstellar Medium



## Numerical Analysis



## References

{% bibliography --cited --file external %}
