dji18njs
========

English
-------
**dji18njs** is a small internationalization and localization script. Original script can be found at: [here][django]

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
        key: value,
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

Here comes my favorite. You can use **dji18njs** as a templating helper:

    var strFormat = "Hello %(username)s, your password is: %(password)s";
    var dicWords = {
        "username": 'vigo',
        "password": '1!2!3!'
    };
    dji18njs.interpolate(strFormat, dicWords, true);
    // you must pass true as 3rd argument to execute named object!
    // returns 'Hello vigo, your password is: 1!2!3!'

Here is an errorious "named interpolate" example:

    // string has %(user)s but there is no "user" in the object. it is "userx".
    // they don't match
    
    dji18njs.interpolate("Hello %(user)s in Turkish", { userx: "lego" }, true);
    
    // returns 'Hello ?%(user)s? in Turkish'

For more details examples, please check: `test.html` file

Türkçe
------

Django ile uğraşırken JavaScript için gördüğüm mükemmel çözüm yöntemini biraz tırtıkladım, sildim baştan yazdım ve çok işime yarayan basit bir script çıkarttım ortaya. Esin kaynağımı [buradan][django] inceleyebilirsiniz.

Benim hazırladığım bu versiyonda;

*   **window.dji18njs**, dji18njs namespace olarak çalışıyor.
*   **dji18njs.lang_id** özelliği ile dili belirleyebilirsiniz.
*   **dji18njs.ngettext** metodunu tamamen baştan yazdım.
*   **dji18njs.interpolate** metodunda hatalı kelime için işaret koyuldu.
*   **version** bilgisi eklendi.

Yapmanız gereken, html içinde, JavaScript'leri nereye koyuyorsanız, sırasıyla aşağıdaki dosyaları da aynı yere koymak:

    <script src="dji18njs-1.1.js"></script>
    <script src="locale-tr.js"></script>

Örnek katalog:

    dji18njs.catalog.tr = {
    // ingilizce => türkçe
        key: value,
        "Hello world": 'Merhaba dünya',
    }

Aşağıdaki gibi kullanınca;

    dji18njs.gettext("Hello world"); // sonuç 'Merhaba dünya' 

İngilizce'deki tekil/çoğul içinde çözüm var. Aslında sizin de bildiğiniz gibi, Türkçe'deki tekil/çoğul olayı İngilizce'den biraz daha farklı.

    django.ngettext("ball", "balls", 5); // sonuç 'balls'
    django.ngettext("ball", "balls", 0); // sonuç 'ball'
    django.ngettext("ball", "balls", 1); // sonuç 'ball'

Python'daki gibi "format string" tadında; 2 kullanım şekli var: dizi(Array) ya da sözlük/obje(dictionary/object):

    var strFormat = "Hello %s, you have %s %s in your pocket";
    dji18njs.interpolate(strFormat, ["vigo", 5, 'coins']);
    // sonuç 'Hello vigo, you have 5 coins in your pocket'


    var strFormat = "Hello %(username)s, your password is: %(password)s";
    var dicWords = {
        "username": 'vigo',
        "password": '1!2!3!'
    };
    dji18njs.interpolate(strFormat, dicWords, true);
    // "named object" olayını kullanmak için mutlaka 3.parametre olarak true geçin.
    // sonuç 'Hello vigo, your password is: 1!2!3!'

Daha fazla örnek ve bilgi için **test.html** dosyasına bakabilirsiniz.

[django]: http://code.djangoproject.com/browser/django/trunk/django/views/i18n.py "Title"
