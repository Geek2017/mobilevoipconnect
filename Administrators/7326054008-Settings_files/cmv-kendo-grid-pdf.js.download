(function ($) {

    kendoGridPdf = function (selector, options) {
        var thIndex = [];
        var excludedColumnsCount = 0;
        var totalColumnsCount = 0;
        //var progress = $.Deferred();
        var clonedGridElement = $(selector).clone()[0];
        var reportTitle = (options.reportTitle != undefined && options.reportTitle != '') ? options.reportTitle : 'CMV Report';
        var reportName = (options.reportName != undefined && options.reportName != '') != '' ? options.reportName : 'CMV Report';
        var pdfTemplate = '<div class="page-template">' +
            '<div class="header-date">' + moment().format('MM/DD/YYYY HH:mm') + '</div>' +
            '<div class="header">' +
            reportTitle  +
            '</div>' +
            '<div class="footer">' +
            '<div style="float: right">Page #: pageNum # of #: totalPages #</div>' +
            '</div>' +
            '</div >';

        var settings = $.extend({
            paperSize: "Letter",
            margin: { top: "2cm", right: "1cm", bottom: "1cm", left: "1cm" },
            multiPage: true,
            template: pdfTemplate,
            repeatHeaders: true,
            scale: .8,
            landscape: false,
            template: pdfTemplate
        }, options);

        excludedColumnsCount = $(clonedGridElement).find('tr > th.ignore').length;
        totalColumnsCount = $(clonedGridElement).find('tr > th').length;

        $('#pdf-container').remove();
        $(clonedGridElement).attr('id', 'grid-pdf');
        $(clonedGridElement).find('p.k-reset a.k-icon').removeClass("k-i-expand").addClass("k-i-collapse");
        $(clonedGridElement).find('tbody tr').removeAttr("style");
        $(clonedGridElement).find('tr.k-state-selected').removeClass("k-state-selected");

        $(clonedGridElement).find('span.grid-command').closest('th').each(function () {
            var index = -1;
            index = $(this).index();

            if (index > -1) {
                thIndex.push(index);
            }

            $(this).remove();
        });

        thIndex.forEach(function (item, index) {
            $(clonedGridElement).find('colgroup col:eq(' + item + ')').remove();
        });

        $(clonedGridElement).find('span.grid-command').closest('td').remove();

        $(clonedGridElement).find('tr > th.ignore').each(function () {
            var index = -1;
            index = $(this).index();

            if (index > -1) {
                thIndex.push(index);
            }

            $(this).remove();
        });

        thIndex.forEach(function (item, index) {
            $(clonedGridElement).find('colgroup col:eq(' + item + ')').remove();
            $(clonedGridElement).find('tfoot tr.k-footer-template td:eq(' + item + ')').remove();
        });
        
        $(clonedGridElement).find('.ignore').remove();
        $(clonedGridElement).find('tr.k-grouping-row td').attr('colspan', totalColumnsCount - excludedColumnsCount);

        $('body').append('<div id="pdf-container" style="position: absolute; left: -10000px; top: 0; height: 100px; width: 100px; overflow: scroll;"><div id="pdf-content" class="k-grid k-widget k-display-block"></div></div>');
        $('#pdf-content').append(clonedGridElement.outerHTML);

        kendo.drawing.drawDOM('#pdf-content', settings)
            .then(function (group) {
                kendo.drawing.pdf.saveAs(group, reportName + '.pdf');
                $('#pdf-container').remove()
            });
    }

}(jQuery));