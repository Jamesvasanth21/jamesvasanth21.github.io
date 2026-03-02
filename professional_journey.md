---
title: Professional Journey
layout: default
permalink: /professional_journey/
---

<div id="professional_journey" class="card">
    <h1>Professional Journey</h1>
    </br>
 
    {% for job in site.data.work_experience %}
    {% assign details = job[1] %}
    
    <div id="{{ details.company_name}}">
    <div class="row align-items-center" style="margin-bottom:20px;padding-bottom:20px;border-bottom:1px solid #e0e0e0;">
        <div class="col-md-2 col-3">
          <img src="{{site.baseurl}}/assets/images/{{ details.company_logo }}" class="img-fluid rounded"
              style="width:90px;height:90px;object-fit:contain;" />
        </div>
        <div class="col-md-10 col-9">
          <h4 class="experience-title">{{ details.designation }}</h4>
          <h6 class="experience-info">{{ details.company_name}}</h6>
          <p class="experience-desc">{{ details.duration }}</p>
          <p class="experience-desc">{{ details.short_description }}</p>
          <p><a href="{{details.company_url}}">{{ exp.company_url}}</a></p>
          <h7 class="experience-info">Detailed Description</h7>
          <p>{{ details.detailed_description}}</p>
        </div>
    <h3>{{ details.company_name}}</h3>
    </div>
    </div>
    
    {% endfor %}

</div>