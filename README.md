## Statamic add-on modifiers : excerpt and all

### Description

This is a pair of super-simple statamic modifiers (filters) that allow the creation of excerpts from the content of a page or post, without having to define a content variable that contains redundant information.

These two modifiers work by using a defined 'excerpt-termination' character string.  

The first modifier is *excerpt*. This modifier allows the user to insert the pre-defined character string in any content area (the stuff below the YAML front matter) that will mark the end of the content to be displayed in excerpts. This is more flexible than the truncate modifier since its position can vary depending on the content and is not fixed to a specific number of characters. The excerpt can therefore end at a sensible position in the content.

The second modifier is *all*. This modifer is used in conjuction with the *excerpt* modifier to strip out the predefined character string from the content area and return it *sans* string. If the character string is not present, it does nothing.

### Installation

Drop the folders *all* and *excerpt* in the add-ons folder in your Statamic project. Inside each folder is the modifier .php file. 

Both files contain constants that define the string to be used in the content area to define the end of the excerpt portion of the content. Right now, this string is ```'[->]'```. This can be changed to whatever string you want. For instance, if you like brevity ```'&>'``` could be used. Whatever you want to use is fine, as long as this string is **the same** in both mod.all.php and mod.excerpt.php. 

Another constant that can be changed in the mod.excerpt.php file is the continuation string. Right now this string is set to display a right arrow ```'&rArr;'``` after the excerpt. It can be set to ellipsis ```'&hellip;'``` or even an empty string.

### Usage

#### Use inside the content area

When adding content, the pre-defined 'excerpt-termination' string is used to mark the point where the content is to be truncated for use as an excerpt.

So a blog posting might look like this with the default 'excerpt-termination' string:

```
---
title: A sample post
categories:
  - trivia
  - grammar
---
Lorem ipsum dolor sit amet, consectetur adipisicing elit. Porro, maiores, doloribus, eius saepe cupiditate mollitia facere repellendus odio nihil aperiam enim fugiat ducimus hic.[->] Repellat, quam praesentium illo incidunt reprehenderit?

Lorem ipsum dolor sit amet, consectetur adipisicing elit. Quibusdam, ad, magni, rem, ullam assumenda fugiat quaerat laudantium error sit saepe dolore voluptatem soluta voluptas. Doloremque et harum corporis officia iste!
```
And the content would be terminated right after 'ducimus hic.' whenever it is passed through the *excerpt* modifier.


#### Use inside a template

The main use of this modifier add-on is to truncate content that is displayed in listings such as a blog or journal. The excerpt modifier is essentially a filter, so a super-simple blog listing template might look like this:

```
<li >
	<h1>
		{{ title }}
	</h1>
	<p>
		posted on {{ date }}
	</p>
	
	{{ content|excerpt }}
</li>
```

Naturally, an issue is that when you want to display the entire content area, that pesky 'excerpt-termination' string is still there. So any time you need to display all the content, simply pass the content through the *all* modifier, which will strip out the string if it is present.

A typical whole-content template might look like this:

```
<article >
	<h1>{{ title}}</h1>
	<p>
		Recorded on {{ date }}
	</p>
	{{ content|all }}
</article>
```

### Homework exercise

This is obviously stupid simple stuff using existing php string functions. Someone more industrious and clever than myself can take this idea and put some more logic in this set of add-ons that would allow an excerpt region of the content to be defined and extracted.





