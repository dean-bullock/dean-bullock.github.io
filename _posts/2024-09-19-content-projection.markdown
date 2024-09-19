---
layout: post
title:  "Content projection"
date:   2024-09-19 12:31:00 +0100
categories: angular patterns
---

**Understanding Content Projection in Angular**

Content projection is a powerful feature in Angular that allows developers to create highly reusable and flexible components by projecting content from the parent component into a child component. It’s a fundamental concept that empowers component-based architecture, ensuring that Angular applications can maintain clean and scalable code.

### What is Content Projection?

Content projection enables a parent component to pass HTML or template content into a child component, which can then display this content in specific locations within its template. This is done using Angular’s `<ng-content>` directive.

### Basic Example

Let’s say you have a `CardComponent` where you want to display different content inside the card from various places in your application. You don’t need to hardcode the content inside the card. Instead, you allow the parent components to pass in the content dynamically:

```html
<!-- card.component.html -->
<div class="card">
  <ng-content></ng-content>
</div>
```

Now, in the parent component, you can use the `CardComponent` like this:

```html
<app-card>
  <h2>Title</h2>
  <p>This is some projected content inside the card.</p>
</app-card>
```

Here, the `<ng-content>` directive acts as a placeholder for the content passed from the parent component, enabling flexible and reusable layouts.

### Multi-Slot Content Projection

In more complex scenarios, you might want to project content into multiple predefined slots. Angular allows you to do this by specifying selectors within multiple `<ng-content>` tags. Here’s an example:

```html
<!-- card.component.html -->
<div class="card">
  <header>
    <ng-content select="[card-title]"></ng-content>
  </header>
  <div class="content">
    <ng-content></ng-content>
  </div>
</div>
```

In the parent component, you can now specify which content goes into each slot:

```html
<app-card>
  <h2 card-title>Card Title</h2>
  <p>This is the main content of the card.</p>
</app-card>
```

Here, the content with the `card-title` attribute is projected into the header section, while the rest is projected into the body.

### Benefits of Content Projection

1. **Reusability:** Content projection promotes component reusability, allowing components to remain flexible and adaptable to various use cases.
2. **Separation of Concerns:** It separates the logic of a component from its presentation, leading to cleaner and more maintainable code.
3. **Customization:** Parent components can customize child components’ content without needing to modify the child component’s template directly.

### Conclusion

Content projection in Angular is a key tool for developers aiming to build reusable, flexible components that can adapt to different content requirements. Whether you're working with simple single-slot projection or more advanced multi-slot scenarios, mastering content projection will improve the flexibility and scalability of your Angular applications.