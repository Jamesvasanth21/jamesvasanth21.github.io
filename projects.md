---
title: Projects
layout: default
permalink: /projects/
---

<div class="card">
  <h1 class="card-title">
    Projects ({{ site.data.projects.projects | size }})
  </h1>
  

  <!-- Main Tags -->
  <div class="tags">
    {% assign main_tags = site.data.projects.projects | map: "tags" | map: "main" | uniq %}
    {% for tag in main_tags %}
      <button onclick="filterMain('{{ tag }}')">{{ tag }}</button>
    {% endfor %}
  </div>

  <!-- Sub Tags -->
  <div id="sub-tags"></div>
  <hr class="section-divider" />

  <!-- Projects List -->
  <div id="project-list">
    {% for project in site.data.projects.projects %}
      <div class="project-item" id="{{ project.id }}"
           data-main="{{ project.tags.main }}"
           data-sub="{{ project.tags.sub | join: ',' }}">

        <h3>
          {{ project.title }}
        </h3>

        <p>{{ project.description }}</p>

        <p><strong>Tech:</strong> {{ project.tech | join: ', ' }}</p>

        <a href="{{ project.github_url }}" target="_blank">GitHub</a>
      </div>
      <hr class="section-divider" />
    {% endfor %}
  </div>
</div>

<script>
function filterMain(tag) {
  const items = document.querySelectorAll(".project-item");
  const subTags = new Set();

  items.forEach(item => {
    if (item.dataset.main === tag) {
      item.style.display = "block";
      item.dataset.sub.split(',').forEach(t => subTags.add(t));
    } else {
      item.style.display = "none";
    }
  });

  // Render sub-tags
  const subTagDiv = document.getElementById("sub-tags");
  subTagDiv.innerHTML = "";

  subTags.forEach(sub => {
    const btn = document.createElement("button");
    btn.innerText = sub;
    btn.onclick = () => filterSub(sub);
    subTagDiv.appendChild(btn);
  });
}

function filterSub(tag) {
  const items = document.querySelectorAll(".project-item");

  items.forEach(item => {
    if (item.dataset.sub.includes(tag)) {
      item.style.display = "block";
    } else {
      item.style.display = "none";
    }
  });
}
</script>