# `aria-labelledby`, `aria-label`, `aria-describedby`, `aria-description`

Attributes: `aria-labelledby`, `aria-label`, `aria-describedby`, `aria-description` are often used randomly and interchangably, without a consideration about their purpose.

## Name vs description
Two of the attributes are intended to provide a [name](<../accessibility tree/name.md>) (`aria-labelledby`, `aria-label`) and the remaining two provide a [description](<../accessibility tree/description.md>) (`aria-describedby`, `aria-description`).

Read more about [the difference between name and description](<../accessibility tree/name-description.md>).

## Name: `aria-labelledby`, `aria-label`
While both attributes are intended to provide a name, they work in a different way.

### `aria-labelledby`
The `aria-labelledby` value must be an id, or a list of ids referencing existing HTML tags. It's similar to the `<label>` tag, as it's also used to name an element by using another element.
Ids must be unique, as otherwise only the first element with given id is referenced.

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

## Description: `aria-describedby`, `aria-description`
`aria-describedby`and `aria-description` are equivalents of `aria-labelledby` and `aria-label`, but for a description.

### `aria-describedby`
As `aria-labelledby`, the `aria-describedby` attribute references id or ids of other elements. Descriptions do not ovewrite the name, they are added to the name.
```
<button aria-describedby="info">Save</button>
<span id="info">Files are saved in the cloud.</span>
```
In the example above, the button's name will be "Save", and description will be: "Files are saved in the cloud." A screen reader announcements will be like: "Save button, Files are saved in the cloud."

```
<label for="new-password>New password</label>
<input type="password" id="new-password" aria-describedby="info1 info2 info3">
<span id="info1">Password needs to have at least 16 characters.</span>
<span id="info2">Previous passwords cannot be reused.</span>
<span id="info3">Use at least one upper case letter.</span>
```
In the example above the `<input>` has a "New password" name, and the description is: "Password needs to have at least 16 characters. Previous passwords cannot be reused. Use at least one upper case letter."

#### Concerns
Concerns resolved in the `aria-labelledby` section apply for the `aria-describedby`. Just replace `aria-labelledby` with `aria-describedby` and "Name" with "Description".

### `aria-description`
The `aria-description` is part of the draft documents. It's mentioned in the [Accessible Name and Description Computation 1.1 (W3C recommendation)](https://www.w3.org/TR/accname-1.1/#mapping_additional_nd_description) and [Accessible Rich Internet Applications (WAI-ARIA) 1.3](https://www.w3.org/TR/wai-aria-1.3/) - both of them are still not finalized recommendations, and `aria-description` is not referenced in the current recommendations.

#### Reality
On the other hand the current browser implementation is far from being a draft. Chrome (desktop and mobile), Safari (desktop and mobile), Firefox - all of them support `aria-description`. When it comes to screen reader support, nothing new is needed from their side. The `aria-description` populates the description field, the same field as `aria-describedby`. As a result the support of `aria-description` is the same as for `aria-describedby`.

#### Should it be used?
The only risk of using `aria-description` at the moment is that it will be removed from the draft documents. The risk of such a case seems to be very low.

#### Example
```
<button aria-description="Closes upload dialog">Close</button>
```
In the example above the `<button>` has "Close" name, and the description is: "Closes upload dialog". A screen reader announcements will be like: "Close button. Closes upload dialog".
#### Concerns
Concerns resolved in the `aria-label` section apply for the `aria-description`. Just replace `aria-labelledby` with `aria-describedby`, `aria-label` with `aria-description` and "Name" with "Description".

## Combine the four in one tag
The rules described in sections above indirectly provide information about what will happen with different combination, but it's easier to show it as examples.

<table>
  <tr>
  <th scope="col">Snippet</th><th scope="col">aria-labelledby</th><th scope="col">aria-label</th><th scope="col">aria-describedby</th><th scope="col">aria-description</th><th scope="col">Name</th><th scope="col">Description</th><th scope="col">Comment</th>
  </tr>
  <tr>
    <td>&lt;button id="b"<br>
      aria-label="Save image"<br>
      aria-labelledby="n"<br>
      aria-description="Files cannot be downloaded"<br>
      aria-describedby="d"&gt;<br>
      Save<br>
      &lt;/button&gt;<br><br>
      &lt;span id="n"&gt;Save file&lt;/span&gt;<br><br>
      &lt;span id="d"&gt;Files are saved in the cloud&lt;/span&gt;
    </td>
    <td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Save file</td><td>Files are saved in cloud</td><td><ul><li>aria-label is ignored as aria-labelledby has precedence</li><li>aria-description is ignored as aria-describedby has precedence.</li></ul></td>
  </tr>
  <tr>
    <td>&lt;button id="b"<br>
      aria-label="Save image"<br>
      aria-labelledby="nn"<br>
      aria-description="Files cannot be downloaded"<br>
      aria-describedby="d"&gt;<br>
      Save<br>
      &lt;/button&gt;<br><br>
      &lt;span id="n"&gt;Save file&lt;/span&gt;<br><br>
      &lt;span id="d"&gt;Files are saved in the cloud&lt;/span&gt;
    </td>
    <td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Save image</td><td>Files are saved in cloud</td><td><ul><li>aria-label is used as aria-labelledby references not existing id</li><li>aria-description is ignored as aria-describedby has precedence.</li></ul></td>
  </tr>
  <tr>
    <td>&lt;button id="b"<br>
      aria-label="Save image"<br>
      aria-labelledby="n"<br>
      aria-description="Files cannot be downloaded"<br>
      aria-describedby=""&gt;<br>
      Save<br>
      &lt;/button&gt;<br><br>
      &lt;span id="n"&gt;Save file&lt;/span&gt;<br><br>
      &lt;span id="d"&gt;Files are saved in the cloud&lt;/span&gt;
    </td>
    <td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Save file</td><td>Files cannot be downloaded</td><td><ul><li>aria-label is ignored as aria-labelledby has precedence</li><li>aria-description is used as aria-describedby doesn't reference any id</li></ul></td>
  </tr>
  <tr>
    <td>&lt;button id="b"<br>
      aria-description="Files cannot be downloaded"<br>
      Save<br>
      &lt;/button&gt;<br><br>
      &lt;span id="n"&gt;Save file&lt;/span&gt;<br><br>
      &lt;span id="d"&gt;Files are saved in the cloud&lt;/span&gt;
    </td>
    <td>No</td><td>No</td><td>No</td><td>Yes</td><td>Save</td><td>Files cannot be downloaded</td><td><ul><li>Name is created from content</li><li>aria-description is used as aria-describedby is not present</li></ul></td>
  </tr>
  <tr>
    <td>&lt;button id="b"<br>
      aria-description="Files cannot be downloaded"<br>      
      &lt;/button&gt;<br><br>
      &lt;span id="n"&gt;Save file&lt;/span&gt;<br><br>
      &lt;span id="d"&gt;Files are saved in the cloud&lt;/span&gt;
    </td>
    <td>No</td><td>No</td><td>No</td><td>Yes</td><td>&lt;Empty&gt;</td><td>Files cannot be downloaded</td><td><ul><li>The button has no name, as there are no name candidates</li><li>aria-description is used as aria-describedby is not present</li><li>Screen reader output will be like: "Unlabled button. Files cannot be downloaded"</li></ul></td>
  </tr>
</table>
