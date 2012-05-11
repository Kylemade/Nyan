# Nyan #

Nyan is an ExpressionEninge plug-in that displays a list of categories in a tag cloud format, where each category is assigned a CSS class based on its popularity.

## Installation

* Copy the `nyan` folder to your `/system/expressionengine/third_party/` directory.

## Parameters

<table>
<tr>
	<th>Parameter</th>
	<th>Type</th>
	<th>Default</th>
	<th>Description</th>
	<th>Required</th>
</tr>
<tr>
	<td>cat_id</td>
	<td>string</td>
	<td></td>
	<td>Comma or pipe delimited string of category group ids.</td>
	<td>Yes</td>
</tr>
<tr>
	<td>css_class</td>
	<td>string</td>
	<td></td>
	<td>Class(es) for the outermost list container.</td>
	<td></td>
</tr>
<tr>
	<td>css_id</td>
	<td>string</td>
	<td></td>
	<td>ID for the outermost list container.</td>
	<td></td>
</tr>
<tr>
	<td>debug</td>
	<td>yes|no</td>
	<td>no</td>
	<td>Set to "yes" to enable debugging.</td>
	<td></td>
</tr>
<tr>
	<td>limit</td>
	<td>int</td>
	<td>0</td>
	<td>Maximum number of categories to show.</td>
	<td></td>
</tr>
<tr>
	<td>min_count</td>
	<td>int</td>
	<td>0</td>
	<td>Minimum number of entries a category should have to appear in the results.</td>
	<td></td>
</tr>
<tr>
	<td>limit</td>
	<td>abc|pop</td>
	<td>pop</td>
	<td>Set to 'abc' for alphabetical or 'pop' for popularity.</td>
	<td></td>
</tr>
<tr>
	<td>scale</td>
	<td>string</td>
	<td>'not-popular, mildly-popular, popular, very-popular, super-popular'</td>
	<td>Comma or pipe delimited string of classes ordered from least to most popular.</td>
	<td></td>
</tr>
<tr>
	<td>sort</td>
	<td>asc|desc</td>
	<td>desc</td>
	<td>Set to "asc" or "desc" (optional, default is 'desc'.</td>
	<td></td>
</tr>
</table>

## Single Variables

<table>
<tr>
	<th>Variable</th>
	<th>Description</th>
</tr>
<tr>
	<td>{cat_id}</td>
	<td>The ID of the category.</td>
</tr>
<tr>
	<td>{cat_name}</td>
	<td>The name of the category.</td>
</tr>
<tr>
	<td>{cat_url_title}</td>
	<td>The URL title of the category.</td>
</tr>
<tr>
	<td>{cat_entry_count}</td>
	<td>The number of entries the category is used in.</td>
</tr>
<tr>
	<td>{cat_weight}</td>
	<td>The CSS class assigned to the category as measured by its popularity.</td>
</tr>
<tr>
	<td>{parent_id}</td>
	<td>The parent ID for the category.</td>
</tr>
</table>

## Additional Single Variables

<table>
<tr>
	<th>Variable</th>
	<th>Description</th>
</tr>
<tr>
	<td>{count}</td>
	<td>The count out of the current category.</td>
</tr>
<tr>
	<td>{no_results}</td>
	<td>Conditional (e.g. {if no_results}No Results!{/if}) for displaying a message when no data is returned.</td>
</tr>
<tr>
	<td>{switch=''}</td>
	<td>Rotates through any number of pipe delimited values.</td>
</tr>
<tr>
	<td>{total_results}</td>
	<td>The total amount of categories returned.</td>
</tr>
</table>

## Examples

### Basic usage

	{exp:nyan cat_id="1"}
	<li class="{cat_weight}">{cat_name} ({cat_entry_count})</li>
	{/exp:nyan}

### Multiple categories

	{exp:nyan cat_id="1|2|3"}
	<li class="{cat_weight}">{cat_name} ({cat_entry_count})</li>
	{/exp:nyan}

### Custom classes for category weight

	{exp:nyan cat_id="1" scale="not-popular, popular, very-popular"}
	<li class="{cat_weight}">{cat_name} ({cat_entry_count})</li>
	{/exp:nyan}

### Limit categories by popularity

This example will only return categories that are used by 2 or more entires.

	{exp:nyan cat_id="1" min_count="2"}
	<li class="{cat_weight}">{cat_name} ({cat_entry_count})</li>
	{/exp:nyan}

### Additional tags example

	{exp:nyan cat_id="1" css_id="my-id" css_class="my-class"}
	<li class="{cat_weight} {switch='odd meow|even meow-meow'}">
		<a href="category/{cat_url_title}">{count} of {total_results}: {cat_name} ({cat_entry_count})</a>
		{if no_results}Sorry, no results.{/if}
	</li>
	{/exp:nyan}

## Change Log

### v1.0.0

* Initial release