---
title: Professional Experience
layout: default
permalink: /professional_experience/
---

<script>

function calculateDuration(
    startDate,
    endDate
) {

    const start = new Date(startDate);

    let end;

    if (
        !endDate ||
        endDate.toLowerCase() === "present"
    ) {
        end = new Date();
    } else {
        end = new Date(endDate);
    }

    let years =
        end.getFullYear() -
        start.getFullYear();

    let months =
        end.getMonth() -
        start.getMonth();

    if (months < 0) {
        years--;
        months += 12;
    }

    return (
        `${years} Years ${months} Months`
    );
}

document.addEventListener(
    "DOMContentLoaded",
    function () {

        const durations =
            document.querySelectorAll(
                ".job-duration"
            );

        durations.forEach(el => {

            const start =
                el.dataset.start;

            const end =
                el.dataset.end;

            el.innerText =
                calculateDuration(
                    start,
                    end
                );
        });
    }
);

</script>

<div id="professional_experience" class="card">
    <!-- <h1>Professional Experience</h1> -->
    <h1 class="card-title">
    Professional Experience ({{ site.data.work_experience | size }} Roles .  )
    </h1>
    <hr class="section-divider">
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
            
            <p class="experience-desc">
            
                {{ details.duration }}
            
                ·
            
                <span
                    class="job-duration"
                    data-start="{{ details.start_date }}"
                    data-end="{{ details.end_date }}">
                </span>
            
            </p>
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