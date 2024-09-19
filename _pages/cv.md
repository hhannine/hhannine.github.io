---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* Ph.D in Theoretical Particle Physics, University of Jyväskylä, 2021
* M.S. in Theoretical Physics, University of Jyväskylä, 2017
* B.S. in Physics, University of Jyväskylä, 2014

Work experience
======
* Summer 2015: Summer intern
  * CERN
  * Duties includes: Testing of machine learning in particle collision simulations.
  * Supervisor: Dr. Sami Räsänen

  
Skills
======
* Quantum Field Theory
  * Color Glass Condensate formalism calculations on the light-cone
  * Perturbative QCD
* Programming
  * C & C++
  * Python
  * Bash / Shell-script
* LaTeX

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
Talks
======
  <ul>{% for post in site.talks reversed %}
    {% include archive-single-talk-cv.html  %}
  {% endfor %}</ul>
  
Teaching
======
  <ul>{% for post in site.teaching reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
<!-- Service and leadership
======
* Currently signed in to 43 different slack teams -->
