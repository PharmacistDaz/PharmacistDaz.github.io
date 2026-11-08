---
layout: post
title: "Why I Built a Chart of Fellowship Numbers"
date: 2026-11-08
tags: [pharmacy, professional-leadership, reflection]
author: Pharmacist Daz
---

I was part of a wide-ranging discussion the other evening, which I think was prompted in part by the [Royal College of Pharmacy Conference](https://www.rcpharm.org/events/rcpharm-annual-conference-2026/) held that day. It was interesting to hear people dismiss the “Fellowship” status of a “dying” organisation. This felt quite personal to me, as I see myself as one of the fortunate people who, through recognition by my peers, was put forward for a [Fellowship](https://www.rcpharm.org/information/list-of-current-fellows/) and accepted by the panel.

Recognition is a funny thing in our profession. Most of us do our work quietly, and when a Fellowship is announced, it often comes as a surprise to the recipient and to everyone watching.

The discussion got me thinking: just how many Fellowships have been awarded over the years? Is there an upward trend? Are they awarded more frequently than I had thought?

So I used my favourite LLM to research the question and assemble the figures. I went back to 2015 and counted from published lists, round by round. Some figures are official; others are counted from names. I couldn't find a figure for six rounds, so I've left those as visible gaps rather than guessing.

I built an interactive chart to share what I found. It is not a league table. It is a way of seeing recognition over time, including the parts nobody has published yet.

Make of the data what you will. This was an exercise driven purely by an inquisitive mind. I'm still working out what recognition means to me. The chart is my first attempt at asking that question properly.

The interactive dashboard below can also be [opened directly in a new tab]({{ '/assets/dashboards/rcpharm-fellowships-chart.html' | relative_url }}).

<div class="fellowships-dashboard">
  <iframe
    id="fellowships-dashboard"
    title="Interactive chart of new Fellows by award round, 2015 to November 2026"
    src="{{ '/assets/dashboards/rcpharm-fellowships-chart.html' | relative_url }}"
    loading="lazy"
    sandbox="allow-scripts allow-downloads"
    referrerpolicy="no-referrer"
    style="display: block; width: 100%; height: 900px; border: 0;">
  </iframe>
</div>

<p><a href="{{ '/assets/dashboards/rcpharm-fellowships-chart.html' | relative_url }}" target="_blank" rel="noopener noreferrer">Open the interactive dashboard in a separate tab</a> (recommended on smaller screens or if the embedded view does not load).</p>

<script>
  (function () {
    var frame = document.getElementById("fellowships-dashboard");
    if (!frame) return;

    window.addEventListener("message", function (event) {
      if (event.source !== frame.contentWindow || !event.data || typeof event.data.rcpHeight !== "number") return;
      var height = Math.round(event.data.rcpHeight);
      if (height < 320 || height > 4000) return;
      frame.style.height = height + "px";
    });
  })();
</script>

<style>
  .fellowships-dashboard {
    width: 100%;
    overflow: hidden;
  }

  .fellowships-dashboard iframe {
    max-width: 100%;
  }
</style>
