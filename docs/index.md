# Embedding draw.io diagrams to mkdocs

Recently I wanted to include draw.io diagrams to our documentation in such way that that the diagrams would be versioned within the repository. 

This is just simple demo to to show they can be embedded with the viewer.

## Usage

Create a `div` element with `data-mxgraph-path` attribute pointing to your digram file.

```html
    <div class="dynamic-graph" data-mxgraph-path="example.xml"></div>
```

## Implementation

The footer file has been overwritten fith a simple script additions that will pick up all div elements with the attribute, fetch the associated diagram xml and then invoke `GraphViewer` to render the diagram.

## An example diagram embedded
<div class="dynamic-graph" data-mxgraph-path="example.xml"></div>


