### Table of Contents

| No. | Questions |
|---- | ---------
|1| [What are different types of compilation in Angular?](#what-are-different-types-of-compilation-in-angular)|
|2| [What is JIT?](#what-is-jit)|
|3| [What is AOT?](#what-is-aot)|
|4| [Why do we need compilation process?](#why-do-we-need-compilation-process)|
|5| [What are the advantages with AOT?](#what-are-the-advantages-with-aot)|
|6| [What are the ways to control AOT compilation?](#what-are-the-ways-to-control-aot-compilation)|
|8| [What are the three phases of AOT?](#what-are-the-three-phases-of-aot)|
|9| [Can I use arrow functions in AOT?](#can-i-use-arrow-functions-in-aot)|
|10| [What is the purpose of metadata json files?](#what-is-the-purpose-of-metadata-json-files)|
|11| [Can I use any javascript feature for expression syntax in AOT?](#can-i-use-any-javascript-feature-for-expression-syntax-in-aot)|
|12| [What is AOT compiler??](#what-is-aot-compiler)|

1. ### What are different types of compilation in Angular?
    Angular offers two ways to compile your application,
    1. Just-in-Time (JIT)
    2. Ahead-of-Time (AOT)

  **[⬆ Back to Top](#table-of-contents)**

2. ### What is JIT?
    Just-in-Time (JIT) is a type of compilation that compiles your app in the browser at runtime. JIT compilation was the default until Angular 8, now default is AOT. When you run the ng build (build only) or ng serve (build and serve locally) CLI commands, the type of compilation (JIT or AOT) depends on the value of the aot property in your build configuration specified in angular.json. By default, aot is set to true.

  **[⬆ Back to Top](#table-of-contents)**

3. ### What is AOT?
    Ahead-of-Time (AOT) is a type of compilation that compiles your app at build time. This is the default starting in Angular 9. When you run the ng build (build only) or ng serve (build and serve locally) CLI commands, the type of compilation (JIT or AOT) depends on the value of the aot property in your build configuration specified in angular.json. By default, aot is set to true.
    
    ```cmd
    ng build
    ng serve
    ```

  **[⬆ Back to Top](#table-of-contents)**

4. ### Why do we need compilation process?
    The Angular components and templates cannot be understood by the browser directly. Due to that Angular applications require a compilation process before they can run in a browser. For example, In AOT compilation, both Angular HTML and TypeScript code converted into efficient JavaScript code during the build phase before browser runs it.

  **[⬆ Back to Top](#table-of-contents)**

5. ### What are the advantages with AOT?
    Below are the list of AOT benefits,

    1. **Faster rendering:** The browser downloads a pre-compiled version of the application. So it can render the application immediately without compiling the app.
    2. **Fewer asynchronous requests:** It inlines external HTML templates and CSS style sheets within the application javascript which eliminates separate ajax requests.
    3. **Smaller Angular framework download size:** Doesn't require downloading the Angular compiler. Hence it dramatically reduces the application payload.
    4. **Detect template errors earlier:** Detects and reports template binding errors during the build step itself
    5. **Better security:** It compiles HTML templates and components into JavaScript.  So there won't be any injection attacks.

  **[⬆ Back to Top](#table-of-contents)**

6. ### What are the ways to control AOT compilation?
    You can control your app compilation in two ways,
    1. By providing template compiler options in the `tsconfig.json` file
    2. By configuring Angular metadata with decorators

  **[⬆ Back to Top](#table-of-contents)**

7. ### What are the three phases of AOT?
    The AOT compiler works in three phases,
    1. **Code Analysis:** The compiler records a representation of the source
    2. **Code generation:** It handles the interpretation as well as places restrictions on what it interprets.
    3. **Validation:** In this phase, the Angular template compiler uses the TypeScript compiler to validate the binding expressions in templates.

  **[⬆ Back to Top](#table-of-contents)**

8. ### Can I use arrow functions in AOT?
    No, Arrow functions or lambda functions can’t be used to assign values to the decorator properties. For example, the following snippet is invalid:

    ```javascript
    @Component({
      providers: [{
        provide: MyService, useFactory: () => getService()
      }]
    })
    ```

    To fix this, it has to be changed as following exported function:

    ```javascript
    function getService(){
      return new MyService();
    }

    @Component({
      providers: [{
        provide: MyService, useFactory: getService
      }]
    })
    ```

    If you still use arrow function, it generates an error node in place of the function. When the compiler later interprets this node, it reports an error to turn the arrow function into an exported function.
    **Note:** From Angular5 onwards, the compiler automatically performs this rewriting while emitting the .js file.

  **[⬆ Back to Top](#table-of-contents)**

9. ### What is the purpose of metadata json files?
    The metadata.json file can be treated as a diagram of the overall structure of a decorator's metadata, represented as an abstract syntax tree(AST). During the analysis phase, the AOT collector scan the metadata recorded in the Angular decorators and outputs metadata information in .metadata.json files, one per .d.ts file.

  **[⬆ Back to Top](#table-of-contents)**

10. ### Can I use any javascript feature for expression syntax in AOT?
    No, the AOT collector understands a subset  of (or limited) JavaScript features. If an expression uses unsupported syntax, the collector writes an error node to the .metadata.json file. Later point of time, the compiler reports an error if it needs that piece of metadata to generate the application code.

  **[⬆ Back to Top](#table-of-contents)**


11. ### What is AOT compiler?
     The AOT compiler is part of a build process that produces a small, fast, ready-to-run application package, typically for production. It converts your Angular HTML and TypeScript code into efficient JavaScript code during the build phase before the browser downloads and runs that code.

     **[⬆ Back to Top](#table-of-contents)**
