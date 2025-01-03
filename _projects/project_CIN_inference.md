---
layout: page
title: Chromosomal instability (CIN) and selection during cancer development
description: Mathematical and computational methods to extract tissue-specific CIN occurrence rates and selection coefficients from single-cell DNA-sequencing data
img: assets/img/project_CIN_inference_background.png
importance: 1
# category: work
related_publications: true
---

---

Recent developments in single-cell DNA-sequencing have provided an unparalleled view into the diversity and ongoing evolution within a tumor.
Direct Library Development+ (DLP+), developed by the [Sohrab Shah Lab](https://www.mskcc.org/research-areas/labs/sohrab-shah), is capable of producing genomic information for tens of thousands of cells, without bias due to amplification or non-uniform coverage {% cite laks2019clonal %}.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_CIN_inference_DLP_1.png" title="DLP+ pipeline" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    DLP+ {% cite laks2019clonal %} provides copy number (CN) information at the cell level.  
    Left: Overview of DLP+ experimental and computational pipeline.  
    Right: Total copy numbers (top) and minor allele fractions (bottom) across the genome in one cell from an ovarian tumor.
</div>

By grouping similar cells into clones and tracking them over time, DLP+ data provides a picture of competition between different clones.
This indicates that selection plays an important role during tumor growth, and certain genomic profiles are preferred over others {% cite salehi2021clonal %}.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_CIN_inference_DLP_2.png" title="DLP+ signatures" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Evolution of clones with distinct copy numbers from a triple-negative breast tumor over time {% cite salehi2021clonal %}.  
    Left: Phylogeny of cells based on their copy number profiles. Cells with similar copy numbers are grouped into a clone.  
    Right: Clonal fractions in the cell population over time.
</div>

Furthermore, applications of DLP+ have led to the realization that knock-outs of certain important genes, such as TP53 and BRCA1/2 in the mammary epithelium, are associated with a significant increase in chromosomal instability {% cite funnell2022single %}.
This manifests in higher number of polyploid cells (resulting from whole-genome duplications) and more chromosome missegregations.
These results explain the high copy number aberrations that have been observed in ovarian and breast cancers.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/project_CIN_inference_DLP_3.png" title="DLP+ signatures" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Copy number changes associated with key genes being turned off in mammary epithelial cell lines {% cite funnell2022single %}.  
    Top: Total and allele-specific copy numbers in cells with TP53 knocked out (left) and both TP53 and BRCA1 knocked out (right).  
    Bottom: Statistics of cell populations, depending on whether TP53, BRCA1 or BRCA2 are knocked out.
</div>

---

We seek

---

{% cite dinh2024cinner %}

{% cite xiang2024inference %}

{% cite dinh2024approximate %}

{% cite mcpherson2024ongoing %}



<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images, even citations {% cite einstein1950meaning %}.
Say you wanted to write a bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
