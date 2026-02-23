---
title: Certifications
layout: default
permalink: /certifications/
---

<div class="col-lg-12">
<div class="row">

  <!-- LEFT PROFILE PANEL -->
  <div class="col-lg-4">
    <div class="card" id="profile-card">
      <a href="/">
        <img src="{{site.baseurl}}/assets/img/{{ site.author_logo }}" class="profile-img" />
      </a>
      <h1 class="profile-name">{{ site.title }}</h1>
      <p class="profile-bio">{{ site.subtitle }}</p>
      {% if site.github_username %} {%- include github_follow_button.html -%} {% endif %}

      <p class="profile-links">
        {% if site.github_username %}
        <a class="social-link" href="http://github.com/{{ site.github_username }}"><i class="fab fa-github"></i></a>
        {% endif %}
        {% if site.linkedin_username %}
        <a class="social-link" href="http://linkedin.com/in/{{ site.linkedin_username }}"><i class="fab fa-linkedin-in"></i></a>
        {% endif %}
      </p>

      {% if site.author_location %}
      <h6><i class="fas fa-map-marker-alt"></i> {{ site.author_location }}</h6>
      {% endif %}
      {% if site.author_email %}
      <h6><i class="fas fa-envelope"></i> {{ site.author_email }}</h6>
      {% endif %}
    </div>

    <div class="card">
      <h1>Skills</h1>
      {%- include author_skills.html -%}
    </div>
  </div>

  <!-- RIGHT CONTENT -->
  <div class="col-lg-8">

    <!-- SUMMARY TABLE -->
    <div class="card mb-3">
      <div class="card-body">
        <table class="table text-center mb-0">
          <thead>
            <tr>
              <th>Professional</th>
              <th>Certifications</th>
              <th>Badges</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>{{ site.author_professional_certifications | size }}</td>
              <td>{{ site.author_certifications | size }}</td>
              <td>{{ site.author_badges | size }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <!-- PROFESSIONAL CERTIFICATIONS -->
    <div class="card mb-3">
      <h1 class="card-title">Professional Certifications</h1>
      <br />

      {% for cert in site.author_professional_certifications %}
      {% if cert.visibility == true %}
      <div class="row align-items-center" style="margin-bottom:20px;padding-bottom:20px;border-bottom:1px solid #e0e0e0;">

        <div class="col-md-2 col-3">
          <img src="{{site.baseurl}}/assets/images/{{ cert.preview_image }}" 
               class="img-fluid rounded"
               style="width:110px;height:110px;object-fit:contain;" />
        </div>

        <div class="col-md-10 col-9">
          <h4 class="experience-title">{{ cert.cert_name }}</h4>
          <h6 class="experience-info">{{ cert.cert_issuer }}</h6>
          <p class="experience-desc">Certified: {{ cert.cert_date }} | Expires: {{ cert.cert_expiry }}</p>
          {% if cert.cert_url %}
          <p><a href="{{cert.cert_url}}" target="_blank">View Credential</a></p>
          {% endif %}
        </div>

      </div>
      {% endif %}
      {% endfor %}
    </div>

    <!-- CERTIFICATIONS -->
    <div class="card mb-3">
      <h1 class="card-title">Certifications</h1>
      <br />

      {% for cert in site.author_certifications %}
      {% if cert.visibility == true %}
      <div class="row align-items-center" style="margin-bottom:20px;padding-bottom:20px;border-bottom:1px solid #e0e0e0;">

        <div class="col-md-2 col-3">
          <img src="{{site.baseurl}}/assets/images/{{ cert.preview_image }}" 
               class="img-fluid rounded"
               style="width:90px;height:90px;object-fit:contain;" />
        </div>

        <div class="col-md-10 col-9">
          <h4 class="experience-title">{{ cert.cert_name }}</h4>
          <h6 class="experience-info">{{ cert.cert_issuer }}</h6>
          <p class="experience-desc">Certified: {{ cert.cert_date }} | Expires: {{ cert.cert_expiry }}</p>
          {% if cert.cert_url %}
          <p><a href="{{cert.cert_url}}" target="_blank">View Credential</a></p>
          {% endif %}
        </div>

      </div>
      {% endif %}
      {% endfor %}
    </div>

    <!-- BADGES -->
    <div class="card mb-3">
      <h1 class="card-title">Badges</h1>
      <br />

      {% for badge in site.author_badges %}
      {% if badge.visibility == true %}
      <div class="row align-items-center" style="margin-bottom:20px;padding-bottom:20px;border-bottom:1px solid #e0e0e0;">

        <div class="col-md-2 col-3">
          <img src="{{site.baseurl}}/assets/images/{{ badge.preview_image }}" 
               class="img-fluid rounded"
               style="width:90px;height:90px;object-fit:contain;" />
        </div>

        <div class="col-md-10 col-9">
          <h4 class="experience-title">{{ badge.badge_name }}</h4>
          <h6 class="experience-info">{{ badge.badge_issuer }}</h6>
          <p class="experience-desc">Awarded: {{ badge.badge_date }} | Expires: {{ badge.badge_expiry }}</p>
          {% if badge.badge_url %}
          <p><a href="{{badge.badge_url}}" target="_blank">View Badge</a></p>
          {% endif %}
        </div>

      </div>
      {% endif %}
      {% endfor %}
    </div>

  </div>
</div>
</div>