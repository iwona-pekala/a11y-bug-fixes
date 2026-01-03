# `aria-labelledby`, `aria-label`, `aria-describedby`, `aria-description`

Attributes: `aria-labelledby`, `aria-label`, `aria-describedby`, `aria-description` are often used randomly and interchangably, without a consideration about their purpose.

## Name vs description
Two of the attributes are intended to provide a [name](<../accessibility tree/name.md>) (`aria-labelledby`, `aria-label`) and the remaining two provide a [description](<../accessibility tree/description.md>) (`aria-describedby`, `aria-description`).

Read more about [the difference between name and description](<../accessibility tree/name-description.md>).

## Name: `aria-labelledby`, `aria-label`
While both attributes are intended to provide a name, they work in a different way.

### `aria-labelledby`
The `aria-labelledby` value must be an id, or a list of ids referencing existing HTML tags. It's similar to the `<label>` tag, as it's also used to name an element by using another element.
Ids must be unique, as otherwise

#### Example with one id
```
<dialog aria-labelledby="dialog-title">
<h2 id="dialog-title">Add address</h2>
…
</dialog>
```
The dialog was labelledby using its main heading.
#### Example with two ids
```
<article>
<h2> id="article-title">About accessibility</h2>
<p>…</p>
<a id="article-link" href="…" aria-labelledby="article-link article-title">Continue reading</a>
</article>
```
In the example above we have an article with a title, followed by a potentially long paragraph, followed by the "Continue reading" link. Sighted users can quickly see that "Continue reading" is visually placed under "Improving accessbility". In case of a long paragraph, screen reader users may get lost and it might be hard to figure out the relationship between "Contnue reading" and the title.
The `aria-labelledby` value references id of both elements, the link text itself and the title. The name of the link is: "Continue reading About accessibility".

#### Concerns
Examples above can raise a few questions.

##### 1. `aria-labelledby` references itself. Won't it create infinite loop?
No, each node is referenced only one, to [prevent infinite loops](https://www.w3.org/TR/accname-1.1/#:~:text=accumulated%20text.-,Important,-%3A%20Each%20node%20in).

##### 2. Does the order of ids matter?
Yes, the name is concatenated using the order provided.

##### 3. Can I use more than two ids?
Yes, it's possible to reference more ids.

##### 4. What happens when the id doesn't exist?
The `aria-labelledby' attribute will be ignored and there will be an attempt to [compute the name](name.md#name-computation-rules) using different methods.
```
<!-- There is a typo in the id referenced in aria-labelledby, the dialog will remain without a name -->
<dialog aria-labelledby="dialog-titel">
<h2 id="dialog-title"></h2>
…
</dialog>
```

##### 5. What happens when there are duplicate ids?
Only the first DOM element with the given id will be used for name computation.
```
<article>
<h2> id="article-title">About accessibility</h2>
<p>…</p>
<a id="article-link" href="…" aria-labelledby="article-link article-title">Continue reading</a>
</article>

<article>
<h2> id="article-title">About usability</h2>
<p>…</p>
<a id="article-link" href="…" aria-labelledby="article-link article-title">Start reading</a>
</article>

<!-- Both links names will be: "Continue reading About accessibility -->
```
### `aria-label`
The `aria-label` attribute value matches the literal string which will become a name.
#### Example ###
```
<button style="background-image: url("arrow.svg");" aria-label="Back"></button>
```
In the example above "Back" becomes a literal name of the button.

#### Concerns
##### 1. What happens if `aria-label` is empty?
It's ignored during name computation, and the [name computation](name.md#name-computation-rules) will be computed using different methods.

### `aria-labelledby` vs `aria-label`
Having two attributes to pick from, there might another set of questions about which and how to use it.

#### 1. Should I use `aria-labelledby` or `aria-label`?
If there is an external element which acts as a visible label, use `aria-labelledby`. Otherwise use `aria-label`.

#### 2. Can I use `aria-labelledby` and `aria-label` for the same tag?
Technically yes, but it probably won't result in the outcome that was expected. If both valid `aria-labelledby` and `aria-label` are present, only `aria-labelledby` is used in [name computation](name.md#name-computation-rules), and `aria-label` is ignored.
