function renderLatexEquations() {
  var body = DocumentApp.getActiveDocument().getBody();

  var insideEquation = false;
  var equationLines = [];
  var startIndex = -1;

  for (var i = 0; i < body.getNumChildren(); i++) {
    var elem = body.getChild(i);

    if (elem.getType() === DocumentApp.ElementType.PARAGRAPH) {
      var text = elem.asParagraph().getText();

      if (!insideEquation) {
        if (text.includes('\\begin{equation}')) {
          insideEquation = true;
          startIndex = i;
          equationLines = [];

          // Add text after \begin{equation} to lines, keep line break
          equationLines.push(text.substring(text.indexOf('\\begin{equation}') + 16));
        }
      } else {
        // Collect all lines inside equation environment
        if (text.includes('\\end{equation}')) {
          // Add up to \end{equation}
          equationLines.push(text.substring(0, text.indexOf('\\end{equation}')));

          // Join all lines with new line characters to preserve formatting
          var equationText = equationLines.join('\n').trim();

          // Render the full latex string including line breaks
          var imageUrl = renderLatexToImage(equationText);

          // Remove paragraphs from startIndex to current i in reverse order
          for (var j = i; j >= startIndex; j--) {
            body.removeChild(body.getChild(j));
          }

          // Insert rendered image at startIndex
          var imgBlob = UrlFetchApp.fetch(imageUrl).getBlob();
          body.insertImage(startIndex, imgBlob);

          // Reset index to correctly continue loop
          i = startIndex - 1;
          insideEquation = false;
          equationLines = [];
        } else {
          // Append paragraph whole text preserving line breaks
          equationLines.push(text);
        }
      }
    }
  }
}

function renderLatexToImage(latex) {
  var encoded = encodeURIComponent(latex);
  return 'https://latex.codecogs.com/png.latex?' + encoded;
}
