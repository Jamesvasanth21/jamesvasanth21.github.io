---
title: Projects
layout: default
permalink: /projects/
---

<div class="card">

  <!-- HEADER -->
  <div class="projects-header">
    <h1 class="card-title">
      Projects ({{ site.data.projects.projects | size }})
    </h1>

    <p class="projects-subtitle">
      AI systems, cloud engineering, platform development projects.
    </p>
  </div>

  <!-- CATEGORY FILTERS -->
  <div class="tags category-tags">

    <button class="active" onclick="resetFilter()">
      All
    </button>

    {% for category in site.data.projects.categories %}
      <button onclick="filterCategory('{{ category | escape }}')">
        {{ category }}
      </button>
    {% endfor %}

  </div>

  <!-- DYNAMIC TAG FILTERS -->
  <div id="sub-tags"></div>

  <hr class="section-divider" />

  <!-- PROJECTS -->
  <div id="project-list">

    {% for project in site.data.projects.projects %}

      <div
        class="project-item"
        id="{{ project.id }}"
        data-category="{{ project.category }}"
        data-tags="{{ project.tags | join: ',' }}"
      >

        <!-- CATEGORY LABEL -->
        <div class="project-category-label">
          {{ project.category }}
        </div>

        <!-- TITLE -->
        <h3 class="project-title">
          {{ project.title }}
        </h3>

        <!-- DESCRIPTION -->
        <p class="project-description">
          {{ project.description }}
        </p>

        <!-- TECH -->
        <div class="tech-stack">

          {% for tech in project.tech %}
            <span class="tech-badge">
              {{ tech }}
            </span>
          {% endfor %}

        </div>

        <!-- TAGS -->
        <div class="project-tags">

          {% for tag in project.tags %}
            <span class="project-tag">
              {{ tag }}
            </span>
          {% endfor %}

        </div>

        <!-- ACTIONS -->
        <div class="project-actions">

          {% if project.github_url %}
          <a
            class="project-btn"
            href="{{ project.github_url }}"
            target="_blank"
          >
            GitHub
          </a>
          {% endif %}

          {% if project.live_url %}
          <a
            class="project-btn live-btn"
            href="{{ project.live_url }}"
            target="_blank"
          >
            Live Site
          </a>
          {% endif %}

          {% if project.kaggle_url %}
          <a
              class="btn btn-sm btn-outline-dark"
              href="{{ project.kaggle_url }}"
              target="_blank"
          >
              {{ project.platform }}
          </a>
          {% endif %}

        </div>

      </div>

      <hr class="section-divider item-divider" />

    {% endfor %}

  </div>
</div>

<style>

/* =========================
   HEADER
========================= */

.projects-header {
  margin-bottom: 25px;
}

.projects-subtitle {
  color: #666;
  margin-top: 6px;
  font-size: 15px;
}

/* =========================
   FILTER BUTTONS
========================= */

.tags,
#sub-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 14px;
}

.tags button,
#sub-tags button {

  border: 1px solid #ccc;
  background: #f8f8f8;

  padding: 7px 14px;

  border-radius: 20px;

  cursor: pointer;

  font-size: 13px;
  font-weight: 500;

  transition: all 0.2s ease;
}

.tags button:hover,
#sub-tags button:hover {
  background: #222;
  color: white;
  border-color: #222;
}

.tags button.active,
#sub-tags button.active {
  background: #111;
  color: white;
  border-color: #111;
}

/* =========================
   PROJECT CARD
========================= */

.project-item {

  padding-top: 10px;
  padding-bottom: 10px;
}

.project-category-label {

  display: inline-block;

  font-size: 12px;
  font-weight: 600;

  color: #666;

  margin-bottom: 8px;

  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.project-title {

  margin-bottom: 12px;
}

.project-description {

  color: rgba(255,255,255,0.78);
  
  line-height: 1.8;
  font-size: 15px;
  
  margin-bottom: 14px;
}

/* =========================
   TECH STACK
========================= */

.tech-stack,
.project-tags {

  display: flex;
  flex-wrap: wrap;

  gap: 8px;

  margin-top: 12px;
}

.tech-badge,
.project-tag {

  display: inline-block;

  padding: 6px 10px;

  border-radius: 14px;

  font-size: 12px;
}

.tech-badge {

  background: #f1f3f5;
  color: #333;
}

.project-tag {

  background: #ececec;
  color: #555;
}

/* =========================
   ACTION BUTTONS
========================= */

.project-actions {

  margin-top: 18px;

  display: flex;
  gap: 10px;
}

.project-btn {

  display: inline-block;

  padding: 8px 14px;

  border-radius: 6px;

  text-decoration: none;

  background: #222;
  color: white;

  font-size: 13px;
  font-weight: 500;

  transition: opacity 0.2s ease;
}

.project-btn:hover {
  opacity: 0.9;
  color: white;
}

.live-btn {
  background: #444;
}

/* =========================
   DIVIDER
========================= */

.item-divider {
  margin-top: 24px;
  margin-bottom: 24px;
}

</style>

<script>

(function () {

  let currentCategory = null;

  /* =========================
     RESET FILTER
  ========================= */

  window.resetFilter = function () {

    currentCategory = null;

    document
      .querySelectorAll(".project-item")
      .forEach(function (item) {
        item.style.display = "block";
      });

    document.getElementById("sub-tags").innerHTML = "";

    setActiveCategoryButton(null);

    syncDividers();
  };

  /* =========================
     FILTER CATEGORY
  ========================= */

  window.filterCategory = function (category) {

    currentCategory = category;

    const tags = new Set();

    document
      .querySelectorAll(".project-item")
      .forEach(function (item) {

        const itemCategory =
          item.getAttribute("data-category");

        if (itemCategory === category) {

          item.style.display = "block";

          const itemTags =
            item.getAttribute("data-tags");

          if (itemTags) {

            itemTags
              .split(",")
              .forEach(function (tag) {

                const clean = tag.trim();

                if (clean) {
                  tags.add(clean);
                }

              });
          }

        } else {

          item.style.display = "none";
        }

      });

    renderSubTags(tags);

    setActiveCategoryButton(category);

    syncDividers();
  };

  /* =========================
     FILTER SUB TAG
  ========================= */

  window.filterTag = function (tag) {

    document
      .querySelectorAll(".project-item")
      .forEach(function (item) {

        const itemCategory =
          item.getAttribute("data-category");

        if (
          currentCategory &&
          itemCategory !== currentCategory
        ) {
          item.style.display = "none";
          return;
        }

        const itemTags =
          (item.getAttribute("data-tags") || "")
          .split(",")
          .map(function (t) {
            return t.trim();
          });

        item.style.display =
          itemTags.indexOf(tag) !== -1
            ? "block"
            : "none";
      });

    syncDividers();
  };

  /* =========================
     RENDER SUB TAGS
  ========================= */

  function renderSubTags(tags) {

    const container =
      document.getElementById("sub-tags");

    container.innerHTML = "";

    tags.forEach(function (tag) {

      const btn =
        document.createElement("button");

      btn.textContent = tag;

      btn.onclick = function () {

        document
          .querySelectorAll("#sub-tags button")
          .forEach(function (b) {
            b.classList.remove("active");
          });

        btn.classList.add("active");

        filterTag(tag);
      };

      container.appendChild(btn);
    });
  }

  /* =========================
     ACTIVE CATEGORY BUTTON
  ========================= */

  function setActiveCategoryButton(category) {

    document
      .querySelectorAll(".category-tags button")
      .forEach(function (btn) {

        btn.classList.remove("active");

        const text =
          btn.textContent.trim();

        if (
          (category === null && text === "All") ||
          text === category
        ) {
          btn.classList.add("active");
        }
      });
  }

  /* =========================
     DIVIDER HANDLING
  ========================= */

  function syncDividers() {

    const items =
      document.querySelectorAll(".project-item");

    const dividers =
      document.querySelectorAll(".item-divider");

    dividers.forEach(function (divider) {
      divider.style.display = "none";
    });

    const visible = [];

    items.forEach(function (item) {

      if (item.style.display !== "none") {
        visible.push(item);
      }
    });

    visible.forEach(function (item, index) {

      const divider =
        item.nextElementSibling;

      if (
        divider &&
        divider.classList.contains("item-divider")
      ) {

        divider.style.display =
          index < visible.length - 1
            ? ""
            : "none";
      }
    });
  }

  /* =========================
     INITIALIZE
  ========================= */

  document.addEventListener(
    "DOMContentLoaded",
    function () {

      syncDividers();
    }
  );

})();

</script>