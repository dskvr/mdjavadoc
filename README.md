Markdown Javadoc is a script that generates markdown javadocs primarily for use in Jekyll and GitHub Pages. It consists of two modules, an [API](./api/README.md) and [CLI](./cli/README.md). If you simply want to generate a set of javadocs in markdown without any scripting, the CLI provides a simple interface with a decent amount of options. If you have a more complex use case, however, it might be more beneficial to look into the API first.

## Installation

These are generic installation instructions that are fairly similar for both the API and CLI. 


### From Source

```shell
git clone https://github.com/dskvr/mdjavadoc
cd mdjavadoc/cli
npm install
sudo npm link
```

For specific usage instructions, see the README for the [API](./api/README.md) or [CLI](./cli/README.md) components.

## Functionality

The program works by searching a set of files for [javadoc comments](https://www.oracle.com/technetwork/java/javase/documentation/index-137868.html), parsing them into a data structure containing the description, tags, and metadata, and then outputting that data into a set of markdown files. For example, a file containing a javadoc comment like the one below would yield the following structure and output...

##### Javadoc

```java
/**
 * This is a method which does a thing with something and stuff.
 * 
 * @param something		This is something.
 * @param stuff			This is a bunch of stuff.
 * @return			A thing.
 */
public static Object doTheThing(int something, String[] stuff) {
	return null;
}
```

##### Data

```javascript
[
  {
    name: "doTheThing",
    description: "This is a method which does a thing with something and stuff.",
    type: ["public", "static", "void"],
    source: "/package/structure/ClassName.java#L2",
    param: [
      {
        content: "@param something\tThis is something.",
        template: ["Parameter Name", "Description"],
        values: ["something", "This is something."]
      },
      {
        content: "@param stuff\t\tThis is a bunch of stuff.",
        template: ["Parameter Name", "Description"],
        values: ["stuff", "This is a bunch of stuff."]
      }
    ],
    return: [
      {
        content: "@return\t\tA thing.",
        template: ["Returned Value"],
        values: ["A thing."]
      }
    ]
  }
]
```

##### Markdown

```md
## [doTheThing](../blob/master/package/structure/ClassName.java#L2)

**Type:** `public` `static` `void`

This is a method which does a thing with something and stuff.

|Parameter Name|Description|
|-----|-----|
|something|This is something.|
|stuff|This is a bunch of stuff.|

**Returned Value:** A thing.
```

## Contributing

Contributions are accepted. See this project's [CONTRIBUTING.md](./.github/CONTRIBUTING.md) for instructions on how to contribute to this project.
