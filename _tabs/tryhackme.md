---
title: TryHackMe
icon: fas fa-shield-halved
order: 5
layout: page
---

{% assign courses = site.posts | where: 'th_parent', 'root' | sort: 'th_order' %}

<div id="page-tryhackme">
  <p class="text-muted mb-4">
    {{ courses | size }} learning paths, {{ site.posts | where_exp: 'p', 'p.th_id' | size }} posts in total.
  </p>

  {% for course in courses %}
    {% assign modules = site.posts | where: 'th_parent', course.th_id | sort: 'th_order' %}

    <div class="card categories mb-4">
      <div class="card-header d-flex justify-content-between hide-border-bottom">
        <span class="ms-2">
          <i class="far fa-folder{% if modules.size > 0 %}-open{% endif %} fa-fw"></i>
          <a href="{{ course.url | relative_url }}" class="mx-2">{{ course.title }}</a>
          <span class="text-muted small font-weight-light">
            {% if modules.size > 0 %}
              {{ modules.size }} {% if modules.size > 1 %}modules{% else %}module{% endif %},
            {% endif %}
            {{ course.th_size }} {% if course.th_size == 1 %}post{% else %}posts{% endif %}
          </span>
        </span>

        {% if modules.size > 0 %}
          <a
            href="#tryhackme-course-{{ forloop.index }}"
            data-bs-toggle="collapse"
            aria-expanded="true"
            aria-label="course-{{ forloop.index }}-trigger"
            class="category-trigger hide-border-bottom"
          >
            <i class="fas fa-fw fa-angle-down"></i>
          </a>
        {% else %}
          <span class="category-trigger hide-border-bottom disabled">
            <i class="fas fa-fw fa-angle-right"></i>
          </span>
        {% endif %}
      </div>

      {% if modules.size > 0 %}
        <div id="tryhackme-course-{{ forloop.index }}" class="collapse show">
          <ul class="list-group">
            {% for module in modules %}
              <li class="list-group-item d-flex justify-content-between align-items-center">
                <span>
                  <i class="far fa-folder fa-fw"></i>
                  <a href="{{ module.url | relative_url }}" class="mx-2">{{ module.title }}</a>
                </span>
                {% if module.th_size > 0 %}
                  <span class="text-muted small font-weight-light text-nowrap">
                    {{ module.th_size }} {% if module.th_size == 1 %}post{% else %}posts{% endif %}
                  </span>
                {% endif %}
              </li>
            {% endfor %}
          </ul>
        </div>
      {% endif %}
    </div>
  {% endfor %}
</div>
