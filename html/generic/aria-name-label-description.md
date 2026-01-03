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
</dialog>
```
The dialog was labelledby using its main heading.
#### Example with two ids
```
<article>
<h2> id="article-title">About improving accessibility</h2>
<p>…</p>
<a id="article-link" href="…" aria-labelledby="article-link article-title">Continue reading</a>
</article>
```
In the example above we have an article with a title, followed by a potentially long paragraph, followed by the "Continue reading" link. Sighted users can quickly see that "Continue reading" is visually placed under "Improving accessbility". In case of a long paragraph, screen reader users may get lost and it might be hard to figure out the relationship between "Contnue reading" and the title.
The `aria-labelledby` value references id of both elements, the link text itself and the title. The name of the link is: "Continue reading About improving accessibility".

#### Concerns
The example above can raise a few questions.

##### 1. `aria-labelledby` references itself. Won't it create infinite loop?
No, each node is referenced only one, to [prevent infinite loops](https://www.w3.org/TR/accname-1.1/#:~:text=accumulated%20text.-,Important,-%3A%20Each%20node%20in).

##### 2. Does the order of ids matter?
Yes, the name is concatenated using the order provided.

##### 3. Can I use more ids?
Yes, it's possible to reference more ids.

### aria-label
The `aria-label` attribute value matches the literal string which will become a name.
#### Example ###
```
<button style="background-image: url("arrow.svg");" aria-label="Back"></button>
```
