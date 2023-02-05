## Домашнее задание по теме «JVM. Организация памяти, сборщики мусора, VisualVM»

### Задание
### Просмотрите код ниже и опишите (текстово или с картинками) каждую строку с точки зрения происходящего в JVM
### Не забудьте упомянуть про:
* ClassLoader’ы,
* области памяти (стэк (и его фреймы), heap)
* сборщик мусора

``` java
public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}
```

`public class JvmComprehension {`
// Класс JvmComprehension отдаётся для загрузки в систему загрузчиков классов (ClassLoader'ов);
// Далее информация о классе JvmComprehension (имя, методы, поля и т.д.) передаётся в область памяти Metaspace;

`public static void main(String[] args) {`
// При вызове метода main, создается фрейм в Стэке.

`int i = 1;`      
// 1. Во фрейме main создается переменная i со значением 1.

`Object o = new Object();     `   
// 2. В heap(куче) создается объект Object и во фрейме main создается переменная o,
// которой присваивается ссылка на этот объект

`Integer ii = 2;`             
// 3. В heap(куче) создается объект Integer со значением 2,а во фрейме main появляется переменная ii со ссылкой на этот объект

`printAll(o, i, ii);`             
// 4. будет создан фрейм, метода printAll() в области памяти Stack Memory,
// а в разделе Stack во фрейме printAll() будет сохранена ссылки «о»и «ii»,
// которые будут ссылаться на Object и Integer,также в Stack будет сохранено значение int i

`System.out.println("finished");`
// 7. В Стэке создается фрейм println,
// которому передается ссылка на созданный в Куче объект String со значением "готово".
// В ходе работы программы отрабатывает Garbage Collector.

`private static void printAll(Object o, int i, Integer ii) {`
`Integer uselessVar = 700;`
// 5. В heap (куче) создается объект Integer со значением 700,
// а во фрейме printAll появляется переменная uselessVar со ссылкой на этот объект.

`System.out.println(o.toString() + i + ii);`
// 6. В Stack'е создается фрейм println, куда передаются ссылки на Object o, int i и Integer ii.
// В Stack'е создается фрейм toString.
