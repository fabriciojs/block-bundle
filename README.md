# Symfony Cmf Block Bundle
## What is this?
This Bundle is part of the [Symfony CMF](http://cmf.symfony.com/). It assists you in managing fragments of contents, so called blocks. What the SymfonyCmfBlockBundle does is similar to what Twig does, but for blocks that are persisted in a DB. Thus the blocks can be made editable for an editor. Also the SymfonyCmfBlockBundle provides the logic to determine which block should be rendered on which pages.

## What is this not?
The SymfonyCmfBlockBundle does not provide an editing functionality for blocks itself. However, you can find examples on how making blocks editable in the [Symfony CMF Sandbox](https://github.com/symfony-cmf/cmf-sandbox).

## Usage
### Installation / Dependencies

Dependencies of the SymfonyCmfBlockBundle are managed by [Composer](https://github.com/composer/composer), so if you use Composer, you just have to add a requirement for ```symfony-cmf/block-bundle``` to your composer.json and run the composer installer. Otherwise check ```composer.json``` and add the required dependencies to your ```deps``` file.

After this, instantiate the bundle in your ```AppKernel.php```

    new Symfony\Cmf\Bundle\BlockBundle\SymfonyCmfBlockBundle()

Since the SymfonyCmfBlockBundle extends the SonataBlockBundle (see [Technical details](#technical-details) for further information), also add this to your ```AppKernel.php```

    new Sonata\BlockBundle\SonataBlockBundle()

### Render your first block
Before you can render a block, you need to create a data object representing your block in the repository. You can do so with the following code snippet (Note that ```$parentPage``` needs to be an instance of page defined by the [SymfonyCmfContentBundle](https://github.com/symfony-cmf/ContentBundle)):

    $myBlock = new SimpleBlock();
    $myBlock->setParentDocument($parentPage);
    $myBlock->setName('sidebarBlock');
    $myBlock->setTitle('My first block');
    $myBlock->setContent('Hello block world!');

    $documentManager->persist($myBlock);

'sidebarBlock' is the identifier we chose for the block. Together with the parent document of the block, this makes the block unique. The other properties are specific to ```Simpleblock```.
Now to have this block actually rendered, you just add the following code to your Twig template:

    {{ sonata_block_render({
        'name': 'sidebarBlock'
    }) }}

This will make the SymfonyCmfBlockBundle rendering the according block on every page that has a block named 'sidebarBlock'. Of course, the actual page needs to be rendered by the template that contains the snippet above.

### Block types
The SymfonyCmfBlockBundle comes with four general purpose blocks:
* __SimpleBlock__: A simple block with nothing but a title and a field of hypertext. This would usually be what an editor edits directly, for example contact information
* __ContainerBlock__: A block that containes 0 to n child blocks
* __ReferenceBlock__: A block that references a block stored somewhere else in the content tree. For example you might want to refer parts of the contact information from the homepage
* __ActionBlock__: A block that calls a Symfony2 action. "Why would I use this instead of directly calling the action from my template?" you might wonder. Well imagine the following case: You provide a block that renders teasers of your latest news. However, there is no rule where they should appear. Instead, your customer wants to decide himself on what pages this block is to be displayed. Providing an according ActionBlock, you allow your customer to do so without calling you to change some templates (over and over again!).

### Create your own block

## Examples
You can find example usages of this bundle in the [Symfony CMF Sandbox](https://github.com/symfony-cmf/cmf-sandbox). Have a look at the BlockBundle in the Sandbox. It also shows you how to make blocks editable using the [LiipVieBundle](https://github.com/liip/LiipVieBundle).

## Technical details
### Sonata Block Bundle


### Tests
The components of the SymfonyCmfBlockBundle are unit tested. You can run the tests with ```phpunit -c .``` in the root directory.

## Authors
* [Alain Horner](https://github.com/elHornair)
* [Uwe Jäger](https://github.com/uwej711)
* [David Buchmann](https://github.com/dbu)
* [Lukas Kahwe Smith](https://github.com/lsmith77)
* [And others](https://github.com/symfony-cmf/BlockBundle/contributors)
