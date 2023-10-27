# Integrating Party Town with WordPress

To get quickly started follow [this guide](https://partytown.builder.io/distribution) to learn how you should separate your files.

From that guide you should have the `/lib/` directory, rename this to `"~partytown"` and place this into the root of your WordPress site.

Once the directory is in the root of your WordPress site you are ready to setup the header file. Firstly you must make sure that you call the partytown script at the **very** top of your `header.php` file.

```html
<head>
    <script src="~partytown/partytown.js"></script>

    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <?php wp_head(); ?>
</head>
```

Party Town has to be the first script to run in order to run any other scripts inside a web worker. 

Next you will need to set up your [forwarding events](https://partytown.builder.io/forwarding-events). **This is an important step** as normally the script, that you are running from a web worker, will add code to the head but now is unable to since it's runing from a web worker. Forwarding will allow the scripts to run as intended. Take a look at the following example:

```html
<head>
    <script src="~partytown/partytown.js"></script>

    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <?php wp_head(); ?>

    <!-- Add forwarding event for Google Tag Manager -->
    <script>
        partytown = {
            forward: ['dataLayer.push'],
        };
    </script>
</head>
```

Once you have added your forwarding events you are ready to be adding your scripts, take a look at the following example:

```html
<head>
    <script src="~partytown/partytown.js"></script>

    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <?php wp_head(); ?>


    <script>
        partytown = {
            forward: ['dataLayer.push'],
        };
    </script>

    <script type="text/partytown">
        /*

            google tag manager

        */
    </script>
</head>
```

You will know your script is working correctly by seeing if the script you added with the `type="text/partytown"` attribute has `-x` added to the end of it.

**All of the code and directory structure can be seen in this repository for reference.**