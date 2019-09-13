(function ($) {

    kendoGridPrint = function (selector, reportName) {
        var thIndex = [];
        var gridElement = $(selector),
            clonedGridElement = gridElement.clone()[0],
            tableSummaryElement = $('#table-summary'),
            noRecElement = $('.k-grid-norecords'),
            printableContent = '',
            printableSummary = '',
            excludedColumnsCount = 0,
            totalColumnsCount = 0,
            noRecColSpan = 1,
            noRecMsg = ''
            noRecTemplate = '<tr><td colspan=\''+ noRecColSpan +'\'>'+ noRecMsg +'</td></tr>',
                win = window.open('', '', 'width=800, height=500, resizable=1, scrollbars=1'),
                doc = win.document.open();

        var htmlStart =
            '<!DOCTYPE html>' +
            '<html>' +
            '<head>' +
            '<meta charset="utf-8" />' +
            '<title>' + reportName + '</title>' +
            '<style>' +
            'html { font: 11pt sans-serif; }' +
            'p { margin: 0px 0px 0px 0px; font-weight: 700; }' +
            '.report-title {  font-size: 12px; font-weight: 700; text-align: center; margin-bottom: 10px;}' +
            '.container { margin-left: 10px; margin-right: 10px; }' +
            '.ignore { display: none; }' +
            '.k-grid { border-top-width: 0; }' +
            '.reportGrids { border: 0px solid black !important; line-height: 1.42857143 !important; color: black !important; width: 100% !important; border-collapse: collapse;}' +
            '.reportGrids tr > td, .reportGrids tr > th { padding: 8px !important; border: 1px solid black; font-size: 11px !important;}' +
            '.reportGrids .k-grid-header .k-header > a { font-size: 11px !important; font-weight: 700 !important; font-family: inherit !important; }' +
            '.reportGrids .k-grid-header .k-header > a:hover, a:link, a:visited, a:active, a a:focus { text-decoration: none; outline: none; color: black; }' +
            '.reportGrids .k-grid-header .k-header { background-color: #cecece; }' +
            '.k-grid, .k-grid-content { height: auto !important; }' +
            '.k-grid-content { overflow: visible !important; }' +
            'div.k-grid table { table-layout: auto; width: 100% !important; }' +
            '.k-grid .k-grid-header th { border-top: 1px solid; }' +
            '.k-grouping-header, .k-grid-toolbar, .k-grid-pager > .k-link { display: none; }' +
            '.k-grid-pager { display: none; }' + // optional: hide the whole pager
            '.k-footer-template { font-weight: 700; }' +
            '#table-summary { font-size: 11px; font-weight: 700; margin-top: 5px; }' +
            '#table-summary > div{ display: inline; margin-right: 5px; }' +
            '.hide { display: none; }' +
            '</style>' +
            '</head>' +
            '<body>' +
            '<div class="container">' +
            '<div class="report-title">' + reportName +'</div>';

        var htmlEnd =
            '</div>' +
			'</body>' +
            '</html>';

        excludedColumnsCount = $(clonedGridElement).find('tr > th.ignore').length;
        totalColumnsCount = $(clonedGridElement).find('tr > th').length;

        if (noRecElement[0]) {
            noRecColSpan = totalColumnsCount - excludedColumnsCount;
            noRecMsg = noRecElement.first().html();
            $(clonedGridElement).find('tbody').append('<tr><td colspan=\'' + noRecColSpan + '\'>' + noRecMsg + '</td></tr>');
        }

        $(clonedGridElement).find('tr.k-grouping-row td').attr('colspan', totalColumnsCount - excludedColumnsCount);

        $(clonedGridElement).find('tr > th.ignore').each(function () {
            var index = -1;
            index = $(this).index();

            if (index > -1) {
                thIndex.push(index);
            }
        });

        thIndex.forEach(function (item, index) {
            $(clonedGridElement).find('tfoot tr.k-footer-template td:eq(' + item + ')').addClass('ignore');
        });

        $(clonedGridElement).find('tbody tr').removeAttr("style");
        $(clonedGridElement).find('span.grid-command').closest('td').remove();
        $(clonedGridElement).find('span.grid-command').closest('th').remove();
        printableContent = clonedGridElement.outerHTML;

        if (tableSummaryElement[0]){
            printableSummary = tableSummaryElement.clone()[0].outerHTML;
        }

        doc.write(htmlStart + printableContent + printableSummary + htmlEnd);
    	doc.close();
    	win.print();
    }

}(jQuery));