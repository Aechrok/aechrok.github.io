---
layout: page
title: 
permalink: /about/
---

<!-- <div id="canvas_container" style="margin: auto; border: 3px solid green; padding: 10px; width: 70vh; height: 90vh;"> -->
<div id="canvas_container" style="margin-left:auto; margin-right:auto;">
    <canvas id="pdf_renderer"></canvas>
</div>

You can download my resume [here](https://github.com/Aechrok/Resume/raw/main/resume.pdf).

<script>
    var myState = {
            pdf: null,
            currentPage: 1,
            zoom: 1.5
        }
      
        pdfjsLib.getDocument('{{ site.baseurl }}/assets/resume.pdf').then((pdf) => {
      
            myState.pdf = pdf;
            render();
 
        });
 
        function render() {
            myState.pdf.getPage(myState.currentPage).then((page) => {
          
                var canvas = document.getElementById("pdf_renderer");
                var ctx = canvas.getContext('2d');
      
                var viewport = page.getViewport(myState.zoom);
 
                canvas.width = viewport.width;
                canvas.height = viewport.height;
          
                page.render({
                    canvasContext: ctx,
                    viewport: viewport
                });
            });
        }
</script>