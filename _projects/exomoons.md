---
layout: page
title: Finding the best exoplanets to search for exomoons by radial velocity
description: Master's thesis research project (1st year)
img: assets/img/saturn.jpg
importance: 2
category: research
related_publications: false
giscus_comments: false
redirect:
pretty_table: true
---

Cover Image by <a href="https://images.nasa.gov/details/PIA14922">NASA</a> showing a natural color view of Titan and Saturn from NASA Cassini spacecraft.
<br>
<br>

Please find the thesis [here](/assets/pdf/exomoons.pdf). The code of the project is not available yet, but will be soon. Stay tuned!

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/eso.jpg" title="eso" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Beta Pictoris as seen in infrared light - annotated. Image taken from [ESO](https://www.eso.org/public/images/eso0842b/)
</div>

## Overview
This research delves into the detection of exomoons through radial velocity variations, focusing on the exoplanet β Pictoris b. Exomoons are natural satellites orbiting planets outside our solar system and may provide critical insights into planetary system formation and habitability. The study combines theoretical modeling, simulation, and real observational data to refine detection techniques and explore new frontiers in exoplanetary science.

## Introduction
The search for exoplanets has revolutionized our understanding of the universe, uncovering thousands of planets beyond our solar system. Techniques like radial velocity and transit photometry have been central to these discoveries. However, detecting exomoons remains a formidable challenge due to their smaller size and weaker signals. This chapter sets the stage by discussing the importance of exomoons and introducing β Pictoris b as a prime candidate for detailed study due to its mass, orbit, and edge-on orientation.

<!-- ![Exoplanet Detection Techniques](path-to-techniques-image.jpg)  
*Figure 2: Overview of exoplanet detection techniques.* -->
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/exoplanets.jpg" title="exoplanets" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/Io_betaPicb.jpg" title="Io_betaPicb" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: Overview of exoplanet detection techniques. Right: The radial velocities of Jupiter (red) and β Pic b (green) that are caused by Io and a potential Earth-mass exomoon period of 10 days respectively as a function of time.
</div>

## Radial Velocity Analysis
We can now examine how moons induce radial velocity variations in their host planets. Using simulations, the study explores the impact of moon mass and orbital period on detectable signals. Comparisons between Jupiter-Io and hypothetical exomoons around β Pictoris b reveal that larger, closer moons produce stronger signals. These findings guide the design of detection strategies for exomoons.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/contour.png" title="contour" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A contour plot showing the peak radial velocity for different masses and orbital periods of a potential exomoon around β Pic b. Note that the x-axis showing the orbital period is in logarithmic scale. The dotted line is representing the isoline for 500 m/s. Blue crosses are the modelled sensitivities for 25 observations with CRIRES+ (more details on that in the next chapters). White and yellow spots show already proposed exomoon candidates for Kepler 1708 and Kepler1625 respectively.
</div>

## Cross-Correlation of Spectra
Radial velocity measurements rely on detecting Doppler shifts in spectral lines. This chapter details the process of simulating β Pictoris b's spectrum, applying Doppler shifts, and extracting velocities using cross-correlation techniques. The study validates these methods with high-resolution spectra, showcasing their potential for detecting subtle exomoon-induced shifts.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/spectrum_1.jpg" title="spectrum_1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/spectrum_2.jpg" title="spectrum_2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    High-resolution simulated spectra of β Pic b used for the cross-correlation analysis. With blue points showing the original spectrum, green points showing the rebinned spectrum, and the red line showing the convolved spectrum. Left: Simulated spectrum provided by Dr. Tomas Stolker. Right: Simulated spectrum provided by Dr. Paul Mollière (based on the best-fit model of GRAVITY Collaboration).
</div>


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/doppler_1.jpg" title="doppler_1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/doppler_2.jpg" title="doppler_2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Each image has two panels showing. On the left, the convolved spectrum for β Pic b in green and the shifted spectrum due to the Doppler effect with v = 3000km/s with red. On the right the result of the cross-correlation of the two spectra on the left. The vertical line represents the v = 0. On the small panel, there is the peak of the cross-correlation that is clearly at a non-zero velocity, close to 0.3 × 107 m/s. Left: Simulated spectrum provided by Dr. Tomas Stolker. Right: Simulated spectrum provided by Dr. Paul Mollière (based on the best-fit model of GRAVITY Collaboration).
</div>

## Simulating Exomoon Detection
Through Bayesian modeling, this chapter simulates the detection of exomoons by creating synthetic radial velocity data with added observational noise. Results demonstrate that moons with higher masses and shorter orbital periods are easier to detect. For β Pictoris b, exomoons larger than 20 Earth masses with a 10-day period or shorter are within detectable thresholds, depending on noise levels.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/rv-t_10_80_500.jpg" title="rv-t_10_80_500" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/corner_10_80_500.jpg" title="corner_10_80_500" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The radial velocity data generated from the exoplanet module for a moon of 80 Earth masses and a period of 10 days with added noise of 500m/s. The blue line represents the posterior, after fitting the Bayesian model, with the 16th and 84th percentile.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/rv-t_10_60_250.jpg" title="rv-t_10_60_250" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/corner_10_60_250.jpg" title="corner_10_60_250" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The radial velocity data generated from the exoplanet module for a moon of 60 Earth masses and a period of 10 days with added noise of 250m/s. The blue line represents the posterior, after fitting the Bayesian model, with the 16th and 84th percentile.
</div>
<!-- 
Period
Noise10 days20 days
250 m/s> 20M⊕> 60M⊕
500 m/s> 40M⊕> 130M⊕
-->

| Orbital Period (days) | Observational Noise (m/s) | Minimum Detectable Moon Mass (Earth Masses) |
|-----------------------|---------------------------|---------------------------------------------|
| 10                    | 250                       | 20                                          |
| 10                    | 500                       | 40                                          |
| 20                    | 250                       | 60                                         |
| 20                    | 500                       | 130                                          |

<p></p>

## Real Data and Surface Spots
This chapter analyzes real radial velocity data from β Pictoris b collected with the CRIRES+ spectrograph. Observed fluctuations are hypothesized to result from atmospheric phenomena, such as surface spots. Simulations show that patterns of 21–33 spots could plausibly explain the observed frequencies, though further analysis is needed to confirm.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/rv_full.jpg" title="rv_full" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The radial velocity data for β Pictoris b that were provided by Dr. Rico Landman. The two panels contain the two separate observational runs on November 11 (left) and November 13 (right) of 2022.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/spots_1.png" title="spots_1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/spots_2.png" title="spots_2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Spot creation using the `starry` package. For this figure, we created 6 spots with 0 latitude and different longitudes. On the left, we see the equirectangular view of the map while on the right panel we find the spherical view of the planet with the spots.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/lombscargle_both.jpg" title="lombscargle_both" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The Fourier Transformation of the radial velocity time-series shown before. On the left panel, we have the first observational run, while the second one is on the right panel. With the red vertical lines showing the main peak frequencies.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/period_fit.jpg" title="period_fit" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/research/exomoon/ampl_size.jpg" title="ampl_size" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: The period of the radial velocity signal as a function of the number of spots on the atmosphere of β Pictoris b. The red line represents the fitted function. Right: Radial velocity amplitudes as a function of the size of the spots. The colours indicate the number of spots that were used in the simulation.
</div>

| | Mean Period (days) | Number of Spots |
|-----------------------|-------------------|-----------------|
| Run 1 | 0.271 +/- 0.025 | 27-33 |
| Run 2 | 0.345 +/- 0.050 | 21-27 |

<p></p>


## Conclusions and Future Work
Detecting exomoons through radial velocity is a challenging but promising endeavor. This study demonstrates the potential for detection under current and future observational capabilities, especially for systems like β Pictoris b. Future research will aim to refine techniques, extend observational datasets, and explore other exoplanetary systems.

---

## Acknowledgments
This work was conducted under the supervision of Prof. Matthew Kenworthy at Leiden Observatory. Special thanks to Dr. Rico Landmann, Dr. Tomas Stolker, and Dr. Paul Mollière for their invaluable contributions.