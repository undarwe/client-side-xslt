Кросс-браузерная работа с XML
=============================

Почти вся кросс-браузерность сводится к двум вариантам: IE и все остальные.


Создание пустого xml-документа
------------------------------

### IE

    var xml = new ActiveXObject( pid );

Где pid это один из id-шников из следующего списка:

    var pids = [ "Msxml2.DOMDocument.6.0", "Msxml2.DOMDocument.5.0", "Msxml2.DOMDocument.4.0", "Msxml2.DOMDocument.3.0", "Msxml2.DOMDocument" ];

Согласно этой статье http://blogs.msdn.com/xmlteam/archive/2006/10/23/using-the-right-version-of-msxml-in-internet-explorer.aspx
имеет смысл использовать в реальной жизни только два pid'а из этого списка: `Msxml2.DOMDocument.6.0` и `Msxml2.DOMDocument.3.0` ---
первый это самый свежий, безопасный, соответствующий стандартам и т.д., а второй --- максимально распростаненный.

Выбираем максимально "свежий" из доступных pid'ов:

    var pids = [ "Msxml2.DOMDocument.6.0", "Msxml2.DOMDocument.3.0" ];
    var xml;
    for (i = 0; i < pids.length; i++) {
        try {
            xml = new ActiveXObject( pids[i] );
            break;
        } catch (e) {}
    }

TODO: Ссылка на msdn

### Не IE

    var xml = document.implementation.createDocument("", "", null);

Ссылка: https://developer.mozilla.org/En/DOM/DOMImplementation.createDocument


Создание xml-документа из строки
----------------------------

### IE

    var xml = .... // создать пустой xml-документ
    xml.loadXML("<page>Hello, World!</page>");

TODO: Ссылка на msdn

### Не IE

    var domparser = new DOMParser();
    var xml = domparser.parseFromString("<page>Hello, World!</page>", "text/xml");

Ссылка: https://developer.mozilla.org/en/DOMParser


Сериализация xml-документа в строку
-----------------------------------

### IE

    var strXML = xml.xml;

TODO: Ссылка на msdn

### Не IE

    var serializer = new XMLSerializer();
    var strXML = serializer.serializeToString(xml);

Ссылка: https://developer.mozilla.org/en/XMLSerializer


Загрузка xml-документа с удаленного ресурса
-------------------------------------------

Можно грузить, например, через jQuery.get.

    var xml;
    $.get("http://mysite.com/my.xml", function(data) {
        xml = data;
    }, "xml")


