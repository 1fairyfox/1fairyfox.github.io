---
layout: page
title: Projects
subtitle: Fairy Fox's software projects, with links into each one's documentation.
permalink: /projects/
---

This list is generated from a single registry (`_data/projects.yml`), which also
drives the home page and the navigation menu, so it stays current. Each project
links to its documentation site, its notes, and its repository.

<div class="grid cols-2" style="margin-top:1.5rem">
{%- for proj in site.data.projects -%}
  <div class="card">
    <h3>{{ proj.name }}</h3>
    <p>{{ proj.blurb }}</p>
    <div style="margin-bottom:.6rem">
      {%- for t in proj.tags -%}<span class="tag">{{ t }}</span>{%- endfor -%}
      {%- if proj.status -%}<span class="tag muted">{{ proj.status }}</span>{%- endif -%}
    </div>
    <div class="card-links">
      {%- if proj.docs -%}<a href="{{ proj.docs }}">Documentation ↗</a>{%- endif -%}
      {%- if proj.notes -%}<a href="{{ proj.notes }}">Notes ↗</a>{%- endif -%}
      <a href="{{ proj.repo }}">Repository ↗</a>
    </div>
  </div>
{%- endfor -%}
</div>

## How the projects connect

This site is the hub for the projects above. The shared engineering standards they
follow are documented in the [documentation library](/docs/), and each project
pulls those standards from the hub on demand. In the other direction, the hub
keeps read-only copies of the projects so their changes can be tracked and written
up. The connections are deliberately loose — git only, no live coupling — which
keeps each repository independent. The full model is described under
[cross-project sync](/docs/cross-project-sync/).

Because the hub uses a custom domain, the projects' own GitHub Pages sites are
served under it too — for example, `fairyfox.io/pokered-save-editor-2/` — so the
navigation can lead straight into a project's documentation.
