# TypeScript Style Guide
> This is the TypeScript Style Guide that [Pobuca](https://www.pobuca.com) uses in every Front-End Project.    

This file also comes with a `tslint.json`.

# Rules

## TypeScript - SPECIFIC

### ban-ts-ignore
 - `// @ts-ignore` comments are not allowed.

### member-access
 - Add always private or public.

### no-empty-interface
 - Empty interfaces are not allowed.

### only-arrow-functions
 - Arrow function expressions are not allowed. Arrow functions are allowed if:  
   + `this` appears somewhere in its body
   + When they have a name

### prefer-for-of
 - Use`for-of` loop, over a standard `for` loop, if the index is only used to access the array being iterated.

### typedef
 - Add always a return type.


## FUNCTIONALITY

### ban-comma-operator
 - Comma operator is not allowed. Read more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comma_Operator) about the comma operator.

### curly
 - Use braces for `if`/`for`/`do`/`while` statements. Do not use braces when statements are on one line and start on the same line as their control-flow keyword.

### for-in
 - Inside a `for ... in` statement you must check that the property exists in the object.

```typescript
// Violation
const obj = { a: 1, b: 2, c: 3};
for(const key in obj) {
    console.log(obj[key]);
}

// Not violation
const obj = { a: 1, b: 2, c: 3};
for(const key in obj) {
    if(obj.hasOwnProperty(key)) {
        console.log(obj[key]);
    }
}
```

### function-constructor
 - Do not use the built-in `Function` constructor.
 > Calling the constructor directly is similar to eval, which is a symptom of design issues. String inputs 
   don’t receive type checking and can cause performance issues, particularly when dynamically created. If 
   you need to dynamically create functions, use “factory” functions that themselves return functions.

### label-position
 - Use [labels](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label) only in `do`/`for`/`while`/`switch` statements.

### no-arg
 - Do not use `arguments.callee`.
 > Using arguments.callee makes various performance optimizations impossible. See 
   [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments/callee) for more details 
   on why to avoid arguments.callee.

### no-async-without-await
 - Functions marked as `async` must contain an `await` or `return` statement.

### no-bitwise
 - Do not use `bitwise operators`.
 > Specifically, the following bitwise operators are banned: 
   `&`, `&=`, `|`, `|=`, `^`, `^=`, `<<`, `<<=`, `>>`, `>>=`, `>>>`, `>>>=`, and `~`. 
   This rule does not ban the use of & and | for intersection and union types.

### no-conditional-assignment
 - Do not use any type of assignment in conditionals.

 > Assignments in conditionals are often typos: for example `if (var1 = var2)` instead of 
   `if (var1 == var2)`. They also can be an indicator of overly clever code which decreases maintainability. 

### no-construct
 - Do not use the constructors of `String`, `Number`, and `Boolean`. Read more [here](https://stackoverflow.com/questions/4719320/new-number-vs-number).

```typescript
// Violation
new Number(a)

// Not violation
Number(foo)
```

### no-duplicate-super
 - Use `super()` only once in a constructor. Read more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super) for super in JavaScript.

### no-duplicate-switch-case
 - Do not have duplicate cases in switch statements.

### no-duplicate-variable
 - A variable declaration must be unique in the same block scope.

### no-empty
 - Empty blocks are not allowed, but empty catch blocks are allowed.

### no-eval
 - Disallows `eval` function invocations.
 > eval() is dangerous as it allows arbitrary code execution with full privileges. There are 
   [alternatives](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) for most of the use cases for eval().

### no-invalid-template-strings
 - Do not use `${` in a non-template string.

### no-invalid-this
 - Do not use the `this` keyword outside of classes.

### no-misused-new
 - Do not define `constructors` for `interfaces` or `new` for `classes`.

### no-return-await
 - Do not use unnecessary `return await`.

### no-shadowed-variable
 - No shadowing variable.

 > When a variable in a local scope and a variable in the containing scope have the same name, shadowing occurs. 
   Shadowing makes it impossible to access the variable in the containing scope and obscures to what value an 
   identifier actually refers.

### no-sparse-arrays
 - Do not contain missing elements in array literal.

```typescript
// Violation
const arr: string[] = ['elemenet1', 'element2'];

// Not violation
const arr: string[] = ['elemenet1', 'element2'];
```

### no-string-literal
 - Do not use unnecessary string literal property access.

```typescript
// Violation
obj['property']

// Not violation
obj.property
```

### no-string-throw
```typescript
// Violation
if (!product) {
    throw ("How can I add new product when no value provided?");
}

// Not violation
if (!product) {
    throw new Error("How can I add new product when no value provided?");
}
```

### no-tautology-expression
 - In a relational/equality binary operators do not use two equal variables/literals as operands.
 > Expression like `3 === 3`, `someVar === someVar`, `"1" > "1"` are either a tautology or contradiction.

### no-this-assignment
 - Do use unnecessary references to this.

### no-unsafe-finally
 - Do not use control flow statements, such as `return`, `continue`, `break` and `throws` in a `finally` block.

### no-var-keyword
 - Do not use the `var` keyword.

### prefer-conditional-expression
 - Use a conditional expression instead of assigning to the same thing in each branch of an if statement.

### prefer-object-spread
 - Use the ES2018 object `spread operator` over the `Object.assign()` where appropriate.

### radix
 - Use the `radix` parameter when calling `parseInt`. Read more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt).

### static-this
 - Do not use `this` in static methods.

### switch-default
 - Use always a `default` case in all `switch` statements.

### triple-equals
 - Use `===` and `!==` instead of `==` and `!=`.

### unnecessary-constructor
 - Delete blank constructors, as they are redundant.

### use-isnan
 - Use the `isNaN()` function to check for NaN references instead of a comparison to the `NaN` constant.


## MAINTAINABILITY

### max-classes-per-file
 - A file may not contain more than one class.

### max-file-line-count
 - TypeScript files must remain under `300` lines.

### no-duplicate-imports
 - Do not multiple import statements from the same module.

```typescript
// Violation
import { Observable } from 'rxjs';
import { Observer } from 'rxjs';

// Not violation
import { Observable, Observer } from 'rxjs';
```

### no-require-imports
 - Use the newer ES6-style `imports` over `require()`.

### prefer-const 
 - Use `const` instead of `let` and `var` if possible.


## STYLE

### array-type
 - Requires using `T[]` for arrays.

```typescript
 // Violation
data: Array<string>;

// Not violation
data: string[];
```

### arrow-return-shorthand
 - Use `() => x` instead of `() => { return x; }`.

```typescript
 // Violation
public a = {
	b: () =>  { return ''; }
};

// Not violation
public a = {
	b: () => ''
};

```

### binary-expression-operand-order
 - In a binary expression, a literal should always be on the right-hand side if possible. 

```typescript
// Violation
public a(x) {
    const b = 1 + x;
}

// Not violation
public a(x) {
    const b = x + 1;
}
```

### class-name
 - Use PascalCased class and interface names.

```typescript
// Violation
class appComponent

// Not violation
class AppComponent
```

### comment-format
 - Add a space after the `//` and only the first comment of a series of comments needs to be uppercase.

```typescript
//violation

// Not violation
```

### comment-type
 - Comments starting with `///` are not allowed. 

### encoding
 - Use `UTF-8` file encoding.

### file-name-casing
 - File names must be kebab-cased: `file-name.ts`.

### interface-name
 - Interface names must start with an `I`

```typescript
// Violation
interface Marker { }

// Not violation
interface IMarker { }
```

### no-unnecessary-callback-wrapper
 - Replaces `x => f(x)` with just `f`. There’s generally no reason to wrap a function with a callback wrapper 
   if it’s directly called anyway. Doing so creates extra inline lambdas that slow the runtime down.

```typescript
// Violation
const handleContent = (content) => console.log('Handle content:', content);
const handleError = (error) => console.log('Handle error:', error);
promise.then((content) => handleContent(content)).catch((error) => handleError(error));

// Not violation
const handleContent = (content) => console.log('Handle content:', content);
const handleError = (error) => console.log('Handle error:', error);
promise.then(handleContent).catch(handleError);
```

### object-literal-key-quotes
 - Only property names which require quotes may be quoted.

```typescript
// Violation
const a = { 'b': 1 };

// Not violation
const a = { b: 1 };
```

### object-literal-shorthand
 - Use ES6 object literal shorthand.

```typescript
// Violation
const a = 5;
const myObj = {
    a: a,
    b: function () { }
};

// Not violation
const a = 5;
const myObj = {
    a,
    b: () => { }
};
```

### one-line
 -  The specified tokens must be on the same line as the expression preceding them.

```typescript
// Violation
if (a) {
    console.log('a is true');
}
else {
    console.log('a is false');
}

try {
    console.log('try');
}
catch(ex) {
    console.log(ex);
}
finally {
    console.log('always');
}

// Not violation
if (a) {
    console.log('a is true');
} else {
    console.log('a is false');
}

try {
    console.log('try my');
} catch(ex) {
    console.log(ex);
} finally {
    console.log('always');
}
```

### one-variable-per-declaration
 - Multiple variable definitions in the same declaration statement are not allowed.

```typescript
// Violation
let a = 1, b = 2;

// Not violation
let a = 1; 
let b = 2;
```

### prefer-switch
 - Use a switch statement instead of an if statement when the if is a simple === comparisons. The number of cases must be more than 2.

### prefer-template
 - Use a template expression over string literal concatenation.

```typescript
// Violation
const t = 'Bearer' + token;

// Not violation
const t = `Bearer ${token}`;
```

### prefer-while
 - Use while loops instead of for loops without an initializer and incrementor.

### space-before-function-paren
 - Do not add a space before function parenthesis.

### switch-final-break
 - The final clause of a switch statement must end with a `break`. 

### unnecessary-else
 - Do not use `else`, if the block ends with a `break`, `continue`, `return`, or `throw statement`.

### variable-name
 - The variables names must be `lowerCamelCased` or `UPPER_CASED`.

## FORMAT

### align
 - Vertical align your code. Consistent alignment for code statements helps keep code readable and clear.
   Statements misaligned from the standard can be harder to read and understand.

### arrow-parens
 - Arrow functions must have parentheses.

### import-spacing
 - Use one space between import statement keywords.

```typescript
// Violation
import { a as b   }    from './a';

// Not violation
import { a as b } from './a';
```

### indent
 - For intent use tabs with 4 spaces.

### max-line-length
 - Limiting the length of a line of code to `200` characters, improves code readability.

## new-parens
 - Use parentheses when invoking a constructor via the `new` keyword.

```typescript
// Violation
const a = new Object;

// Not violation
const a = new Object();
```

### no-consecutive-blank-lines
 - Do not use more than one blank line in a row.

### no-irregular-whitespace
 - Do not use irregular whitespace within a file, including strings and comments.

### no-trailing-whitespace
 - Do not use trailing whitespace at the end of a line.

### number-literal-format
 - Decimal literals should begin with `0.` instead of just `.`.

```typescript
// Violation
const a = .5;

// Not violation
const a = 0.5;
```

### quotemark
 - Use single quotes or backticks.

### semicolon
 - Use semicolon at the end of every statement, except in interfaces.
