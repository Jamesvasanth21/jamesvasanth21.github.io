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
    <h3>{{ details.company_name}}</h3>
    </div>
    
    {% endfor %}

</div>