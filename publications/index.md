---
title: Publications
banner_image: images/diffractometer_crop.jpg
banner_position: top left
banner_title: Publications
banner_subtitle: A list of my academic publications
enable_alm: true
template: base.html
---

{%- import "macros.html" as macros %}

<h2 class="mb-4">
Protein Structures in the RCSB Protein Data Bank
</h2>
<button class="btn btn-secondary btn-sm me-1 mb-2" type="button"
      data-bs-toggle="collapse" data-bs-target="#collapse-99"
      aria-expanded="false" aria-controls="collapse-99">
    Find out more <i class="fa fa-chevron-circle-down ms-1" aria-hidden="true"></i>
</button>
<div id="collapse-99" class="collapse mt-2 overflow-hidden">
<p> These are the novel protein structures that I've contributed to through doing one or a combination of these things: expressing, purifying, crystallising, finding ligands for co-crystallisation, collecting data or solving and refining the structure.
</p>
 
 <table>
 <tr>
    <th>Class</th>
    <th>Name</th>
    <th>ID</th>
    <th>Name</th>
    <th>ID</th>
    <th>Name</th>
    <th>ID</th>
    <th>Name</th>
    <th>ID</th>
  </tr>
{%- for struct in page.structures %}
<tr>
  <td>
  <h2 class="fs-4 mb-1">
  {%- if struct.class != "None" %}
    {{ struct.class|trim }}
  {%- else %}
  <p></p>
  {%- endif %}
  </h2>
  </td>
  {%- for protein in struct.members %}
  <td>
   <h2 class="fs-6 mb-1">
    <a target="_blank" href="https://pubchem.ncbi.nlm.nih.gov/gene/{{ protein.hugo }}">{{ protein.hugo }}</a>
  </h2>
  </td>
   <td>
  {%- for pdb in protein.members %}
   <h4 class="fs-6 mb-1 pr-5">
    <a target="_blank" href="https://www.rcsb.org/structure/{{ pdb }}">{{ pdb }}</a>
  </h4>
  {%- endfor %}
  </td>
  {%- endfor %}
  </td>
</tr>
{%- endfor %}
</table>
</div>

<h2 class="mb-4">
Research Papers
</h2>
<button class="btn btn-secondary btn-sm me-1 mb-2" type="button"
      data-bs-toggle="collapse" data-bs-target="#collapse-98"
      aria-expanded="false" aria-controls="collapse-98">
    Find out more <i class="fa fa-chevron-circle-down ms-1" aria-hidden="true"></i>
</button>
<div id="collapse-98" class="collapse mt-2 overflow-hidden">

<h4> This list, currently under construction, gives details of my contributions to published research papers. 
</h4>

{%- for paper in page.papers %}
  {%- set id = loop.index %}
  {%- if paper.doi is defined %}
    {%- set doi = paper.doi %}
  {%- else %}
    {%- set doi = paper.preprint %}
  {%- endif %}
  {%- if paper.openaccess is defined and paper.openaccess %}
    {%- set pdf = "https://doi.org/" ~ paper.doi %}
  {%- elif paper.preprint is defined %}
    {%- set pdf = "https://doi.org/" ~ paper.preprint %}
  {%- elif paper.pdf is defined %}
    {%- set pdf = paper.pdf %}
  {%- endif %}
<div class="mb-5">
  <h2 class="fs-4 mb-1">
    {{ paper.title|trim }}
  </h2>
  <p class="mb-1">
    <span class="text-muted">{{ paper.year }}</span>
    |
    {{ paper.authors|trim }}
  </p>
  <p class="text-muted fs-6">
    {%- if paper.openaccess is defined and paper.openaccess %}
      <span class="badge bg-success fw-normal me-1">
        <i class="ai ai-open-access me-1" aria-hidden="true"></i>
        open-access
      </span>
    {%- endif %}
    {%- if paper.preprint is defined and not paper.doi is defined %}
      <span class="badge bg-warning text-dark fw-normal me-1">
        preprint
      </span>
    {%- endif %}
    {{ paper.journal }},
    doi:<a target="_blank" href="https://doi.org/{{ doi }}">{{ doi }}</a>
  </p>
  <button class="btn btn-secondary btn-sm me-1 mb-2" type="button"
      data-bs-toggle="collapse" data-bs-target="#collapse-{{ id }}"
      aria-expanded="false" aria-controls="collapse-{{ id }}">
    Find out more <i class="fa fa-chevron-circle-down ms-1" aria-hidden="true"></i>
  </button>
  {{ macros.button_link(pdf, "PDF", type="btn-primary", icon="fa fa-file-pdf") }}
  {%- if paper.data is defined %}
    {{ macros.button_link("https://doi.org/" ~ paper.data, "Data", type="btn-light", icon="fa fa-chart-bar") }}
  {%- endif %}
  {%- if paper.github is defined %}
    {{ macros.button_link("https://github.com/" ~ paper.github, "Code", type="btn-light", icon="fab fa-github") }}
  {%- endif %}
  <div id="collapse-{{ id }}" class="collapse paper-info mt-2 overflow-hidden">
    {%- if paper.note is defined %}
      <div class="callout callout-note mb-4">
        <p><strong>Note:</strong> {{ paper.note|trim }}</p>
      </div>
    {%- endif %}
    <h3 class="fs-4">Abstract</h3>
    <p>{{ paper.abstract|trim }}</p>
    <h3 class="fs-4">Cite as</h3>
    <blockquote class="mb-4">{{ paper.citation|trim }}</blockquote>
    <h3 class="fs-4 mb-4">Citations</h3>
    <span class="__dimensions_badge_embed__" data-doi="{{ doi }}"></span>
  </div>
</div>
{%- endfor %}
</div>
