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
  <hr id="top-divider" class="section-divider" />

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
      <hr class="section-divider item-divider" />
    {% endfor %}
  </div>
</div>

<style>
/* Tag buttons */
.tags,
#sub-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 10px;
}

.tags button,
#sub-tags button {
  display: inline-block;
  padding: 6px 14px;
  font-size: 13px;
  font-weight: 500;
  line-height: 1;
  border: 1.5px solid #aaa;
  border-radius: 20px;
  background: #f5f5f5;
  color: #333;
  cursor: pointer;
  transition: background 0.15s, border-color 0.15s, color 0.15s;
  white-space: nowrap;
}

.tags button:hover,
#sub-tags button:hover {
  background: #333;
  border-color: #333;
  color: #fff;
}

.tags button.active,
#sub-tags button.active {
  background: #222;
  border-color: #222;
  color: #fff;
}

#sub-tags {
  margin-top: 8px;
}
</style>

<script>
(function () {

  var currentMain = null;

  function syncDividers() {
    var items = document.querySelectorAll(".project-item");
    var dividers = document.querySelectorAll(".item-divider");

    /* Hide all dividers first */
    dividers.forEach(function (hr) { hr.style.display = "none"; });

    /* Find visible items and show a divider after each except the last */
    var visibleItems = [];
    items.forEach(function (item) {
      if (item.style.display !== "none") visibleItems.push(item);
    });

    visibleItems.forEach(function (item, idx) {
      /* Each .project-item is immediately followed by an .item-divider */
      var next = item.nextElementSibling;
      if (next && next.classList.contains("item-divider")) {
        /* Show divider after every visible item except the last */
        next.style.display = idx < visibleItems.length - 1 ? "" : "none";
      }
    });

    /* Hide the top divider when there are no sub-tags and nothing filtered */
    var topDivider = document.getElementById("top-divider");
    if (topDivider) {
      topDivider.style.display = visibleItems.length === 0 ? "none" : "";
    }
  }

  function setActiveMainButton(tag) {
    document.querySelectorAll(".tags button").forEach(function (btn) {
      btn.classList.remove("active");
      if (
        (tag === null && btn.getAttribute("onclick") === "resetFilter()") ||
        btn.getAttribute("onclick") === "filterMain('" + tag + "')"
      ) {
        btn.classList.add("active");
      }
    });
  }

  window.resetFilter = function () {
    currentMain = null;
    document.querySelectorAll(".project-item").forEach(function (item) {
      item.style.display = "block";
    });
    document.getElementById("sub-tags").innerHTML = "";
    setActiveMainButton(null);
    syncDividers();
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

    setActiveMainButton(tag);
    renderSubTags(subTags);
    syncDividers();
  };

  function renderSubTags(subTags) {
    var container = document.getElementById("sub-tags");
    container.innerHTML = "";

    subTags.forEach(function (sub) {
      var btn = document.createElement("button");
      btn.textContent = sub;
      btn.onclick = function () {
        document.querySelectorAll("#sub-tags button").forEach(function (b) {
          b.classList.remove("active");
        });
        btn.classList.add("active");
        filterSub(sub);
      };
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
    syncDividers();
  };

  /* Run once on load so dividers are correct from the start */
  document.addEventListener("DOMContentLoaded", function () {
    syncDividers();
    /* Mark "All" as active by default */
    var allBtn = document.querySelector(".tags button[onclick='resetFilter()']");
    if (allBtn) allBtn.classList.add("active");
  });

})();
</script>