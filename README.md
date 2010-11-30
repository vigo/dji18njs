dji18njs
========

English
-------
**dji18njs** is a small internationalization and localization script. Original script can be found at : [here][django]

I tweaked and changed a lot. i hope you all like it! i've added some sample locale files and a test.html.

Here is the list of my tweaks:

*   Bind to **window.dji18njs**, dji18njs namespace 
*   You can set language by **dji18njs.lang_id**
*   **dji18njs.ngettext** re-written from scratch and changed
*   **dji18njs.interpolate** has changed and added "erroious notification"
*   **version** property

Usage
-----

Include the script as usual place, then add the locale file (or files). Default language is always **English** (en)

    <script src="dji18njs-1.1.js"></script>
    <script src="locale-tr.js"></script>

Catalog file looks like this:

    dji18njs.catalog.tr = {
    // english => turkish
        "key": 'value',
        "Hello world": 'Merhaba dünya',
    }

You can call it:

    dji18njs.gettext("Hello world"); // returns 'Merhaba dünya' 

Singular, plural solution:

    django.ngettext("ball", "balls", 5); // returns 'balls'
    django.ngettext("ball", "balls", 0); // returns 'ball'
    django.ngettext("ball", "balls", 1); // returns 'ball'

Interpolation or i call this **format string** in a python way!

    var strFormat = "Hello %s, you have %s %s in your pocket";
    dji18njs.interpolate(strFormat, ["vigo", 5, 'coins']);
    // returns 'Hello vigo, you have 5 coins in your pocket'

lets do this more complex!
    
    var strFormat = "Hello %s, you have %s %s in your pocket";
    var intCoin = 1;
    var strSingularPlural = dji18njs.ngettext("coin", "coins", intCoin);
    dji18njs.interpolate(strFormat, ["vigo", intCoin, strSingularPlural]);
    // returns 'Hello vigo, you have 1 coin in your pocket'

If the catalog exists:

    dji18njs.catalog.tr = {
        "coin": 'jeton',
        "coins": 'jeton',
        "Hello %s, you have %s %s in your pocket": 'Selam %s, cebinde %s tane %s var'
    };
    // the function above
    // returns 'Selam vigo, cebinde 1 tane jeton var'

Here comes my favourite. You can use **dji18njs** as a templating helper.

    var strFormat = "Hello %(username)s, your password is: %(password)s";
    var dicWords = {
        "username": 'vigo',
        "password": '1!2!3!'
    };
    dji18njs.interpolate(strFormat, dicWords, true);
    // returns 'Hello vigo, your password is: 1!2!3!'

For more details examples, please check: **test.html** file

[django]: http://code.djangoproject.com/browser/django/trunk/django/views/i18n.py "Title"
