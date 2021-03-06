QuakeC
======

About QuakeC
------------

QuakeC is a very simplified dialect of the well-known C programming language, and is used by the Quake I engine and its derivatives. Xonotic uses the GMQCC dialect of QuakeC, so only this dialect will be described (as well as some common extensions among Quake engines).

There are several documents describing the original version of QC as used in Quake 1:
- an [old version](http://www.gamers.org/dEngine/quake/spec/quake-spec34/index1.htm) which is a part of unofficial [Quake Documentation](http://www.gamers.org/dEngine/quake/spec/quake-spec34/)
- a probably slightly [newer version](http://www.cataboligne.org/extra/qcmanual.html)
- a [newer and extended version](http://pages.cs.wisc.edu/~jeremyp/quake/quakec/quakec.pdf) in PDF

Even this page is outdated and incomplete, not all GMQCC QuakeC constructs are described here and some of the bugs mentioned here have already been fixed.

Other resources
---------------

- [QC Tutorial for Absolute Beginners](https://web.archive.org/web/20091118154016/http://forums.inside3d.com/viewtopic.php?t=1286)
- [List of builtins on quakewiki.org](https://quakewiki.org/wiki/List_of_builtin_functions)
- comments and `doc.md` in the `qcsrc/dpdefs` directory

Example code
------------

To see what QuakeC looks like, here is a piece of example code:

```c
// needed declarations:
float vlen(vector v) = #12;
entity nextent(entity e) = #47;
.string classname;
.vector origin;
// ...
entity findchain(.string fld, string match)
{
    entity first, prev;
    first = prev = world;
    for(entity e = world; (e = nextent(e)); e++) {
        if (e.fld == match) {
            e.chain = world;
            if (prev) {
                prev.chain = e;
            } else {
                first = e;
            }
            prev = e;
        }
    }
    return first;
}
// ...
entity findnearestspawn(vector v)
{
    entity nearest;
    for (entity e = findchain(classname, "info_player_deathmatch"); e; e = e.chain) {
        if (!nearest) {
            nearest = e;
        } else if(vlen(e.origin - v) < vlen(nearest.origin - v)) {
            nearest = e;
        }
    }
    return nearest;
}
```

**Note:** *findchain* is implemented in QuakeC for demonstration purposes only so one can see how to build a linked list, as this function is already built in to the engine and can be used directly

Variables
=========

Declaring
---------

To declare a variable, the syntax is the same as in C:

```c
float i;
```

Whenever a variable declaration could be interpreted as something else by the compiler, the *var* keyword helps disambiguating. For example,

```c
float(float a, float b) myfunc;
```

is an old-style function declaration, while

```c
var float(float a, float b) myfunc;
```

declares a variable of function type. An alternate and often more readable way to disambiguate variable declarations is using a *typedef*, like so:

```c
typedef float(float, float) myfunc_t;
myfunc_t myfunc;
```

Scope
-----

A variable declared in the global scope has global scope, and is visible starting from its declaration to the end of the code. The order the code is read in by the compiler is defined in the file %progs.src%.
A variable declared inside a function has block scope, and is visible starting from its declaration to the end of the smallest block that contains its declaration.

Some variables are declared in [sys.qh](http://git.xonotic.org/?p=xonotic/xonotic-data.pk3dir.git;a=blob_plain;f=qcsrc/server/sys.qh;hb=HEAD). Their declarations or names should never be changed, as they have to match the order and names of the variables in the file file [progdefs.h](http://svn.icculus.org/twilight/trunk/darkplaces/progdefs.h?view=markup) of the engine exactly, or the code won’t load. The special markers *end\_sys\_globals* and *end\_sys\_fields* are placed to denote the end of this shared declaration section.

Types
=====

Quake only knows four elementary data types: the basic types `float`, `vector`, `string`, and the object type `entity`. Also, there is a very special type of types, `fields`, and of course `functions`. GMQCC also adds `arrays`, although these are slow. Note that there are no pointers!

There are also `int` and `bool` typedefs, but no guarantees are made on the range of values as they are currently not supported by GMQCC.

float
-----

This is the basic numeric type in QuakeC. It represents the standard 32bit floating point type as known from C. It has 23 bits of mantissa, 8 bits of exponent, and one sign bit. The numeric range goes from about `1.175e-38` to about `3.403e+38`, and the number of significant decimal digits is about six.

As float has 23 bits of mantissa, it can also be used to safely represent integers in the range from `–16777216` to `16777216`. `16777217` is the first integer *float* can not represent.

Common functions for `float` are especially **ceil**, **floor** (working just like in C, rounding up/down to the next integer), and **random**, which yields a random number `r` with `0 <= r < 1`.

vector
------

This type is basically three floats together. By declaring a `vector v`, you also create three floats `v_x`, `v_y` and `v_z` (note the underscore) that contain the components of the vector. GMQCC also accepts dot notation to access these components: `v.x`, `v.y` and `v.z`

**COMPILER BUG:** Always use `entity.vector_x = float` instead of `entity.vector.x = float`, as the latter creates incorrect code! Reading from vectors is fine, however.

Vectors can be used with the usual mathematical operators in the usual way used in mathematics. For example, `vector + vector` simply returns the sum of the vectors, and `vector * float` scales the vector by the given factor. Multiplying two vectors yields their dot product of type float.

Common functions to be used on vectors are `vlen` (vector length), `normalize` (vector divided by its length, i.e. a unit vector).

Vector literals are written like `'1 0 0'`.

string
------

A *string* in QuakeC is an immutable reference to a null-terminated character string stored in the engine. It is not possible to change a character in a string, but there are various functions to create new strings:
-  **ftos** and **vtos** convert *floats* and *vectors* to strings. Their inverses are, of course, **stof** and **stov**, which parse a *string* into a *float* or a *vector*.

-   **strcat** concatenates 2 to 8 strings together, as in:
    ```c
    strcat("a", "b", "c") == "abc";
    ```

-   **strstrofs(haystack, needle, offset)** searches for an occurrence of one string in another, as in:
    ```c
    strstrofs("haystack", "ac", 0) == 5;
    ```

The offset defines from which starting position to search, and the return value is `–1` if no match is found. The offset returned is *0*-based, and to search in the whole string, a start offset of *0* would be used.

-   **strreplace(old, new, string)** searches for certain characters in a string and replaces them with other characters, as in:
    ```c
    strreplace("de", "con", "destruction") == "construction";
    ```

-   **substring(string, startpos, length)** returns part of a string.

The offset is *0*-based here, too. A length of `-1` designates the end of the string (it will return the part of the string after the start position), a length of `-2` designates the penultimate character of the string, and so on.

-   **strtoupper(string)** capitalizes a string.
-   **strtolower(string)** lowercases a string.

Note that there are different kinds of *strings*, regarding memory management:

-   **Temporary strings** are strings returned by built-in string handling functions such as **substring**, **strcat**. They last only for the duration of the function call from the engine. That means it is safe to return a temporary string in a function you wrote, but not to store them in global variables or objects as their storage will be overwritten soon.
-   **Allocated strings** are strings that are explicitly allocated. They are returned by *strzone* and persist until they are freed (using **strunzone**). Note that **strzone** does not change the string given as a parameter, but returns the newly allocated string and keeps the passed temporary string the same way! That means:
    +   To allocate a string, do for example:
        ```c
        myglobal = strzone(strcat("hello ", "world"));
        ```

    +   To free the string when it is no longer needed, do:
        ```c
        strunzone(myglobal);
        ```

-   **Engine-owned strings**, such as *netname*. These should be treated just like temporary strings: if you want to keep them in your own variables, *strzone* them.
-   **Constant strings:** A string literal like *“foo”* gets permanent storage assigned by the compiler. There is no need to *strzone* such strings.
-   **The null string:** A global uninitialized *string* variable has the special property that is is usually treated like the constant, empty, string *“”* (so using it does not constitute an error), but it is the only string that evaluates to FALSE in an if expression (but not in the ! operator~~ in boolean context, the string “” counts as FALSE too). As this is a useful property, Xonotic code declares such a string variable of the name *string\_null*. That means that the following patterns are commonly used for allocating strings:
    +   Assigning to a global string variable:
        ```c
        if (myglobal) {
            strunzone(myglobal);
        }

        myglobal = strzone(...);
        ```

    +   Freeing the global string variable:
        ```c
        if (myglobal) {
            strunzone(myglobal);
        }

        myglobal = string_null;
        ```

    +   Checking if a global string value has been set:
        ```c
        if (myglobal) {
            value has been set;
        } else {
            string has not yet been set;
        }
        ```

entity
------

The main object type in QuakeC is *entity*, a reference to an engine internal object. An *entity* can be imagined as a huge struct, containing many *fields*. This is the only object type in the language. However, *fields* can be added to the *entity* type by the following syntax:

```c
.float myfield;
```

and then all objects *e* get a field that can be accessed like in *e.myfield*.

The special entity *world* also doubles as the *null* reference. It can not be written to other than in the *spawnfunc\_worldspawn* function that is run when the map is loaded, and is the only entity value that counts as *false* in an *if* expression. Thus, functions that return *entities* tend to return *world* to indicate failure (e.g. *find* returns *world* to indicate no more entity can be found).

If a field has not been set, it gets the usual zero value of the type when the object is created (i.e. *0* for *float*, *string\_null* for *string*, *’0 0 0’* for *vector*, and *world* for *entity*).

fields
------

A reference to such a field can be stored too, in a field variable. It is declared and used like

```c
.float myfield;
// ...
// and in some function:
var .float myfieldvar;
myfieldvar = myfield;
e.myfieldvar = 42;
```

Field variables can be used as function parameters too - in that case you leave the *var* keyword out, as it is not needed for disambiguation.

functions
---------

Functions work just like in C:

```c
float sum3(float a, float b, float c)
{
    return a + b + c;
}
```

However, the syntax to declare function pointers is simplified:

```c
// in global scope
typedef float(float, float, float) op3func_t;
var float(float a, float b, float c) f;
op3func_t g;

// in local scope
f = sum3;
g = f;
print(ftos(g(1, 2, 3)), "\n"); // prints 6
```

Also note that the *var* keyword is used again to disambiguate from a global function declaration.

In original QuakeC by iD Software, this simplified function pointer syntax also was the only way to define functions (you may still encounter this in Xonotic’s code in a few places):

```c
float(float a, float b) sum2 = {
    return a + b;
}
```

A special kind of functions are the built-in functions, which are defined by the engine. These are imported using so-called built-in numbers, with a syntax like:

```c
string strcat(string a, string b, ...) = #115;
```

The function/field syntax is ambiguous. In global scope a declaration can be a variable, field or function. In local scope, it's always a variable. The `var` keyword can be used in global scope to treat it as local scope (always declaring a variable). The following table shows declarations in global scope:

| Example code | Meaning |
|--------------|---------|
| `.float a;` | Entity field of type `float` |
| `float(float x1) a;` or `float a(float x1);` | Function with a `float` param returning `float` |
| `.float a(float x1);` | Function with a float param returning a `float` field reference |
| `.float(float x1) a;` | Entity field of type function with a `float` param returning `float` |
| `.float(float x1) a(float x2);` | Function with a `float` param returning a field reference of type function with a `float` param returning `float` |

These rules were determined by experimenting with GMQCC:
- if there are parentheses after the name, it's always a function
- else if it starts with a period, it's a field
- else if there are parentheses after the type, it's a function (using the old QC syntax)
- else it's a variable

GMQCC allows even weirder declarations like `float f(float)();` which can be called as `f()(42);`. It's not clear whether this behavior is intentional or the result of one of the many compiler bugs.

void
----

Just like in C, the *void* type is a special placeholder type to declare that a function returns nothing. However, unlike in C, it is possible to declare variables of this type, although the only purpose of this is to declare a variable name without allocating space for it. The only occasion where this is used is the special *end\_sys\_globals* and *end\_sys\_fields* marker variables.

arrays
------

As the QuakeC virtual machine provides no pointers or similar ways to handle arrays, array support is added by GMQCC and very limited. Arrays can only be global, must have a fixed size (not dynamically allocated), and are a bit slow. Almost as great as in FORTRAN, except they can’t be multidimensional either!

You declare arrays like in C:

```c
#define MAX_ASSASSINS 16
entity assassins[MAX_ASSASSINS];
#define BTREE_MAX_CHILDREN 5
.entity btree_child[BTREE_MAX_CHILDREN];
#define MAX_FLOATFIELDS 3
var .float myfloatfields[MAX_FLOATFIELDS];
```

The former is a global array of entities and can be used the usual way:

```c
assassins[self.assassin_index] = self;
```

The middle one is a global array of (allocated and constant) entity fields and **not** a field of array type (which does not exist), so its usage looks a bit strange:

```c
for (int i = 0; i < BTREE_MAX_CHILDREN; i++)
    self.(btree_child[i]) = world;
```

Note that this works:

```c
var .entity indexfield;
indexfield = btree_child[i];
self.indexfield = world;
```

The latter one is a global array of (assignable) entity field variables, and looks very similar:

```c
myfloatfields[2] = health;
self.(myfloatfields[2]) = 0;
// equivalent to self.health = 0;
```

Do not use arrays when you do not need to - using both arrays and function calls in the same expression can get messed up (**COMPILER BUG**), and arrays are slowly emulated using functions `ArrayGet*myfloatfields` and `ArraySet*myfloatfields` the compiler generates that internally do a binary search for the array index.

Peculiar language constructs
============================

This section deals with language constructs in QuakeC that are not similar to anything in other languages.

if not (deprecated)
-------------------

There is a second way to do a negated *if*:

```c
if not(expression)
    ...
```

It compiles to the same code as

```c
if (!expression)
    ...
```

and has the notable difference that

```c
if not("")
    ...
```

will not execute (as *“”* counts as true in an *if* expression), but

```c
if (!"")
    ...
```

will execute (as both `""` and `string_null` is false when boolean operators are used on it).

Common patterns
===============

Some patterns in code that are often encountered in Xonotic are listed here, in no particular order.

Classes in Quake
----------------

The usual way to handle classes in Quake is using *fields*, function pointers and the special property *classname*.

But first, let’s look at how the engine creates entities when the map is loaded.

Assume you have the following declarations in your code:

```c
entity self;
    .string classname;
    .vector origin;
    .float height;
```

and the engine encounters the entity

```c
{
    "classname" "func_bobbing"
    "height" "128"
    "origin" "0 32 –64"
}
```

then it will, during loading the map, behave as if the following QuakeC code was executed:

```c
self = spawn();
self.classname = "func_bobbing";
self.height = 128;
self.origin = '0 32 -64';
spawnfunc_func_bobbing();
```

We learn from this:
-   The special global *entity* variable *self* is used when “methods” of an object are called, like - in this case - the “constructor” or spawn function `spawnfunc_func_bobbing`.
-   Before calling the spawn function, the engine sets the mapper specified fields to the values. String values can be treated by the QC code as if they are constant strings, that means there is no need to **strzone** them.
-   Spawn functions always have the *spawnfunc\_* name prefix and take no arguments.
-   The *string* field *classname* always contains the name of the entity class when it was created by the engine.
-   As the engine uses this pattern when loading maps and this can’t be changed, it makes very much sense to follow this pattern for all entities, even for internal use. Especially making sure *classname* is set to a sensible value is very helpful.

Methods are represented as fields of function type:

```c
.void() think;
```

and are assigned to the function to be called in the spawn function, like:

```c
void func_bobbing_think()
{
    // lots of stuff
}
```

```c
void spawnfunc_func_bobbing()
{
    // ... even more stuff ...
    self.think = func_bobbing_think;
}
```

To call a method of the same object, you would use

```c
self.think();
```

but to call a method of another object, you first have to set *self* to that other object, but you typically need to restore *self* to its previous value when done:

```c
entity oldself;
// ...
oldself = self;
self.think();
self = oldself;
```

Think functions
---------------

A very common entry point to QuakeC functions are so-called think functions.

They use the following declarations:

```c
.void() think;
.float nextthink;
```

If *nextthink* is not zero, the object gets an attached timer: as soon as *time* reaches *nextthink*, the *think* method is called with *self* set to the object. Before that, *nextthink* is set to zero. So a typical use is a periodic timer, like this:

```c
void func_awesome_think()
{
    bprint("I am awesome!");
    self.nextthink = time + 2;
}
```

```c
void spawnfunc_func_awesome()
{
    // ...
    self.think = func_awesome_think;
    self.nextthink = time + 2;
}
```

Find loops
----------

One common way to loop through entities is the find loop. It works by calling a built-in function like

```c
entity find(entity start, .string field, string match) = #18;
```

repeatedly. This function is defined as follows:

-   if *start* is *world*, the first entity *e* with `e.field==match` is returned
-   otherwise, the entity *e* **after** *start* in the entity order with `e.field==match` is returned
-   if no such entity exists, *world* is returned

It can be used to enumerate all entities of a given type, for example `"info_player_deathmatch"`:

```c
for (entity e = world; (e = find(e, classname, "info_player_deathmatch")); )
    print("Spawn point found at ", vtos(e.origin), "\n");
```

There are many other functions that can be used in find loops, for example *findfloat*, *findflags*, *findentity*.

Note that the function *findradius* is misnamed and is not used as part of a find loop, but instead sets up a linked list of the entities found.

Linked lists
------------

An alternate way to loop through a set of entities is a linked list. I assume you are already familiar with the concept, so I’ll skip information about how to manage them.

It is however noteworthy that some built-in functions create such linked lists using the *entity* field *chain* as list pointer. Some of these functions are the aforementioned *findradius*, and *findchain*, *findchainfloat*, *findchainflags* and *findchainentity*.

A loop like the following could be used with these:

```c
for (entity e = findchain(classname, "info_player_deathmatch"); e; e = e.chain)
        print("Spawn point found at ", vtos(e.origin), "\n");
```

The main advantage of linked lists however is that you can keep them in memory by using other fields than *chain* for storing their pointers. That way you can avoid having to search all entities over and over again (which is what *find* does internally) when you commonly need to work with the same type of entities.

Error handling
--------------

Error handling is virtually non-existent in QuakeC code. There is no way to throw and handle exceptions.

However, built-in functions like *fopen* return `-1` on error.
To report an error condition, the following means are open to you:
-   Use the *print* function to spam it to the console. Hopefully someone will read that something went wrong. After that, possibly use *remove* to delete the entity that caused the error (but make sure there are no leftover references to it!).
-   Use the *error* function to abort the program code and report a fatal error with a backtrace showing how it came to it.
-   Use the *objerror* function to abort spawning an entity (i.e. removing it again). This also prints an error message, and the entity that caused the error will not exist in game. Do not forget to *return* from the spawn function directly after calling *objerror*!

target and targetname
---------------------

In the map editor, entities can be connected by assigning a name to them in the *target* field of the targeting entity and the *targetname* field of the targeted entity.
To QuakeC, these are just strings - to actually use the connection, one would use a find loop:

```c
entity oldself = self;
for (self = world; (self = find(self, targetname, oldself.target)); )
    self.use();
self = oldself;
```

the enemy field and its friends
-------------------------------

As the find loop for *target* and *targetname* causes the engine to loop through all entities and compare their *targetname* field, it may make sense to do this only once when the map is loaded.

For this, a common pattern is using the pre-defined *enemy* field to store the target of an entity.

However, this can’t be done during spawning of the entities yet, as the order in which entities are loaded is defined by the map editor and tends to be random. So instead, one should do that at a later time, for example when the entity is first used, in a think function, or - the preferred way in the Xonotic code base - in an *InitializeEntity* function:

```c
void teleport_findtarget()
{
    // ...
    self.enemy = find(world, targetname, self.target);
    if (!self.enemy)
        // some error handling...
    // ...
}
```

```c
void spawnfunc_trigger_teleport()
{
    // ...
    InitializeEntity(self, teleport_findtarget, INITPRIO_FINDTARGET);
    // ...
}
```

*InitializeEntity* functions are guaranteed to be executed at the beginning of the next frame, before the *think* functions are run, and are run in an order according to their priorities (the *INITPRIO*\_ constants).

Tracing
-------

Pitfalls and compiler bugs
==========================

variable shadowing
------------------

```c
.float height;
void update_height(entity e, float height) {
    e.height = height;
}
```
`error: invalid types in assignment: cannot assign .float to float`

The height *field* overrides the height *parameter*; change the parameter name somehow (`_height`).

complex operators
-----------------

Do not count on the modifying and reading operators like *+=* or *++* to always work. Using them in simple cases like:
```c
a += 42;
for (int i = 0; i < n; i++) {
    ...
}
```
is generally safe, but complex constructs like:
```c
self.enemy.frags += self.value--;
```
are doomed. Instead, split up such expressions into simpler steps:
```c
self.enemy.frags = self.enemy.frags + self.value;
self.value -= 1;
```
The compiler warning **RETURN VALUE ALREADY IN USE** is a clear indicator that an expression was too complex for it to deal with it correctly. If you encounter the warning, do make sure you change the code to no longer cause it, as the generated code **will** be incorrect then.
Also, do not use the *+=* like operators on *vector*s, as they are known to create incorrect code and only operate on the *x* component of the vector.

functions VS. arrays
--------------------

Mixing function calls with array dereferencing, or doing more than one array dereferencing in the same expression, is known to create incorrect code. Avoid constructs like:

```c
print(ftos(floatarray[i]), " --> ", stringarray[i], anotherstringarray[i], "\n");
```

as the array dereferencings and the *ftos* return value are likely to overwrite each other. Instead, simplify it:
```c
float f;
string s, s2;
// ...
f = floatarray[i];
s = stringarray[i];
s2 = anotherstringarray[i];
print(ftos(f), " --> ", s, s2, "\n");
```

vectoangles does not match makevectors
--------------------------------------

The pitch angle is inverted between these two functions. You have to negate the pitch (i.e. the *x* component of the vector representing the euler angles) to make it fit the other function.
As a rule of thumb, *vectoangles* returns angles as stored in the *angles* field (used to rotate entities for display), while *makevectors* expects angles as stored in the *v\_angle* field (used to transmit the direction the player is aiming). There is about just as much good reason in this as there is for 1:1 patch cables. Just deal with it.

Entry points
============

The server-side code calls the following entry points of the QuakeC code:

-   **void ClientDisconnect()**: called when a player leaves the server. Do not forget to *strunzone* all *strings* stored in the player entity here, and do not forget to clear all references to the player!
<br />

-   **void SV\_Shutdown()**: called when the map changes or the server is quit. A good place to store persistent data like the database of race records.
<br />

-   **void SV\_ChangeTeam(float newteam)**: called when a player changes his team. Can be used to disallow team changes, or to clear the player’s scores.
<br />

-   **void ClientKill()**: called when the player uses the ”kill" console command to suicide.
<br />

-   **void RestoreGame()**: called directly after loading a save game. Useful to, for example, load the databases from disk again.
<br />

-   **void ClientConnect()**: called as soon as a client has connected, downloaded everything, and is ready to play. This is the typical place to initialize the player entity.
<br />

-   **void PutClientInServer()**: called when the client requests to spawn. Typically puts the player somewhere on the map and lets him play.
<br />

-   **.float SendEntity(entity to, float sendflags)**: called when the engine requires a CSQC networked entity to send itself to a client, referenced by *to*. Should write some data to *MSG\_ENTITY*. *FALSE* can be returned to make the entity not send. See *EXT\_CSQC* for information on this.
<br />

-   **void URI\_Get\_Callback(...)**:
<br />

-   **void GameCommand(string command)**: called when the “sv\_cmd” console command is used, which is commonly used to add server console commands to the game. It should somehow handle the command, and print results to the server console.
<br />

-   **void SV\_OnEntityNoSpawnFunction()**: called when there is no matching spawn function for an entity. Just ignore this...
<br />

-   **void SV\_OnEntityPreSpawnFunction**: called before even looking for the spawn function, so you can even change its classname in there. If it remove()s the entity, the spawn function will not be looked for.
<br />

-   **void SV\_OnEntityPostSpawnFunction**: called ONLY after its spawn function or SV\_OnEntityNoSpawnFunction was called, and skipped if the entity got removed by either.
<br />

-   **void SetNewParms()**:
<br />

-   **void SetChangeParms()**:
<br />

-   **.float customizeentityforclient()**: called for an entity before it is going to be sent to the player specified by *other*. Useful to change properties of the entity right before sending, e.g. to make an entity appear only to some players, or to make it have a different appearance to different players.
<br />

-   **.void touch()**: called when two entities touch; the other entity can be found in *other*. It is, of course, called two times (the second time with *self* and *other* reversed).
<br />

-   **.void contentstransition()**:
<br />

-   **.void think()**: described above, basically a timer function.
<br />

-   **.void blocked()**: called when a *MOVETYPE\_PUSH* entity is blocked by another entity. Typically does either nothing, reverse the direction of the door moving, or kills the player who dares to step in the way of the Mighty Crusher Door.
<br />

-   **.void movetypesteplandevent()**: called when a player hits the floor.
<br />

-   **.void PlayerPreThink()**: called before a player runs his physics. As a special exception, *frametime* is set to 0 if this is called for a client-side prediction frame, as it still will get called for server frames.
<br />

-   **.void PlayerPreThink()**: called after a player runs his physics. As a special exception, *frametime* is set to 0 if this is called for a client-side prediction frame, as it still will get called for server frames.
<br />

-   **void StartFrame()**: called at the beginning of each server frame, before anything else is done.
<br />

-   **void EndFrame()**: called at the end of each server frame, just before waiting until the next frame is due.
<br />

-   **void SV\_PlayerPhysics()**: allows to replace the player physics with your own code. The movement the player requests can be found in the *vector* field *movement*, and the currently pressed buttons are found in various fields, whose names are aliased to the *BUTTON*\_ macros.
<br />

-   **void SV\_ParseClientCommand(string command)**: handles commands sent by the client to the server using “cmd ...”. Unhandled commands can be passed to the built-in function *clientcommand* to execute the normal engine behaviour.
<br />
