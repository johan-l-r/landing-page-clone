# Landing Page Clone
As the title suggests, this project is a clone of a [landing page design](https://www.figma.com/site/zLvikKTisugthSaY9KmDaN/Friendly-Accounting-Services--Community-?node-id=0-1&p=f&t=zlt33i7HGSYKMlbB-0) that I found online.

## Why does this project exists? 
The answer may seem obvious, but if I want to become a frontend developer, one of the most fundamental skills I need is the ability to take a Figma design and turn it into a real, responsive web page.

This project is an opportunity to practice that workflow while improving my HTML and CSS skills.

## What do I expect to learn 
One of the biggest challenges I face when building web pages is making them responsive. The goal is not to create separate CSS files for desktop, tablet, and mobile (although some companies still follow that approach). Instead, I want to learn how to build layouts that naturally adapt to different screen sizes using responsive design techniques.

By completing this project, I hope to improve my understanding of:
- Responsive layouts with Flexbox and CSS Grid.
- Writing scalable and maintainable CSS.
- Translating a Figma design into clean HTML and CSS.
- Building components that adapt to different viewport sizes without duplicating styles.

## AI usage 
I believe it's important to include a section like this because AI is here to stay. As developers, we shouldn't fear or reject it; instead, we should learn how to use it responsibly to improve the way we work.

Since I'm still learning, I use AI as if it were a senior developer reviewing my code. Rather than asking it to write features for me, I use it to identify weaknesses in my implementation, explain best practices, recommend learning resources, and point out design decisions that could become problems as the project grows.

A great example of this can be seen in the next section.

A great example of this will be expalined in the next section.

## Mobile version finished (07/15/2026)
I've finished the mobile version of the landing page, and the next logical step is implementing the tablet and desktop layouts.

However, as I started thinking about the responsive version, I realized that my current CSS architecture would force me to rewrite a large portion of my existing rules inside media queries. That wasn't just because responsive design is challenging—it was a sign that my code wasn't structured to scale.

This is where AI became an excellent learning tool.

After reviewing my codebase, it distinguished between things that were simply "good enough" for a beginner and design decisions that would become maintainability issues as the project grew. Instead of rewriting my code for me, it explained _why_ certain patterns were problematic and suggested better alternatives.

The most valuable pieces of feedback were:

- **Overuse of decentant selectors**: Reusable components should be independent of where they're placed. If a button needs different styles depending on the section it's belongs to, then it isn't truly reusable.
	```css
	.services .button { ... }
	.experts .button { ... }
	
	...
	
	.button, 
	.button--alt { ... }
	.button { ... }
	.button--alt { ... }

	```
	The same button component appears in multiple sections of the page. Rather than styling it based on its parent container, it's better to create component variants (`.button--alt`, for example) that clearly describe the visual differences while keeping the component reusable.
- **Components having page knowledge**: A component's responsibility is to define its own appearance and behavior—not its position within the page.

	For example, a button shouldn't decide how much space exists between itself and the paragraph above it. That spacing belongs to the layout or section that contains the button.
	```css
	.button, 
	.button--alt {
	  margin-block-start: var(--lg-spacing);
	}
	```
	Removing layout-related spacing from reusable components makes them much easier to reuse in different contexts without unexpected side effects.
- **Better variables**:  CSS variables are most valuable when their names describe their purpose rather than their size.

	My original naming convention looked like this:
	```css
	:root {
		...
		
	  --xs-fs: 0.75rem;
	  --sm-fs: 1rem;
	  
		...
		
	  --lg-spacing: 2.5rem;
	}
	```
	While this works, names like `--sm-fs` or `--lg-spacing` don't communicate _where_ or _why_ they're used. A more semantic naming convention makes the stylesheet easier to read and maintain, especially as the project grows.
