---
title: MutationRecord.nextSibling
slug: Web/API/MutationRecord/nextSibling
page-type: web-api-instance-property
tags:
  - nextSibling
  - MutationRecord
  - Property
  - Reference
browser-compat: api.MutationRecord.nextSibling
---

{{APIRef("DOM")}}

The {{domxref("MutationRecord")}} read-only property **`nextSibling`** is the next sibling of an added or removed child node of the [`target`](/en-US/docs/Web/API/MutationRecord/target) of a {{domxref("MutationObserver")}}.

## Value

If a node is added to or removed from the [`target`](/en-US/docs/Web/API/MutationRecord/target) of a {{domxref("MutationObserver")}}, the value is the {{domxref("Node")}} that is the next sibling of the added or removed node: that is, the node immediately following this one in the parent's {{domxref("Node.childNodes", "childNodes")}} list.

The value is `null` if there are no added or removed nodes, or if the node is the last child of its parent.

## Examples

### Log the next sibling of a mutation

This adds a node every time you click the button, but it adds the node at the _start of the target_, not the end. Then the observer logs the `textContent` of the `nextSibling` of the added node. The first time this is `null` because the target didn't have any children to begin with (so now it has only the most recently added node), but after this it logs the node after (the `nextSibling` of) the one we just added.

#### HTML

```html
<button id="add-nodes">Add a node</button>
<button id="reset">Reset</button>

<pre id="log" class="log">Next sibling of added node:</pre>
<pre id="counter" class="log">Node count: 0</pre>
<div id="target"></div>
```

```css hidden
.log {
  border: 1px dotted black;
  padding: .5rem;
}
```

#### JavaScript

```js
const addNodes = document.querySelector("#add-nodes");
const reset = document.querySelector("#reset");
const counter = document.querySelector("#counter");
const target = document.querySelector("#target");
let nodeNumber = 1;

addNodes.addEventListener("click", () => {
  const newPara = document.createElement("p");
  newPara.textContent = `Node #${nodeNumber}`;
  nodeNumber++;
  target.insertBefore(newPara, target.firstChild);
});

reset.addEventListener("click", () => self.location.reload());

function logNextSibling(records) {
  for (const record of records) {
    if (record.type === "childList") {
      for (const newNode of record.addedNodes) {
        counter.textContent = `Node count: ${target.children.length}`;
        log.textContent = `Next sibling of added node: ${record.nextSibling?.textContent}`
      }
    }
  }
}

const observer = new MutationObserver(logNextSibling);
observer.observe(target, {childList: true});
```

#### Result

{{EmbedLiveSample("Log the next sibling of a mutation", "", 250)}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}
