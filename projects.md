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
    <button onclick="resetFilter()">All</button>
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

        <h3>{{ project.title }}</h3>

        <p>{{ project.description }}</p>

        <p><strong>Tech:</strong> {{ project.tech | join: ', ' }}</p>

        <a class="btn btn-sm btn-outline-dark"
           href="{{ project.github_url }}"
           target="_blank">
          GitHub
        </a>
      </div>
      <hr class="section-divider" />
    {% endfor %}
  </div>
</div>

<script>
(function () {

  var currentMain = null;

  window.resetFilter = function () {
    currentMain = null;
    document.querySelectorAll(".project-item").forEach(function (item) {
      item.style.display = "block";
    });
    document.getElementById("sub-tags").innerHTML = "";
  };

  window.filterMain = function (tag) {
    currentMain = tag;
    var subTags = new Set();

    document.querySelectorAll(".project-item").forEach(function (item) {
      if (item.getAttribute("data-main") === tag) {
        item.style.display = "block";
        var sub = item.getAttribute("data-sub");
        if (sub) {
          sub.split(",").forEach(function (s) {
            var clean = s.trim();
            if (clean) subTags.add(clean);
          });
        }
      } else {
        item.style.display = "none";
      }
    });

    renderSubTags(subTags);
  };

  function renderSubTags(subTags) {
    var container = document.getElementById("sub-tags");
    container.innerHTML = "";

    subTags.forEach(function (sub) {
      var btn = document.createElement("button");
      btn.textContent = sub;
      btn.onclick = function () { filterSub(sub); };
      container.appendChild(btn);
    });
  }

  window.filterSub = function (tag) {
    document.querySelectorAll(".project-item").forEach(function (item) {
      if (item.getAttribute("data-main") !== currentMain) {
        item.style.display = "none";
        return;
      }
      var subs = (item.getAttribute("data-sub") || "")
        .split(",")
        .map(function (s) { return s.trim(); });
      item.style.display = subs.indexOf(tag) !== -1 ? "block" : "none";
    });
  };

})();
</script>