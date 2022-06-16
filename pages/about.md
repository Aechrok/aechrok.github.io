---
layout: page
title: 
permalink: /about/
---

#### (scrollable)
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=2">
        <script
        src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.0.943/pdf.min.js">
        </script>
        <style>
            div {text-align: center;}
            #canvas_container {
                width: 800px;
                height: 450px;
                overflow: auto;
            }
        </style>
    </head>
    <body>
        <div id="canvas_container">
            <canvas id="pdf_renderer"></canvas>
        </div>
    </body>
</html>

You can download my resume [here](https://github.com/Aechrok/Resume/raw/main/resume.pdf).

<script>
    var myState = {
            pdf: null,
            currentPage: 1,
            zoom: 1.25
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