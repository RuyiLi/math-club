<<<<<<< HEAD
# test

asdf



<style>
    canvas { 
        border-image: linear-gradient(120deg, #155799, #159957);
        border-image-slice: 1;
        border-width: 50px;
        border-style: solid;
    }
</style>

<!--
    Import PDF.js required libraries 
-->
<script src="pdf.js"></script>
<script src="pdf.worker.js"></script>

<canvas data-source="https://raw.githubusercontent.com/chfrn/Erindale-Math-Club/master/Number%20Theory/Divisibility%20and%20GCD%20Part%201.pdf" data-scale="0.5"></canvas>

<script type="text/javascript">

    const renderPDF = async (canvas, fname, zoom = 1) => {
        const $ = document.querySelector.bind(document);

        //const canvas = document.createElement('canvas');
        const ctx = canvas.getContext('2d');
        const rect = canvas.getBoundingClientRect();
    

        const pdf = await pdfjsLib.getDocument(fname);

        const { numPages } = pdf._pdfInfo;

        let currentPage = 0, page, viewport;

        canvas.onclick = (e) => {
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            updatePage(x > canvas.width / 2);
        }

        document.onkeydown = (e) => {
            if(e.keyCode === 39 || e.keyCode === 37) updatePage(e.keyCode === 39)
        }

        const updatePage = async (right) => {
            if(right) currentPage = Math.min(currentPage + 1, numPages);
            else currentPage = Math.max(1, currentPage - 1)

            page = await pdf.getPage(currentPage);

            let view = page.getViewport(1 / zoom);

            canvas.width = view.width;
            canvas.height = view.height;

            const renderContext = { 
                canvasContext: ctx,
                viewport: view
            }

            await page.render(renderContext);
        }

        updatePage(1);
    }

    for(const c of document.getElementsByTagName('canvas')){
        console.log(c.dataset)
        renderPDF(c, c.dataset.source, +c.dataset.scale || 0.5);
    }

</script>
=======
# math-club
A website for the competitive math club
>>>>>>> 5415f03850c8add216f97485b90b532499b38f48
