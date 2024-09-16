---
title: Notebooks.Timelines
hidden: true
tags: [notebook]
---

The notebook creates a default Super-Timeline.

Timelines are used to visualize time series data from other
collections in the same place. This notebook template creates an
initial timeline.

Once this timeline is created, you can add any time series table in
other notebooks (e.g. Collection or Hunt notebooks) to this super
timeline.


<pre><code class="language-yaml">
name: Notebooks.Timelines
description: |
  The notebook creates a default Super-Timeline.

  Timelines are used to visualize time series data from other
  collections in the same place. This notebook template creates an
  initial timeline.

  Once this timeline is created, you can add any time series table in
  other notebooks (e.g. Collection or Hunt notebooks) to this super
  timeline.

type: NOTEBOOK

parameters:
  - name: TimelineName
    description: The name of the super timeline to create.
    default: Supertimeline

sources:
  - notebook:
      - type: markdown
        template: |
          # {{ Scope "TimelineName" }}

          Add to this timeline any time-series data from any other
          notebooks:

          1. Click the `Add Timeline` button at the top of any table.
          2. Switch to global notebook timelines and select this timeline.
          3. Select the timestamp and message columns to add a timeline.

          {{ Scope "TimelineName" | Timeline }}

      - type: vql
        template: |
          /*
          # Timeline Annotations

          Refresh this to list all timeline annotations as a table.
          */
          SELECT *
          FROM timeline(notebook_id=NotebookId,
                        components="Annotation",
                        timeline=TimelineName)
          ORDER BY Timestamp

</code></pre>
