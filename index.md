---
layout: home
title: 🏠 Home
nav_exclude: false
nav_order: 1
# trigger rebuild
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

[Jump to the current week](#{{ site.modules.first.title | slugify }}){: .btn data-current-week-link="" }
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
  if (!jumpLink) return;

  const modules = Array.from(document.querySelectorAll('.module'));
  if (!modules.length) return;

  const today = new Date();
  today.setHours(0, 0, 0, 0);

  let target = null;

  // Find the current or most recent week using data-week-start/end attributes
  for (let i = modules.length - 1; i >= 0; i--) {
    const moduleEl = modules[i];
    const weekStart = moduleEl.getAttribute('data-week-start');
    if (weekStart) {
      const startDate = new Date(weekStart + 'T00:00:00');
      if (today >= startDate) {
        target = moduleEl.querySelector('.module-header');
        break;
      }
    }
  }

  // Default to first week if nothing found
  if (!target) {
    target = modules[0].querySelector('.module-header');
  }

  if (target && target.id) {
    jumpLink.setAttribute('href', '#' + target.id);
    // Auto-scroll to current week on page load (centered)
    target.scrollIntoView({ behavior: 'smooth', block: 'center' });
  }

  // Handle click to scroll
  jumpLink.addEventListener('click', function(e) {
    e.preventDefault();
    if (target && target.id) {
      window.location.hash = target.id;
      target.scrollIntoView({ behavior: 'smooth', block: 'center' });
    }
  });
})();
</script>