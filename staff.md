---
layout: page
title: 👩‍🏫 Staff
description: A listing of all the course staff members.
nav_order: 6
---

# 👩‍🏫 Staff

## Instructor

<div class="staffer">
  <img class="staffer-image" src="/assets/staff-images/tauhidur-rahman.jpg" alt="Tauhidur Rahman">

  <div>
    <h3 class="staffer-name">
      <a href="https://www.tauhidurrahman.com/">Tauhidur Rahman</a>
    </h3>

    <!-- Contact Information -->
    <p>
      <a href="mailto:trahman@ucsd.edu">trahman@ucsd.edu</a><br>
    </p>

    <!-- Instructor Paragraph -->
    <p>
    Tauhidur Rahman is an Assistant Professor in the Halıcıoğlu Data Science Institute at the University of California San Diego where he directs the <a href="https://mosaic-laboratory.github.io/">Mobile Sensing and Ubiquitous Computing Laboratory (MOSAIC Lab)</a>. His research focuses on developing innovative ubiquitous and mobile health sensing technologies that capture low-level physiological and environmental signals, translating them into meaningful biological and behavioral insights.
    </p>
  </div>
</div>


## Staff

{% assign tas = site.staffers | where: 'role', 'TA' %}
{% for staffer in tas %}
{{ staffer }}
{% endfor %}

{% assign staff = site.staffers | where: 'role', 'Tutor' %}
<div class="role">
  {% for staffer in staff %}
  {{ staffer }}
  {% endfor %}
</div>
