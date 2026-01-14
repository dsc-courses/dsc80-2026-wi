---
layout: home
title: 🏠 Home
nav_exclude: false
nav_order: 1
---

# {{ site.tagline }}

{: .mb-2 }
{{ site.description }}
{: .fs-6 .fw-300 }

{{ site.staffersnobio }}

[syllabus]: https://dsc80.com/syllabus
[campuswire]: https://campuswire.com/c/GFDCC5DB7
[gradescope]: https://www.gradescope.com/courses/1209672
[github]: https://github.com/dsc-courses/dsc80-2026-fa
[welcome-survey]: https://forms.gle/byE5q4b1iKsBzEwN7

[Jump to the current week](#{{ site.modules.first.title | slugify }}){: .btn data-current-week-link } 
[Podcasts](https://podcast.ucsd.edu/){: .btn }
[Welcome Survey][welcome-survey]{: .btn }


{: .success }
**Welcome to DSC 80! 👋 Make sure to read the [syllabus][syllabus], check that you can access [Gradescope][gradescope] and [Campuswire][campuswire], and fill out the [Welcome Survey][welcome-survey].**

{% for module in site.modules %}
{{ module }}
{% endfor %}


<script>
(function() {
  const jumpLink = document.querySelector('[data-current-week-link]');
  if (!jumpLink) {
    return;
  }

  const modules = Array.from(document.querySelectorAll('.module'));
  if (!modules.length) {
    return;
  }

  const parseDate = (value) => {
    if (!value) {
      return null;
    }
    const parsed = new Date(value + 'T00:00:00');
    if (Number.isNaN(parsed.getTime())) {
      return null;
    }
    return parsed;
  };

  const moduleData = modules
    .map((moduleEl) => {
      const start = parseDate(moduleEl.dataset.weekStart);
      const end = parseDate(moduleEl.dataset.weekEnd);
      const header = moduleEl.querySelector('.module-header');
      if (!start || !end || !header || !header.id) {
        return null;
      }
      return { start, end, header };
    })
    .filter(Boolean);

  if (!moduleData.length) {
    return;
  }

  moduleData.sort((a, b) => a.start - b.start);

  const today = new Date();
  const todayMidnight = new Date(today.getFullYear(), today.getMonth(), today.getDate());
  let target = moduleData.find((module) => (
    todayMidnight >= module.start && todayMidnight <= module.end
  ));

  if (!target) {
    if (todayMidnight < moduleData[0].start) {
      target = moduleData[0];
    } else {
      for (let i = moduleData.length - 1; i >= 0; i -= 1) {
        if (todayMidnight > moduleData[i].end) {
          target = moduleData[i];
          break;
        }
      }
    }
  }

  if (target) {
    jumpLink.setAttribute('href', '#' + target.header.id);
  }
})();
</script>