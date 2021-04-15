JimToolbox, conception notes
================
2021-04-15




Jim tool box is a toolbox located on the side of screen. You can click its different tabs to expand the corresponding panels.





Screenshots
======
2021-04-15


### Collapsed
![jimtoolbox collapsed](https://lingtalfi.com/img/universe/JimToolbox/jimtoolbox-collapsed.png)


### Expanded
![jimtoolbox expanded](https://lingtalfi.com/img/universe/JimToolbox/jimtoolbox-expanded.png)





How does it work
==========
2021-04-15



JimToolbox require a certain html markup to function properly.



Here is how it works (note that both our js and css files are required):


```php

<?php

$nbItems = 4;

?>

<div class="jim-toolbox toolbox-close">
    <div class="toolbox-toggle">


        <div class="toolbox-toggle-top d-flex flex-column justify-content-center align-items-center mb-1">
            <i class="far fa-plus-square text-toggle-plus"></i>
            <i class="far fa-minus-square text-toggle-minus"></i>
            <i class="fas fa-arrow-up mt-3 arrow-icon arrow-icon-up"></i>
        </div>

        <div class="toolbox-toggle-container">

            <div class="toolbox-toggle-container-slider">

                <?php for ($i = 1; $i <= $nbItems; $i++): ?>


                    <div class="toolbox-toggle-item" title="Module <?php echo $i; ?>"
                         data-target="module-<?php echo $i; ?>">

                        <i class="fab fa-accusoft"></i>
                        <div class="toolbox-toggle-item-name">Option <?php echo $i; ?></div>
                    </div>
                <?php endfor; ?>
            </div>
        </div>

        <div class="d-flex justify-content-center mt-1">
            <i class="fas fa-arrow-down arrow-icon arrow-icon-down"></i>
        </div>
    </div>

    <div class="toolbox-panel">


        <div class="toolbox-content">


            <?php for ($i = 1; $i <= $nbItems; $i++): ?>

                <div class="toolbox-module" data-id="module-<?php echo $i; ?>">
                    <div class="toolbox-title">
                        <button type="button" class="close float-right toolbox-close-btn" aria-label="Close">
                            <span aria-hidden="true">×</span>
                        </button>

                        <h4 class="mb-0 d-inline-block">Module <?php echo $i; ?></h4>
                    </div>

                    <div class="toolbox-body">
                        My module #<?php echo $i; ?>
                    </div>
                </div>

            <?php endfor; ?>

        </div>
    </div>
</div>


<script>

    document.addEventListener("DOMContentLoaded", function (event) {
        $(document).ready(function () {


            var jToolbox = $('.jim-toolbox');
            JimToolbox.init({
                context: jToolbox,
            });
        });
    });

</script>
```



In the above example, we used the **div.jim-toolbox** as the context.

The **jim toolbox** as a combination of
two elements:

- the toggle
- the panel



The toggle is the part you see when the jim toolbox is collapsed,
while the panel is the part you see when the toolbox is expanded (see the screenshots above).

The toggle itself is composed of items, each of which contains a text and an icon.

When you click a **toggle item**, the corresponding **module** opens in the panel.


One has to make sure that the **data-target** attribute of the **toggle item** matches the **data-id** attribute of the **module**.  


### Useful css classes
2021-04-15


- **toolbox-close**: apply this css class to your context to hide the toolbox (it's open by default) 
- **toolbox-close-btn**: inside a module, use this class to close the module




### The js options
2021-04-15


The **jim toolbox** comes with the following options for the **init** method:


- context: jquery element, required, the context in which the toolbox is contained
- useToggleShortcut: bool=true, whether to allow a shortcut to toggle the visibility of the toggle
- toggleShortcutKey: string=t, assuming that useToggleShortcut=true, the key to type to actually toggle the toolbox's visibility
        Note that if a module is opened in the panel, the shortkey will close the panel first (i.e. a second
  stroke on the shortcut key is required to hide the toggle as well).



