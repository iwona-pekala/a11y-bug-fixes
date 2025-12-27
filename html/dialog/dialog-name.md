# Dialog name

## Code
A dialog **must** have an implicit name. A name can be added via aria-label ***or*** aria-labelledby attributes. 

## aria-label
The aria-label content is a literal string that will be read by screen readers.

**aria-label examples:**

`<div role="dialog" aria-label="Upload files">…</div>`

`<dialog aria-label="Upload files">…</dialog>`

## aria-labelledby
The aria-labelledby content is the list of ids of existing HTML tags. In the most common case one is referenced.

**aria-labelledby examples:**

```
<div role="dialog" aria-labelledby="dialog_heading">
  <h2 id="dialog_heading">Upload files</h2>
…
</div>
```

```
<dialog aria-labelledby="dialog_heading">
  <h2 id="dialog_heading">Upload files</h2>
…
</dialog>
```


