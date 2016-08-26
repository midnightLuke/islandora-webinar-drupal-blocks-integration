# Islandora Templates
(...which are really just Drupal templates)


## What is a template?

- Drupal 6 & 7 use PHPTemplate (flat PHP)
- Variables are passed to the template
- Template renders variables for display in HTML
- Templates can be overridden for customization


## Islandora and Templates

- Most cModels ship with custom templates
- Different templates display different things
- Some flexibility (ie metadata displays with SOLR)
- Up to the solution pack developers to include things like:
  - Citations
  - Metadata displays
  - Datastream lists


## What does a template look like?

```php
<?php

/**
 * @file
 * This is the template file for the object page for basic image
 *
 * @TODO: add documentation about file and available variables
 */
?>

<div class="islandora-basic-image-object islandora" vocab="http://schema.org/" prefix="dcterms: http://purl.org/dc/terms/" typeof="ImageObject">
  <div class="islandora-basic-image-content-wrapper clearfix">
    <?php if (isset($islandora_content)): ?>
      <div class="islandora-basic-image-content">
        <?php print $islandora_content; ?>
      </div>
    <?php endif; ?>
  </div>
  <div class="islandora-basic-image-metadata">
    <?php print $description; ?>
    <?php if ($parent_collections): ?>
      <div>
        <h2><?php print t('In collections'); ?></h2>
        <ul>
          <?php foreach ($parent_collections as $collection): ?>
            <li><?php print l($collection->label, "islandora/object/{$collection->id}"); ?></li>
          <?php endforeach; ?>
        </ul>
      </div>
    <?php endif; ?>
    <?php print $metadata; ?>
  </div>
</div>
```

Notes:

- Point out the "parent collection" and "metadata" sections
  - All cModels have this, only some display it


## Pros/Cons

- **PRO**: Override-able for developers
- **CON**: Site builders are locked out
- **CON**: Relies on solution pack developers
