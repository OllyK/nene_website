---
title: About
banner_image: images/queenstown_hd_wide.jpg
banner_position: top left
banner_title: About me
banner_subtitle: A bit more about me and my work
template: base.html
---


<section class="mb-5">

## The slightly longer version

I work as a Data Analysis Scientist in Machine Vision, working as part of the Data Analysis group at [Diamond Light Source][dls-link], South Oxfordshire, UK. 
Before this, I worked in a product design start-up that specialised in the Internet of Things. My work there was a mixture of writing RESTful APIs in Python, setting up an end-to-end testing framework with integrated hardware, consulting on the feasibility of new IOT projects and researching potential new clients. 
Prior to working in the startup I completed an MSc. degree in Computer Science 
at the University of Bristol, which was a big change from my previous vocation 
as a research scientist in Chemical Biology. 

My current work makes use of deep learning, particularly convolutional neural networks, 
to create tools that help scientists who work at Diamond as well as those who visit as
facility users. One of the main areas is [segmentation][segment] of 3-dimensional image data such as that produced by [X-ray computed tomography][xray-ct] (XCT), [electron cryo-tomography][ect] (cryoET) or [serial block-face scanning electron microscopy][sbf] (SBF-SEM). In addition, I have created deep learning tools that aid scientists who are performing experiments where they aim to grow protein crystals. For example, detecting the location of these crystals is the first step in collecting in-situ data on a fully automated macromolecular crystallography (MX) beamline at Diamond, known as [VMXi][vmxi-link].


<section class="mb-5">

## Education

{% import "macros.html" as macros %}

{# The education list is defined in about/data.yml #}
{% for item in page.education %}

<div class="mb-3">
{%- set id = loop.index %}
<h2 class="fs-4 mb-1">
  {{ item.level|trim }}
</h2>
<p class="mb-1">
  <span class="text-muted">{{ item.year }}</span>
  |
  {{ item.institution|trim }}
</p>
<p class="mb-1 text-muted fs-6">
  Thesis: {{ item.title|trim }}
</p>
<p class="mb-1 text-muted fs-6">
  Supervisors: {{ item.advisor }}
</p>
<button class="btn btn-secondary btn-sm me-1 mb-2" type="button"
    data-bs-toggle="collapse" data-bs-target="#collapse-abstract-{{ id }}"
    aria-expanded="false" aria-controls="collapse-abstract-{{ id }}">
  Find out more <i class="fa fa-chevron-circle-down ms-1" aria-hidden="true"></i>
</button>
{%- if item.pdf is defined %}
  {{ macros.button_link("../pdf/" ~ item.pdf, "PDF", type="btn-primary", icon="fa fa-file-pdf") }}
{%- endif %}
<div id="collapse-abstract-{{ id }}" class="collapse paper-info mt-2 overflow-hidden">
  <h3 class="">About</h3>
  {{ item.notes }}
{%- if item.abstract is defined %}
  <h3 class="">Abstract</h3>
  <p>{{ item.abstract|trim }}</p>
{%- endif %}
</div>
</div>

{% endfor %}

</section>


[dls-link]: https://www.diamond.ac.uk
[segment]: https://en.wikipedia.org/wiki/Image_segmentation
[xray-ct]: https://www.diamond.ac.uk/Instruments/Techniques/Imaging/Tomography.html
[ect]: https://en.wikipedia.org/wiki/Electron_cryotomography
[sbf]: https://en.wikipedia.org/wiki/Serial_block-face_scanning_electron_microscopy
[vmxi-link]: https://www.diamond.ac.uk/Instruments/Mx/VMXi.html