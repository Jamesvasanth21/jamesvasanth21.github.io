---
title: Professional Journey
layout: default
permalink: /professional_journey/
---

<div id="professional_journey" class="card">
    <h1>Professional Journey</h1>
    
    {% for job in site.data.work_experience %}
    {% assign key = job[0] %}
    {% assign details = job[1] %}
    
    <div id="{{ key }}">
    <div class="row align-items-center" style="margin-bottom:20px;padding-bottom:20px;border-bottom:1px solid #e0e0e0;">
        <div class="col-md-2 col-3">
            <a href="{{details.company_url}}">
            <img src="{{site.baseurl}}/assets/images/{{ details.company_logo }}" class="img-fluid rounded" style="width:90px;height:90px;object-fit:contain;" />
            </a>
        </div>
        <div class="col-md-10 col-9">
            <h3>{{ details.company_name}}</h3>
            <h4 class="experience-title">{{ details.designation }}</h4>
            <p class="experience-desc">{{ details.duration }}</p>
            <p class="experience-desc">{{ details.short_description }}</p>
            <h7 class="experience-info">Detailed Description:</h7>
            <p>
            {% for section in details.detailed_description %}
            <ul>
            <li>{{ section.title }}</li>
                {% for point in section.points %}
                <ul>
                <li>{{ point }}</li>
                </ul>
                {% endfor %}
            </ul>
            {% endfor %}
            </p>
            <!-- <p><a href="{{details.company_url}}">{{ details.company_name }}</a></p> -->
        </div>
    </div>
    </div>
    
    {% endfor %}

</div>