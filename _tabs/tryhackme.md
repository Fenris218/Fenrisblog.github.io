---
title: TryHackMe
icon: fas fa-shield-halved
order: 5
---

{% assign courses = site.posts | where: 'th_parent', 'root' | sort: 'th_order' %}
{% assign th_modules = site.posts | where: 'th_kind', 'module' %}
{% assign th_notes = site.posts | where: 'th_kind', 'note' %}

<p class="text-muted">
  Personal notes from the TryHackMe SOC roadmap, reorganised into a browsable tree:
  {{ courses | size }} learning paths, {{ th_modules | size }} modules and
  {{ th_notes | size }} individual notes.
</p>

{% for course in courses %}
  {% assign modules = site.posts | where: 'th_parent', course.th_id | sort: 'th_order' %}
  <div class="card mb-4">
    <div class="card-header d-flex justify-content-between align-items-center">
      <a class="fw-semibold text-decoration-none" href="{{ course.url | relative_url }}">
        {{ course.title }}
      </a>
      <span class="badge bg-secondary">{{ course.th_size }} notes</span>
    </div>
    <div class="card-body">
      <div class="row row-cols-1 row-cols-md-2 g-2">
        {% for module in modules %}
          <div class="col">
            <a
              href="{{ module.url | relative_url }}"
              class="d-flex justify-content-between align-items-center border rounded px-3 py-2 h-100 text-decoration-none"
            >
              <span class="text-body">{{ module.title }}</span>
              {% if module.th_size > 0 %}
                <span class="badge bg-light text-dark border ms-2">{{ module.th_size }}</span>
              {% endif %}
            </a>
          </div>
        {% endfor %}
      </div>
    </div>
  </div>
{% endfor %}
