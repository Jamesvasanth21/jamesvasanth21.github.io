---
title: Professional Experience
layout: default
permalink: /professional_experience/
---

<script>
console.log("Script initialized");

function normalizeEndDate(endDate) {
    if (!endDate || String(endDate).toLowerCase() === "present") {
        return new Date();
    }
    const date = new Date(endDate);
    if (isNaN(date.getTime())) {
        return new Date();
    }
    return date;
}

function calculateMonths(startDate, endDate) {
    const start = new Date(startDate);
    const end = normalizeEndDate(endDate);
    const today = new Date();

    if (isNaN(start.getTime()) || isNaN(end.getTime()) || start > today || start > end) {
        return 0;
    }

    let totalMonths = (end.getFullYear() - start.getFullYear()) * 12 + (end.getMonth() - start.getMonth());
    let remainingDays = end.getDate() - start.getDate();

    if (remainingDays < 0) {
        totalMonths -= 1;
        remainingDays += new Date(end.getFullYear(), end.getMonth(), 0).getDate();
    }

    const daysInMonth = new Date(end.getFullYear(), end.getMonth() + 1, 0).getDate();
    if (remainingDays >= daysInMonth / 2) {
        totalMonths += 1;
    }

    return Math.max(totalMonths, 0);
}

function formatDuration(totalMonths) {
    const years = Math.floor(totalMonths / 12);
    const months = totalMonths % 12;

    const yearStr = years === 1 ? "1 Year" : `${years} Years`;
    const monthStr = months === 1 ? "1 Month" : `${months} Months`;

    return `${yearStr} ${monthStr}`;
}

window.addEventListener(
    "load",
    function () {

        console.log("Rendering durations");

        var totalMonths = 0;

        var durations =
            document.querySelectorAll(
                ".job-duration"
            );

        console.log(
            "Durations found:",
            durations.length
        );

        if (durations.length === 0) {

            return;
        }

        durations.forEach(function (el) {

            var start =
                el.getAttribute("data-start");

            var end =
                el.getAttribute("data-end");

            console.log(
                "Processing:",
                start,
                end
            );

            var months =
                calculateMonths(
                    start,
                    end
                );

            totalMonths += months;

            el.innerText =
                formatDuration(months);
        });

        console.log(
            "Total months:",
            totalMonths
        );

        var totalExperience =
            document.getElementById(
                "total-experience"
            );

        if (totalExperience) {

            totalExperience.innerText =
                formatDuration(totalMonths);

            console.log(
                "Updated total experience"
            );
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