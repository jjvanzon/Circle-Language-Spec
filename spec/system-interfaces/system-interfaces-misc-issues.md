﻿Encircle Language Spec | System Interfaces
==========================================

Misc Issues
-----------

`[ Preliminary documentation ]`

__Contents__

- [System Command Calls by User](#system-command-calls-by-user)
- [Objects Floating Around](#objects-floating-around)
- [System Command Extension](#system-command-extension)
- [Parameters For Objects](#parameters-for-objects)
    - [Concept](#concept)
    - [Diagram Notation](#diagram-notation)
- [Referrers](#referrers)
    - [Object Referrers](#object-referrers)
        - [Concept](#concept-1)
            - [`Not*` Supporting `the*` Referrers Concept](#not-supporting-the-referrers-concept)
        - [Diagram Notation](#diagram-notation-1)
    - [Class Referrers](#class-referrers)
        - [Concept](#concept-2)
            - [`Not*` Registering Class Referrers](#not-registering-class-referrers)
        - [Diagram Notation](#diagram-notation-2)
    - [Referrers Versus Related Objects](#referrers-versus-related-objects)
    - [`The*` Referrers Concept](#the-referrers-concept)
- [Loose Ideas](#loose-ideas)
    - [Loose Ideas about Referrers](#loose-ideas-about-referrers)

### System Command Calls by User

A user will often execute __Gets__ and __Sets__ and other system commands when connecting symbols together, but they will only see the connectors and the *result* of a __Get__ and __Set__, but never the explicit __Get__ and __Set__ calls. The system commands are executed as the user builds up a diagram.

### Objects Floating Around

Objects are never directly accessed. They are always floating around somewhere you cannot touch. You are always accessing an object through an *object reference*. You are always dealing with *references* to objects, never with the object directly.

![](images/5.%20System%20Objects%20Misc%20Issues.001.png)

The smaller, contained circles are *references* to objects, even though the bigger circle seems to be the sole container of the objects themselves. An object does not really contain sub-objects. An object contains pointers to its sub-objects. Even when the object seems the sole container of the other objects, the other objects are really only referenced. You do not see the actual object. You are only seeing references to it.

Another symbol can start referring to the same object, making the object all of a sudden not part of a unique container anymore.

![](images/5.%20System%20Objects%20Misc%20Issues.002.png)

When you annul the object reference in the original parent, the second parent all of a sudden becomes the sole container of the object.

![](images/5.%20System%20Objects%20Misc%20Issues.003.png)

The object has moved from one parent to another.

![](images/5.%20System%20Objects%20Misc%20Issues.004.png)

![](images/5.%20System%20Objects%20Misc%20Issues.005.png)

Objects are always just floating around like that. They do not have to stay in a fixed spot.

In reality the objects do not move at all. They are physically stored in the same spot all the time, no matter where they appear to be. An object can just be freely referenced from anywhere, because objects are always accessed through references.

Even when you *create* an object, you are not directly in touch with the object. The object is immediately assigned to an object reference. Also: when you assign a *value* to an object, you do not assign the value directly to the object, but you assign it through an object reference.

Each object reference gets its own identifier, even when an object reference is __Nothing__. An object itself, does not have an identifier. An object can be given a __Name__ attribute, though.

### System Command Extension

One thing that makes it important to be aware of system commands at all is *extension* of system commands.

A system command, such as __Get Value__, can be decorated with a procedure, that determines the value that is returned. It is the new computer language’s equivalent of __Getters__ and __Setters__ or __Property__ procedures. The __Get Object__ command can be extended as well, which makes you able to further control the connection between one object and the other.

Any system command can be decorated with a __Pre-Extension__, __Post-Extension__ or __Override__. 

System command extensions are implemented the same way as ‘normal’ command extensions. Command extension is put under the topic of *Inheritance*, because it is an extension technique.

System command extension will get a notation, that complies to the notation of normal command extension. The code base will implement system command extension like normal command extension and the way extension is implemented inside the code base will influence how the eventual notation will look.

It might look something like this:

![](images/5.%20System%20Objects%20Misc%20Issues.006.png)

But the exact way in which command extension is implemented will be covered by the *Inheritance* articles.

### Parameters For Objects

#### Concept

This is a preliminary description of the concept. The details are still to be worked out. It could be that in practice, when the new computer language is up and running, the details that have to be solved, will come to light straight away.

In other programming languages there are *getters* and *setters*, which are also called *properties*. Those are replaced by the fact, that any related object has a set of system commands, such as __Get Object__ and __Set Object__, that can be extended with extra code around the __Get__ and __Set__ actions.

For properties it is sometimes handy to hand a *parameter* to the retrieval of a value, and then a certain value is returned. For instance to return the pressure value of a sound wave at a certain time you could have a __Pressure__ object, that returns a value when you pass the __Time__ to it as an argument.

```
Pressure  (  Time  )
```

Even through the retrieval of pressure could be made a command with a parameter, one might want to see __Pressure__ as an *object*, rather than a *command*.

You can use a related object for that. A related object has a system interface, that allows you to let the eventual object it displays be determined by a procedure. The system interface controls what is returned as the related object. You can extend the __Get Value__ and __Set Value__ system commands. The new computer language must allow you to be able to add extra parameters to system commands, or add extra sub-objects to a system aspect, such as the __Value__ aspect, creating a single parameter for both __Get Value__ and __Set Value__ at the same time, and the new computer language should also allow you to add sub-objects to the whole system interface, to give the retrieval and assignment of any aspect the same parameter. So it is not really the object itself, that gets a parameter, but the related object, that gets a parameter. An object *reference* gets a parameter. That is why the parameter needs to be part of the system interface.

Because you can add a parameter to the whole system interface which extends every system command with a parameter, the new computer language should supply the capability to select which system commands actually get extended with the same parameter, and whether the __Time__ parameter is required or optional. __Time__ is a sub-object of the related object’s system interface, so it is not really a parameter of a command. However, it does extend the system commands with a __Time__ parameter, so a sub-object of a system interface is always called a parameter, but it is called a parameter of a *related* object instead of a parameter of a command.

Adding parameters to the system interface of a related object or extensive extension of system commands is a way to let a retrieval procedure be represented by an object instead of a command.

A command in the new computer language can have multiple return values, but when you convert the command into the retrieval procedure of a related object, the command will actually have a single return value. So in this case, you do have the concept of having only one single return value, unlike commands, in which you can have multiple return values.

There are no plans yet to make a command, that is a retrieval procedure, and a related object with an extensive retrieval procedure, two completely equally present views on the same thing (like other flat and structured interchange concepts within the language, like exchangeability of class commands and command parameters).

A query is also an example of a related object or related list with an extended system interface, that determines the item, list or result set eventually returned. Dependent on the parameters of the related object, the outcome is calculated.

#### Diagram Notation

Default system commands can be called with an easy notation, that does not show the system command definition:

![](images/5.%20System%20Objects%20Misc%20Issues.007.png)

![](images/5.%20System%20Objects%20Misc%20Issues.008.png)

![](images/5.%20System%20Objects%20Misc%20Issues.009.png)

Even though you can also display the system interface and show a call to the command definition:

![](images/5.%20System%20Objects%20Misc%20Issues.010.png)

When you very much customize the system interface, you do not always have a standard notation for a consult of the system interface anymore. Giving a related object’s __Get Object__ and __Set Object__ a parameter, you have to display the system interface all the time.

![](images/5.%20System%20Objects%20Misc%20Issues.011.png)

This shows, that the related __Pressure__ object has a __Time__ parameter.  
In this case the whole system interface is extended with a parameter, because the __Time__ parameter is not shown in a specific system command or specific system aspect, but shown inside the whole system interface. This means, that with any system command you can supply the __Time__ parameter.

A call to the system command, such as value assignment, will show the __Time__ parameter:

![](images/5.%20System%20Objects%20Misc%20Issues.012.png)

The notation above might not the best one. You may want to show the __Time__ parameter in the related object’s system interface at all times:

![](images/5.%20System%20Objects%20Misc%20Issues.013.png)

This clearly depicts, that the __Pressure__ related object has a __Time__ parameter. You can not go around this parameter.

### Referrers

#### Object Referrers

##### Concept

Objects can have references to other objects. A referenced object may not aware of its referrers, but it might be an option to explore for an object to have all its referrers registered in a list.

`The*` referrers `are not* the*` parents `containing the*` references to `the*` object, `but* the*` referrers `are the*` *references* to `the*` object `themselves`.

`When*` a related item `is set to point` to a `certain` object, `the*`  __Related Item  .  Object  .  Set__  command `will` update `the*` target’s list of __Referrers__. `So the*` *referrers* `update the*` target’s __Referrers__ list. `The*` referenced object `does not*` update `the*` __Referrers__ list `itself`.

`The*` __Referrers__ list `consists` of references *back* to `the*` referrers, `but*` that `does not* mean the*` object `in turn becomes` a referrer of `the*` referrer `again`.

An object `can* have` a referrers list, `but*` an object reference, `so` a related item or related list item (see `the*` *System Interfaces* articles), `can*` also `have` its `own` referrers list for references that `refer` to references.

###### `Not*` Supporting `the*` Referrers Concept

An object `could*` choose `not*` to support `the*` __Referrers__ concept, `if* the*` programmer `knows,` that `this` object `will` be referenced `so many` times, and there `is so little interest` in `knowing all` its referrers, that it `would*` be `ridiculous` maintain a list.

`But* by default, the*` __Referrers__ concept `is always` supported.

##### Diagram Notation

`The*` referrers of an object `are simply` displayed as a sub-list called __Referrers__, `every` item of which `points` back to `the*` references to `the*` object:

![](images/5.%20System%20Objects%20Misc%20Issues.014.png) 

`The*` entry in `the*` __Referrers__ list `is` pointing to a related item in `the*` parent object __A__, `not* directly` to an object.

`The*` lines `coming out` of `the*` referrers list `are usually not*` shown, `because*` a line `tied *to*` an object `already *implies*` a referrer. `The*` diagrams `will have more` features `later`, and the referrer lines `would* obscure the*` picture.

![](images/5.%20System%20Objects%20Misc%20Issues.015.png)

`Even the* whole` referrers list may `even` be `left out` of `the*` diagram `by default, but*` it `is not* clear yet, if*` that `is the* way to go`.

`If*` something `refers` to a reference, `then* this` may look `like this` in a diagram:

__b__ in __A__ `is` a reference to `the*` reference to __c__ inside __B__. `To display the*` referrers in `the*` diagram, `you* could*` < > `do` something `like this` < >:

![](images/5.%20System%20Objects%20Misc%20Issues.016.png)

![](images/5.%20System%20Objects%20Misc%20Issues.017.png)

#### Class Referrers

##### Concept

`The*` *Referrers* article `explained how` an object `can*` be `made aware` of its referrers. A *class* `can* also` be `made aware` of `the*` objects `using` it as a class.

~Classes `are` implemented as an aspect.~ That concept `adds` an object reference to `the*` system interface. `This` object reference `points out` which other object `is` its class. `So oddly`, an object reference, that `points` out `the*` class, `is already` added to `the*` class’s list of referrers. `The*` classes `are registered` inside `the* same` list of referrers as object referrers. `This is actually just fine. The*` __Referrers__ list `is supposed to be` a `low-level` view on `the*` referrers.

A class `is usually only` *used* as a class, and `not* also used` as an object, `so in practice, the*` __Referrers__ list of a class, `actually already *is*` a list of class referrers. `So` a `separate` list of __Class Referrers__ `will not*` be `implemented`.

`But* if*` in `the* future` there `is` a `need` to `also maintain` a `separate` list of class referrers, a `separate` __Class Referrers__ concept `could*` be `implemented. In that case, when*` a related item’s *class* `is` set, `the*` __Related Item  .  Class  .  Set__ `will` update `the* target`’s list of __Class Referrers__.

###### `Not*` Registering Class Referrers

`The*` amount of referrers of a __Number__ *object* may be `small, but* the*` amount of referrers of `the*` __Number__ *class* `is humungous. The*` class `will even have` a __Referrers__ list, `when* the*` class `is not*` a created object, `because*` __Referrers__ `applies` to `both` symbols and objects.

`You* would* want to` turn `the*` __Referrers__ concept `*off*` for `the*` __Number__ class and *on* for __Number__ objects. `But* the* problem here is`, that a class `is` a blueprint for an object. An object `only supports` __Referrers__, `because* the*` *class* `supports` it.

`The* first solution proposed was` to `simply not* support the*` __Referrers__ concept for classes that `are widely` used. `But* then*` for `widely` used classes, `the*` __Referrers__ concept `never` be `supported`. That `is against the*` idea of `supporting the*` __Referrers__ concept `by default`.

`If* you* can* not* stop` a class from `supporting` __Referrers__ `without stopping` objects from `supporting` __Referrers__ at `the* same time, then* the*` __Referrers__ concept `will not*` be `widely` used `anymore`.

`Therefore, you* are` going to `have to specify` for a symbol or object, that it `is` a non-practitioner of a concept. Derivation of objects `will` take over `the* specified` concept, `but* not* the*` non-practitioner aspect. Or perhaps instead of calling it non-practitioner, `you* could*` call it __Objects Support Concept Referrers__, or something.

##### Diagram Notation

< `The*` notation of a reference to an object reference’s class `needs to be determined` in `the* future`. >

`Because* the*` concept of referrers `simply also functions` as `the*` concept of class referrers, it `can*` be displayed in a diagram `the* same way, except`, that classes and class references `are` displayed with dashed lines.

![](images/5.%20System%20Objects%20Misc%20Issues.018.png)

`The*` reference line of `the*` item in `the*` __Referrers__ list `is` displayed, `then*` it `has to` point to `the*` class redirection of symbol __b__. There `is no final` notation `yet` for a to something `else’s` class. `But*` a preliminary notation `could* either` be a reference to `the*` __Class__ inside __b__’s system interface:

![](images/5.%20System%20Objects%20Misc%20Issues.019.png)

`Or` a reference line `connected` to __b__’s class line:

![](images/5.%20System%20Objects%20Misc%20Issues.020.png)

`The*` referrers `are` pointed at by solid lines, `because*` they `are just` references to `the*` objects, that `use` it as a class. `No implicit` notation of `making the*` referrer lines *dashed* `will` be used `here, because*` that `will` introduce `too much ambiguity` in `the*` diagram `notation`.

As `mentioned` in `the*` article *Referrers*, it `is not* clear yet` under which circumstances `the* whole` referrers list might be `completely` left out of `the*` diagram.

`If*` a class `defines` that its objects `support` __Referrers__, `but* the*` class `itself won’t` register its __Referrers__, `then* the*` Referrers list of `the*` class `will` be drawn out with dashed lines.

![](images/5.%20System%20Objects%20Misc%20Issues.021.png)

`Obviously, the*` inactive referrers list `will not* contain any` object references.

#### Referrers Versus Related Objects

Referrers `are` handy, `when* so many` classes relate to another class, that `the*` other class does `not*` want to maintain a separate list for `each` class that links to it.

It `is` also handy for `when*` a class `can't*` be aware of its related classes, `so can* not*` automatically get a relation back to classes, that want to link to it. In that case `the*` other class `can* not*` establish a dual relation with `the*` remote class, probably, `because*` it does `not* have` permission to alter `the*` remote class. Or `the*` remote class denies dual relationships to it altogether.

To make `the*` remote class or object aware of its referrers anyway, `you* can*` let it support `the*` referrers concept.

#### `The*` Referrers Concept

A __Number__ class `could*` choose to support `the*` __Referrers__ concept. `This will` give a __Number__ object `only` one list of `all` referrers, instead of a separate list for `every` class that uses __Numbers__. __Numbers__ may be used by `many` classes, `but*` an individual __Number__ object, `is` never used `much`. It `is not*` a `lot` of data to register inside an __Number__ object, which objects refer to that particular __Number__.

`But* then* the*` __Number__ class `will` also register `all` its *class referrers*, which `is` undoable, `because*` a humongous amount of objects refer to `this` class. `But*` a solution for `this was already` proposed by `the*` article *Class Referrers*. `You* can*` choose for a class to `not*` register its class referrers, while objects do register their referrers.

### Loose Ideas

#### Loose Ideas about Referrers

Taken out of `the*` Referrers article:

< Compared to giving a number class a related list for `every` class that uses integers >

A number class `could*`, however, choose to support a single list of `all` referrers. `Then*` a number object `will have only` one related list. Numbers may be used by `many` classes, `but*` an individual number object, `is` never used `much`. It `is not*` a `lot` of data to register inside an integer object, which objects refer to that particular number.

JJ

-----

Referrers,  
2008-08-10

`The*` Referrers concept `needs to be` redone. Consider `the*` system interface and make `sure you* can*` register referrers in a reference, as well as referrers to an object, and consider whether `you*` want `the*` referrers list to point to references or `the*` parents of `the*` references. `The*` article Referrers in a Diagram, Class Referrers in a Diagramand Command Definition Referrers in a Diagram `are` involved.

`I was` looking at `the*` Refferes diagrams. It’s `not*` correct. `The*` referrers list registers `the*` parents of `the*` references. `I`’m thinking now: they `should` register `the*` references themselves. `I must have` been that `I was` unaware of `the*` workings of `the*` system interface back `then*`...

JJ

-----

Referrers,  
2008-08-28

Referrers `has to be` redone. It `has to` become a list of related items and related list items, that they `are` inside their parents.

Redoing Referrers `was` postponed in `the*` project Work Out Basic Command Articles, `because*` it involves `too much` other material, that takes `too much` time to go into.

Referrers `is` mainly part of Relations.  
`You* are` probably going to `have to` read over `the*` whole Relations article group.

`The*` following articles may `have to be` redone, `when*` redoing Referrers:

- Referrers
- Referrers in a Diagram
- Class Referrers
- Class Referrers in a Diagram
- Referrers Versus Related Objects
- Command Object Referrers
- Command Object Referrers in a Diagram
- Command Definition Referrers
- Command Definition Referrers in a Diagram

JJ

-----

Referrers,  
2008-08-28

`The*` referrers articles `are not* finished`, because referrers `needs to be` reconsidered later, and it involves `much` different material, that takes time to go into.

- `I` hate it, that `I could* not* finish the*` referrers articles.
- `But*` it `is too much` to go into `just like` that.
- `I have to` accept that `the*` produced article group `will` contain two subjects, that `are not* finished`.

JJ

-----

Referrers,

Referenties naar een copy functie wil je ook niet in de in de copy command definitie zelf bijhouden. Maar je zou wel de mogelijkheid willen hebben om te querien welke kopieeracties er binnen een bepaald systeem zijn. Je kunt altijd een ruwe sequentiële zoek-query uitvoeren op een subsysteem. Maar je wilt het misschien ook centraal bijhouden. Dan zou je een filter index moeten kunnen maken, maar een filter index gezet op een elders gedefinieerde method of class.

Ik heb er toch best moeite mee, dat je in een stuk diagram niet ziet wat er allemaal naar een bepaald object verwijst, maar alleen waarnaar de objecten in de diagram verwijzen. O, wacht, dat gebeurt voor objecten wel, omdat de gerelateerde objecten als sub objecten worden getoond. Heen en weer relaties tussen objecten in principe gelijkwaardig. Maar bij methods `is` het anders. Die hebben altijd een richting, en de relatie terug `is` echt de backwards verwijzing.

Het `is` zeg maar een kwestie van 'belachelijk om allemaal bij te houden'.

Alleen soms wil je voor een definitie, die zijn referrers niet bijhoudt, toch referrers bijhouden.

Eigenlijk moet dan een systeem de referrers naar een definitie van een ander systeem bij kunnen houden.

Je maakt bij methods eigenlijk ook relaties tussen method definitions aan. Die zouden dan ook referrers bij kunnen houden, en een gesynchroniseerde relatie aan kunnen gaan.

JJ