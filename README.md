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

# Generating a page from a template

Under the hood, the class you care about is ClayTemplate, this is the class that allows you to generate a nice piece of output from a template.
To get an instance of ClayTemplate, you use the builder class, ClayTemplateBuilder, which has a builder pattern to it's use.

First off, you want to start up a builder by calling the static function **newBuilder** in ClayTemplate.
```
ClayTemplate::newBuilder()
```

Now you set the file path of the template you want to use using **setTemplateFilePath(path)**

```
ClayTemplate::newBuilder()
->setTemplateFilePath('path/to/my/template.clay.html')
```

Next you add the properties to use during generation and their values via **addProperty(name, value)**

```
ClayTemplate::newBuilder()
->setTemplateFilePath('path/to/my/template.clay.html')
->addProperty('foo', 'bar')
->addProperty('userName', 'Mark')
```

Once this is done you can use **build()** to get your instance of ClayTemplate.

```
ClayTemplate::newBuilder()
->setTemplateFilePath('path/to/my/template.clay.html')
->addProperty('foo', 'bar')
->addProperty('userName', 'Mark')
->build()
```

A ClayTemplate instance only has one publically accesible function, **toString()**, this will return as a string the output from your template with the properties you specified in the builder.

Here's an example that ties all of this together and simply outputs the finished result to the user immedietally:
```
echo ClayTemplate::newBuilder()
->setTemplateFilePath('path/to/my/template.clay.html')
->addProperty('foo', 'bar')
->addProperty('userName', 'Mark')
->build()
->toString();
```
