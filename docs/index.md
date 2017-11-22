# Embedding draw.io diagrams to mkdocs

Recently I wanted to include draw.io diagrams to our documentation in such way that that the diagrams would be versioned within the repository. 

This is just simple demo to to show they can be embedded with the viewer.

## Usage

Create a `div` element with `data-mxgraph-path` attribute pointing to your digram file.

```html
    <div class="dynamic-graph" data-mxgraph-path="example.xml"></div>
```

## Implementation

The [footer file](https://github.com/sakumikko/mkdocs-drawio/blob/master/theme/partials/footer.html) has been overwritten with a simple script additions that will pick up all div elements with the attribute, fetch the associated diagram xml and then invoke `GraphViewer` to render the diagram.

```html
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
  <script>
      var graphJson = { 
          "highlight":"#0000ff",
          "nav":true,
          "resize":true,
          "toolbar": "zoom layers lightbox" 
          }
      window.onDrawioViewerLoad = function() {
          $("div[data-mxgraph-path]").each(function(index, element){
              fetch($(element).data("mxgraph-path"))
              .then(function(response){
                  return response.text()
              })
              .then(function(text){
                  var jsonText = JSON.stringify(
                      Object.assign({}, graphJson, {xml: text})
                      )
                  element.setAttribute("data-mxgraph", jsonText) 
                  GraphViewer.createViewerForElement(element)
              })
          })
      }
  </script>
  <script src="https://www.draw.io/js/viewer.min.js">
  </script>

```

## An example diagram embedded
<div class="dynamic-graph" data-mxgraph-path="example.xml"></div>


