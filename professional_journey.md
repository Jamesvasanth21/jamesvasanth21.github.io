---
title: Professional Experience
layout: default
permalink: /professional_experience/
---

<script>

function normalizeEndDate(endDate) {

    if (
        !endDate ||
        String(endDate).toLowerCase() === "present"
    ) {

        return new Date();
    }

    return new Date(endDate);
}

function calculateMonths(
    startDate,
    endDate
) {

    const start =
        new Date(startDate);

    const end =
        normalizeEndDate(endDate);

    if (
        isNaN(start.getTime()) ||
        isNaN(end.getTime())
    ) {

        return 0;
    }

    let months =
        (end.getFullYear() - start.getFullYear()) * 12;

    months +=
        end.getMonth() - start.getMonth();

    if (end.getDate() < start.getDate()) {

        months--;
    }

    return Math.max(months, 0);
}

function formatDuration(months) {

    const years =
        Math.floor(months / 12);

    const remainingMonths =
        months % 12;

    return (
        `${years} Years ${remainingMonths} Months`
    );
}

window.addEventListener(
    "load",
    () => {

        let totalMonths = 0;

        const durationElements =
            document.querySelectorAll(
                ".job-duration"
            );

        durationElements.forEach(el => {

            const start =
                el.dataset.start;

            const end =
                el.dataset.end;

            const months =
                calculateMonths(
                    start,
                    end
                );

            totalMonths += months;

            el.innerText =
                formatDuration(months);
        });

        const totalExperience =
            document.getElementById(
                "total-experience"
            );

        if (totalExperience) {

            totalExperience.innerText =
                formatDuration(totalMonths);
        }
    }
);

</script>

<style>

.experience-header {

    display: flex;

    align-items: baseline;

    gap: 12px;

    flex-wrap: wrap;

    margin-bottom: 12px;
}

.experience-meta {

    font-size: 1rem;

    color: rgba(255,255,255,0.65);

    font-weight: 400;

    letter-spacing: 0.3px;
}

.job-duration {

    color: rgba(255,255,255,0.7);
}

.job-card {

    margin-bottom: 24px;

    padding-bottom: 24px;

    border-bottom: 1px solid #e0e0e0;
}

.company-logo {

    width: 90px;

    height: 90px;

    object-fit: contain;
}

.details-heading {

    margin-top: 16px;

    margin-bottom: 12px;

    font-weight: 600;
}

.job-description-list {

    padding-left: 18px;
}

.job-description-list li {

    margin-bottom: 10px;
}

</style>

<div id="professional_experience" class="card">

    <div class="experience-header">

        <h1 class="card-title">
            Professional Experience
        </h1>

        <span class="experience-meta">

            {{ site.data.work_experience | size }} Roles
            ·
            <span id="total-experience"></span>

        </span>

    </div>

    <hr class="section-divider">

    {% for job in site.data.work_experience %}

    {% assign key = job[0] %}
    {% assign details = job[1] %}

    <div
        id="{{ key | slugify }}"
        class="job-card"
    >

        <div class="row align-items-center">

            <div class="col-md-2 col-3">

                <a
                    href="{{ details.company_url }}"
                    target="_blank"
                >

                    <img
                        src="{{site.baseurl}}/assets/images/{{ details.company_logo }}"
                        class="img-fluid rounded company-logo"
                    />

                </a>

            </div>

            <div class="col-md-10 col-9">

                <h3>
                    {{ details.company_name }}
                </h3>

                <h4 class="experience-title">
                    {{ details.designation }}
                </h4>

                <p class="experience-desc">

                    {{ details.duration }}

                    ·

                    <span
                        class="job-duration"
                        data-start="{{ details.start_date }}"
                        data-end="{{ details.end_date }}">
                    </span>

                </p>

                <p class="experience-desc">
                    {{ details.short_description }}
                </p>

                <div class="details-heading">
                    Detailed Description
                </div>

                <ul class="job-description-list">

                    {% for section in details.detailed_description %}

                    <li>

                        {{ section.title }}

                        {% if section.points %}

                        <ul>

                            {% for point in section.points %}

                            <li>
                                {{ point }}
                            </li>

                            {% endfor %}

                        </ul>

                        {% endif %}

                    </li>

                    {% endfor %}

                </ul>

            </div>

        </div>

    </div>

    {% endfor %}

</div>