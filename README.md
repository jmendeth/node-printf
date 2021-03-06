                _       _    __ 
               (_)     | |  / _|
     _ __  _ __ _ _ __ | |_| |_ 
    | '_ \| '__| | '_ \| __|  _|
    | |_) | |  | | | | | |_| |  
    | .__/|_|  |_|_| |_|\__|_|  
    | |                         
    |_| 

A complete implementation of the **`printf` C functions family**
for [Node.JS][node], written in pure JavaScript.  
The code is strongly inspired by the one availabe in the [Dojo Toolkit][dojo].

**Bonus!** You get extra features, like the `%O` converter (which `inspect`s
the argument). See [Extra Features](#extra-features) below.

## Installing

Via [NPM][npm]:

```bash
$ npm install printf
```

## Usage

Use it like you would in C (`printf`/`sprintf`):

``` javascript
var printf = require('printf');
var result = printf(format, args...);
```

It can also output the result for you, as `fprintf`:

``` javascript
var printf = require('printf');
printf(write_stream, format, args...);
```

## Features

``` javascript
var printf = require('printf');
```
    
### Flags

##### ` ` (space)

``` javascript
assert.eql('  -42', printf('% 5d', -42));
```

##### `+` (plus)

``` javascript
assert.eql('  +42', printf('%+5d', 42));
```

##### `0` (zero)

``` javascript
assert.eql('00042', printf('%05d', 42));
```

##### `-` (minus)

``` javascript
assert.eql('42   ', printf('%-5d', 42));
```

### Width / precision

``` javascript
assert.eql('42.90', printf('%.2f', 42.8952));
assert.eql('042.90', printf('%06.2f', 42.8952));
```

### Numerical bases

``` javascript
assert.eql('\x7f', printf('%c', 0x7f));
assert.eql('a', printf('%c', 'a'));
assert.eql('"', printf('%c', 34));
```

### Miscellaneous

``` javascript
assert.eql('10%', printf('%d%%', 10));
assert.eql('+hello+', printf('+%s+', 'hello'));
assert.eql('$', printf('%c", 36));
```

## Extra features!

### Inspector

The `%O` converter will call [`util.inspect(...)`][util_inspect] at the argument:

``` javascript
assert.eql("Debug: { hello: 'Node', repeat: false }",
  printf('Debug: %O', {hello: 'Node', "repeat": false})
);
assert.eql("Test: { hello: 'Node' }",
  printf('%2$s: %1$O', {"hello": 'Node'}, 'Test')
);
```

**Important:** it's a capital "O", *not* a zero!

### Argument mapping

In addition to the old-fashioned `n$`,  
you can use **hashes** and **property names**!

``` javascript
assert.eql('Hot Pockets',
  printf('%(temperature)s %(crevace)ss', {
    temperature: 'Hot',
    crevace: 'Pocket'
  })
);
assert.eql('Hot Pockets',
  printf('%2$s %1$ss', 'Pocket', 'Hot')
);
```

### Positionals

Lenght and precision can now be variable:

``` javascript
assert.eql(' foo', printf('%*s', 'foo', 4));
assert.eql('      3.14', printf('%*.*f', 3.14159265, 10, 2));
assert.eql('0000003.14', printf('%0*.*f', 3.14159265, 10, 2));
assert.eql('3.14      ', printf('%-*.*f', 3.14159265, 10, 2));
```

## Test

Using [Expresso][expresso]:

```bash
expresso
```


[dojo]: http://www.dojotoolkit.org  "The Dojo Toolkit"
[node]: http://nodejs.org "The Node.JS platform"
[npm]:  https://github.com/isaacs/npm "The Node Package Manager"
[util_inspect]: http://nodejs.org/api/util.html#util_util_inspect_object_showhidden_depth_colors "util.inspect() documentation"
[expresso]: http://visionmedia.github.com/expresso "The Expresso TDD"
