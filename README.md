JavascriptClassBundle
=====================

# IMPORTANT!

Generate javascript mootools classes providing xhr-managed persistence for an entity in a bundle from its yaml mapping.

This bundle is **NOT finished nor working** right now. Its would-be aim is to provide
a generated doctrine-like environment in javascript based on the same mapping.
However, its realistic, first-release aim will *not* provide an Entity Manager nor support for Entity Associations.
Therefore, for now, only basic stuff like accessors and mutators for Entity fields.

Also, authentication and security are inexistant.


Oh, and almost no Tests either... \\(°ö°)/ !


# Installation

### Get the bundle

To install the bundle, place it in the `src/Nutellove` directory of your project
(so that it lives at `src/Nutellove/JavascriptClassBundle`). You can do this by adding the bundle as a submodule,
cloning it, or simply downloading the source.

    git submodule add git://github.com/Nutellove/JavascriptClassBundle.git src/Nutellove/JavascriptClassBundle

### Add the namespace to your autoloader

If it is the first Nutellove bundle you install in your Symfony 2 project, and it is, because there is only one, you
need to add the `Nutellove` namespace to your autoloader:

    // app/autoload.php
    $loader->registerNamespaces(array(
        'Nutellove'                       => __DIR__.'/../src'
        // ...
    ));

### Initialize the bundle

To start using the bundle, initialize the bundle in your Kernel. This
file is usually located at `app/AppKernel`:

    public function registerBundles()
    {
        $bundles = array(
            // ...
            new Nutellove\JavascriptClassBundle\JavascriptClassBundle(),
        );
    )



# TODO

There are **many** things to do to improve this Bundle, such as :

* Release
  * Use options in config
* Cleaning up my student code :p
  * Create a JavascriptClassBundle git repo (done)
  * Create a JavascriptClassTestBundle git repo
  * Use git submodules (done)
  * Validate [the guidelines](http://docs.symfony-reloaded.org/guides/bundles/best_practices.html) except for spaces
  * Writing up Tests (I swear I'll take time to write some, and then some more)
  * Mootools ≥ 1.3 in dependencies (Quote : A bundle should not embed third-party libraries written in JavaScript)
* Next
  * Abstract Class for all Generators (code refactorization)
  * Writing a command that does all the Entities within a Bundle
* Future
  * Adding new JS Entity Classes :
    * Pure JS (CoffeeScript <3 except for implement)
    * jQuery
   * Authentication, User rights management, Security. Think.
   * JS Entity Manager
  * Minifying => Assetic :)
  * Collections
  * Entity Associations
    * One-to-One
      * Unidirectional
      * Bidirectional
      * Self-referencing
    * One-to-Many
      * Unidirectional with Join Table
      * Bidirectional
      * Self-referencing
    * Many-To-One, Unidirectional
    * Many-to-Many
      * Unidirectional
      * Bidirectional
      * Self-referencing


# USAGE

## MAPPING

In your ORM mapping, you must provide for each field a `js` attribute under the `options` attribute, with one of the following values.

Possible values for `js` are :

* for reading only :
  * read
  * r
* for writing only :
  * write
  * w
* for reading and writing :
  * readwrite
  * rw

## COMMANDS

    $ app/console jsclass:generate:entity <bundle> <entity>

Replace `<bundle>` and `<entity>` by the names of the Bundle and Entity you want to
generate the Mootools Classes of.

## WHAT IS IT?

Each Doctrine 2 Entity converted to Mootools will need a total of 6 files :

### Javascript Mootools Classes

* `Nutellove/JavascriptClassBundle/Resources/js/BaseEntityAbstract.class.js` is a static (non-generated) Class that holds the XHR magic
* `Entity/Mootools/Base/Base<Entity>.class.js` is a generated Mootools Entity Base Class that extends the above BaseEntityAbstract Class, you should *not* manually edit this file
* `Entity/Mootools/<Entity>.class.js` extends the above Base class, is initially generated (almost) empty and not overwritten, so you might write your custom logic inside

### PHP AJAX Controllers

* Abstract (shared by all Controllers)
* Base (re-generated each time)
* Final (initially empty, then custom) <- Editing only this !

NOTE : In the above paths, `<Entity>` is your Entity Name, without namespace. (may cause problems!)

Therefore, the first time you execute the command-line for a given Bundle/Entity pair, 4 files will be generated.
After that, only the 2 Base files will be re-generated.


## DEVCOMMENT

    $ app/console_dev doctrine:generate:entities JavascriptClassBundle

    $ app/console_dev doctrine:schema:create

    $ app/console_dev assets:install web


## WHY MOOTOOLS FIRST ?

Easy. ;)

## THANKS

- Fabien Potencier, for he taught me *a lot*
- Jonathan Wage, cause he's awesome too
- Aaron Newton, kudos to his super-cow-powers
- *You*, sneaky FOSS lover !

## FREE, as in free (b|sp)ee(ch|r)

**The Carcase**

The object that we saw, let us recall,  
This summer morn when warmth and beauty mingle —  
At the path's turn, a carcase lay asprawl  
Upon a bed of shingle.  

Legs raised, like some old whore far-gone in passion,  
The burning, deadly, poison-sweating mass  
Opened its paunch in careless, cynic fashion,  
Ballooned with evil gas.  

On this putrescence the sun blazed in gold,  
Cooking it to a turn with eager care —  
So to repay to Nature, hundredfold,  
What she had mingled there.  

The sky, as on the opening of a flower,  
On this superb obscenity smiled bright.  
The stench drove at us, with such fearsome power  
You thought you'd swoon outright.

Flies trumpeted upon the rotten belly  
Whence larvae poured in legions far and wide,  
And flowed, like molten and liquescent jelly,  
Down living rags of hide.  

The mass ran down, or, like a wave elated 
Rolled itself on, and crackled as if frying: 
You'd think that corpse, by vague breath animated, 
Drew life from multiplying.

Through that strange world a rustling rumour ran 
Like rushing water or a gust of air, 
Or grain that winnowers, with rhythmic fan, 
Sweep simmering here and there. 

It seemed a dream after the forms grew fainter,  
Or like a sketch that slowly seems to dawn 
On a forgotten canvas, which the painter 
From memory has drawn. 



Behind the rocks a restless cur that slunk 

Eyed us with fretful greed to recommence 

His feast, amidst the bonework, on the chunk 

That he had torn from thence.



Yet you'll resemble this infection too 

One day, and stink and sprawl in such a fashion, 

Star of my eyes, sun of my nature, you, 

My angel and my passion!



Yes, you must come to this, O queen of graces, 

At length, when the last sacraments are over, 

And you go down to moulder in dark places 

Beneath the grass and clover.



Then tell the vermin as it takes its pleasance 

And feasts with kisses on that face of yours, 

I've kept intact in form and godlike essence 

Our decomposed amours!


— Roy Campbell, Poems of Baudelaire (New York: Pantheon Books, 1952)


# ESSAY

Associate this scene to children watching the adults' world.

I want your copies by the end of the semester.