---
title: Certifications
layout: default
permalink: /certifications/
---

<div class="col-lg-12">
<div class="row">
  <div class="col-lg-4">
    <div class="card" id="profile-card">
      <a href="/">
        <img src="{{site.url}}{{site.baseurl}}/assets/img/{{ site.author_logo }}" class="profile-img" />
      </a>
      <h1 class="profile-name">{{ site.title }}</h1>
      <p class="profile-bio">{{ site.subtitle }}</p>
      {% if site.github_username %} {%- include github_follow_button.html -%} {% endif %}

      <p class="profile-links">
        {% if site.twitter_username %}
        <a class="social-link" href="http://twitter.com/{{ site.twitter_username }}">
          <i class="fab fa-twitter"></i>
        </a>
        {% endif %}
        {% if site.facebook_username %}
        <a class="social-link" href="http://facebook.com/{{ site.facebook_username }}">
          <i class="fab fa-facebook-f"></i>
        </a>
        {% endif %}
        {% if site.instagram_username %}
        <a class="social-link" href="http://instagram.com/{{ site.instagram_username }}">
          <i class="fab fa-instagram"></i>
        </a>
        {% endif %}
        {% if site.medium_username %}
        <a class="social-link" href="http://medium.com/@{{ site.medium_username }}">
          <i class="fab fa-medium-m"></i>
        </a>
        {% endif %}
        {% if site.github_username %}
        <a class="social-link" href="http://github.com/{{ site.github_username }}">
          <i class="fab fa-github"></i>
        </a>
        {% endif %}
        {% if site.behance_username %}
        <a class="social-link" href="http://behance.net/{{ site.behance_username }}">
          <i class="fab fa-behance"></i>
        </a>
        {% endif %}
        {% if site.linkedin_username %}
        <a class="social-link" href="http://linkedin.com/in/{{ site.linkedin_username }}">
          <i class="fab fa-linkedin-in"></i>
        </a>
        {% endif %}
        {% if site.telegram_username %}
        <a class="social-link" href="http://t.me/{{ site.telegram_username }}">
          <i class="fab fa-telegram-plane"></i>
        </a>
        {% endif %}
        {% if site.dribbble_username %}
        <a class="social-link" href="https://dribbble.com/{{ site.dribbble_username }}">
          <i class="fab fa-dribbble"></i>
        </a>
        {% endif %}
        {% if site.flickr_username %}
        <a class="social-link" href="https://www.flickr.com/photos/{{ site.flickr_username }}">
          <i class="fab fa-flickr"></i>
        </a>
        {% endif %}
      </p>

      {% if site.author_location %}
      <h6><a href="https://www.google.com/maps/search/?api=1&query={{ site.author_location }}" class="social-link"><i class="fas fa-map-marker-alt"></i> {{ site.author_location }}</a></h6>
      {% endif %}
      {% if site.author_email %}
      <h6><a href="mailto:{{ site.author_email }}"><i class="fas fa-envelope" class="social-link"></i> {{ site.author_email }}</a></h6>
      {% endif %}
      {% if site.author_website_url %}
      <h6><a href="{{ site.author_website_url }}"><i class="fas fa-link" class="social-link"></i> {{ site.author_website_url }}</a></h6>
      {% endif %}
    </div>

    <div class="card">
      <h1>Skills</h1>
      {%- include author_skills.html -%}
    </div>
  </div>

  <div class="col-lg-8">
    <!-- Summary table -->
    <div class="card mb-3">
      <div class="card-body">
        <table class="table text-center mb-0">
          <thead>
            <tr>
              <th>Professional Certifications</th>
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

    <!-- Professional Certifications Section -->
    <div class="card mb-3">
      <h1 class="card-title">Professional Certifications</h1>
      <br />
      {% if site.author_professional_certifications %}
        {% for cert in site.author_professional_certifications %}
          {% if cert.visibility == true %}
          <div class="row" style="margin-bottom: 20px; padding-bottom: 20px; border-bottom: 1px solid #e0e0e0;">
            <div class="col-md-2">
              <div class="preview-container" style="width:100%;display:flex;align-items:center;justify-content:center;min-height:96px;">
                {% if cert.preview_image %}
                  <img src="{{ cert.preview_image }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                {% elsif cert.preview_embed %}
                  {% assign pe = cert.preview_embed | strip %}
                  {% if pe contains '<' %}
                    <div class="embed-wrapper" style="display:flex;align-items:center;justify-content:center;">{{ pe }}</div>
                    {% if pe contains 'credly' %}{% assign has_credly = true %}{% endif %}
                  {% elsif pe contains 'http' %}
                    <img src="{{ pe }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                  {% endif %}
                {% elsif cert.cert_url %}
                  {% assign url_lower = cert.cert_url | downcase %}
                  {% if url_lower contains '.png' or url_lower contains '.jpg' or url_lower contains '.jpeg' or url_lower contains '.svg' or url_lower contains '.gif' %}
                    <img src="{{ cert.cert_url }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                  {% else %}
                    <img src="https://www.google.com/s2/favicons?sz=128&domain_url={{ cert.cert_url | uri_escape }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                  {% endif %}
                {% else %}
                  <img src="{{site.url}}{{site.baseurl}}/assets/img/profile.png" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                {% endif %}
              </div>
            </div>
            <div class="col-md-10">
              <h4 class="experience-title">{{ cert.cert_name }}</h4>
              <h6 class="experience-info">{{ cert.cert_issuer }}</h6>
              <p class="experience-desc">Certified: {{ cert.cert_date}} | Expires: {{ cert.cert_expiry }}</p>
              {% if cert.cert_url %}
              <p><a href="{{cert.cert_url}}" target="_blank">View Credential</a></p>
              {% endif %}
            </div>
          </div>
          {% endif %}
        {% endfor %}
      {% else %}
        <p>No professional certifications to display at this time.</p>
      {% endif %}
    </div>

    <!-- Certifications Section -->
    <div class="card mb-3">
      <h1 class="card-title">Certifications</h1>
      <br />
      {% if site.author_certifications %}
        {% for cert in site.author_certifications %}
          {% if cert.visibility == true %}
          <div class="row" style="margin-bottom: 20px; padding-bottom: 20px; border-bottom: 1px solid #e0e0e0;">
            <div class="col-md-2">
              <div class="preview-container" style="width:100%;display:flex;align-items:center;justify-content:center;min-height:96px;overflow:hidden;">
                {% if cert.preview_image %}
                  <img src="{{ cert.preview_image }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                {% elsif cert.preview_embed %}
                  {% assign pe = cert.preview_embed | strip %}
                  {% if pe contains '<' %}
                    <div class="embed-wrapper" style="display:flex;align-items:center;justify-content:center;">{{ pe }}</div>
                    {% if pe contains 'credly' %}{% assign has_credly = true %}{% endif %}
                  {% elsif pe contains 'http' %}
                    <img src="{{ pe }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                  {% endif %}
                {% elsif cert.cert_url %}
                  {% assign url_lower = cert.cert_url | downcase %}
                  {% if url_lower contains '.png' or url_lower contains '.jpg' or url_lower contains '.jpeg' or url_lower contains '.svg' or url_lower contains '.gif' %}
                    <img src="{{ cert.cert_url }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                  {% else %}
                    <img src="https://www.google.com/s2/favicons?sz=128&domain_url={{ cert.cert_url | uri_escape }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                  {% endif %}
                {% else %}
                  <img src="{{site.url}}{{site.baseurl}}/assets/img/profile.png" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                {% endif %}
              </div>
            </div>
            <div class="col-md-10">
              <h4 class="experience-title">{{ cert.cert_name }}</h4>
              <h6 class="experience-info">{{ cert.cert_issuer }}</h6>
              <p class="experience-desc">Certified: {{ cert.cert_date}} | Expires: {{ cert.cert_expiry }}</p>
              {% if cert.cert_url %}
              <p><a href="{{cert.cert_url}}" target="_blank">View Credential</a></p>
              {% endif %}
            </div>
          </div>
          {% endif %}
        {% endfor %}
      {% else %}
        <p>No certifications to display at this time.</p>
      {% endif %}
    </div>

    <!-- Badges Section -->
    <div class="card mb-3">
      <h1 class="card-title">Badges</h1>
      <br />
      {% if site.author_badges %}
        {% for badge in site.author_badges %}
          {% if badge.visibility == true %}
          <div class="row" style="margin-bottom: 20px; padding-bottom: 20px; border-bottom: 1px solid #e0e0e0;">
            <div class="col-md-2">
              <div class="preview-container" style="width:100%;display:flex;align-items:center;justify-content:center;min-height:96px;">
                {% if badge.preview_image %}
                  <img src="{{ badge.preview_image }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                {% elsif badge.preview_embed %}
                  {% assign pe = badge.preview_embed | strip %}
                  {% if pe contains '<' %}
                    <div class="embed-wrapper" style="display:flex;align-items:center;justify-content:center;">{{ pe }}</div>
                    {% if pe contains 'credly' %}{% assign has_credly = true %}{% endif %}
                  {% elsif pe contains 'http' %}
                    <img src="{{ pe }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                  {% endif %}
                {% elsif badge.badge_url %}
                  {% assign url_lower = badge.badge_url | downcase %}
                  {% if url_lower contains '.png' or url_lower contains '.jpg' or url_lower contains '.jpeg' or url_lower contains '.svg' or url_lower contains '.gif' %}
                    <img src="{{ badge.badge_url }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                  {% else %}
                    <img src="https://www.google.com/s2/favicons?sz=128&domain_url={{ badge.badge_url | uri_escape }}" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                  {% endif %}
                {% else %}
                  <img src="{{site.url}}{{site.baseurl}}/assets/img/profile.png" class="img-fluid rounded" alt="preview" style="max-width:96px;max-height:96px;" />
                {% endif %}
              </div>
            </div>
            <div class="col-md-10">
              <h4 class="experience-title">{{ badge.badge_name }}</h4>
              <h6 class="experience-info">{{ badge.badge_issuer }}</h6>
              <p class="experience-desc">Awarded: {{ badge.badge_date}} | Expires: {{ badge.badge_expiry }}</p>
              {% if badge.badge_url %}
              <p><a href="{{badge.badge_url}}" target="_blank">View Badge</a></p>
              {% endif %}
            </div>
          </div>
          {% endif %}
        {% endfor %}
      {% else %}
        <p>No badges to display at this time.</p>
      {% endif %}
    </div>
  </div>
</div>
{% if has_credly %}
<script type="text/javascript" async src="//cdn.credly.com/assets/utilities/embed.js"></script>
{% endif %}
</div>
