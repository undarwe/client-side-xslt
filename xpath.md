Поддержка XPath
===============

Выборка одной или нескольких нод по xpath'у
-------------------------------------------

### IE

В IE все более-менее просто. У любой ноды есть два метода: `selectSingleNode` и `selectNodes`.

    var xml = ....;
    xml.loadXML("<page><data><id>1</id></data><data><id>2</id></data></page>");

    var first = xml.selectSingleNode("/page/data[1]"); // в first одна нода

    var data = xml.selectNodes("/page/data"); // в data нодесет из двух нод


### Не IE

    var xml = ....;

    var evaluator = new XPathEvaluator();

    var result;

    result = evaluator.evaluate("/page/data[1]", xml, null, XPathResult.FIRST_ORDERED_NODE_TYPE, null);
    var first = result.singleNodeValue; // в first одна нода

    data = evaluator.evaluate("/page/data", xml, null, XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);
    /*
        В data некий псевдо-массив, у которого есть свойство snapshotLength (длина "нодесета")
        и метод snapshotItem(i), возвращающий i-ый элемент нодесета
    */



