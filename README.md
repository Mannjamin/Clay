# Clay
A library for creating templates for use in PHP web applications.

Clay templates make dynamic content being served to a user in PHP just a whole lot easier, instead of having a messy page with php tags all over the place, you use clay tags to mark out where you need things to be.
These are the currently supported Clay tags.

### {{echo}}
> Syntax: {{echo propertyOrString}}

A very simple tag that simply outputs the given value in its place, if a property is used it will output the value of that property (or null if not set), for example:
```
Hi there, {{echo property.userName}}!
```

### {{if}} and {{/if}}
> Syntax: {{if property condition}} {{/if}}

These two tags are used together to determine whether part of a page should be outputted or not, you can use this to filter out parts of your page that you only want shown in certain circumstances. Here's an example of a greeting that only appears if the userName property is set:
```
{{if property.userName isNotNull}}
  Hi there, {{echo property.userName}}!
{{/if}}
```

### {{include}}
> Syntax: {{include pathToFile}}

You can use this tag to import other files or even other clay templates into the current template. (I use this extensively in my web application) for example:
```
<style type='text/css'>
{{include path/to/css/fonts.clay.css}}
{{include path/to/css/homepage.clay.css}}
</style>
```

### {{signature}}
> Syntax: {{signature typeOfFile}}

Inserts a small signature indicating the page was generated with clay, supports typeOfFile being html, css or js.
