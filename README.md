Stream + Unit testing homework
==============================

A repóban a [stream-playground](https://github.com/jeszy75/stream-playground) projekt egy másolatát találod.

Bónuszfeladat: saját adatállomány feldolgozása
--------------

Egészítsd ki a a projektet egy új package-el, a `brickset`hez és a `countries`hoz hasonlóan. Helyezz el a `resources` mappában egy tetszőleges JSON adatállományt, és írj hozzá feldolgozó osztályokat.

JSON adatállomány kereséséhez az alábbi listák a segítségedre lehetnek:

* [Public APIs](https://github.com/public-apis/public-apis)
* [Awesome JSON Datasets](https://github.com/jdorfman/awesome-json-datasets)

Természetesen nem kötelező ebből a listából választani, viszont a Feedback pull requestben kérlek jelöld meg az általad felhasznált adatállomány forrását.

__Fontos:__ csak olyan adatállomány fogadható el, amely hasonlóan összetett, mint a `countries.json` vagy a `brickset.json`. Nem elfogadható például a [How Many People Are In Space Right Now](http://api.open-notify.org/astros.json) adatállomány, mivel túl kevés tulajdonságot tartalmaz.

Stream feladat
---------------

Ha a bónuszfeladatot kihagytad, dolgozz a `brickset` package-el.

Adj hozzá az általad létrehozott package Repository osztályához __5 különböző metódust__, melyek az adatállományról szolgáltatnak hasznos információkat. A metódusoknak a céljukat világosan kifejező __értelmes neveket__ kell adni, mint például `countLegoSetsWithTag()`. A metódusok közül __legalább 3-nak__ szükséges, hogy __legalább egy paramétere__ legyen. Minden egyes metódus egy __értéket kell, hogy visszaadjon__, a konzolra íratás nem megengedett. A metódusok törzsének pontosan egy *stream* csővezetéket kötelező tartalmazni. A csővezeték egy `return` kulcsszót kell, hogy kövessen. Minden metódushoz kötelező egy azt megfelelően dokumentáló Javadoc megjegyzés. Megfelelő Javadoc megjegyzés nélküli metódusok nem kerülnek elfogadásra.

Példa:
```java
import repository.Repository;

/**
 * Represents a repository of {@code LegoSet} objects.
 */
public class LegoSetRepository extends Repository<LegoSet> {

    public LegoSetRepository() {
        super(LegoSet.class, "brickset.json");
    }

    /**
     * Returns the number of LEGO sets with the tag specified.
     *
     * @param tag a LEGO set tag
     * @return the number of LEGO sets with the tag specified
     */
    public long countLegoSetsWithTag(String tag) {
        return getAll().stream()
                .filter(legoSet -> legoSet.getTags() != null && legoSet.getTags().contains(tag))
                .count();
    }

    // ...

}

```

Az 5 metódust az alábbi követelmények alapján szükséges implementálni:

1. Egy metódus hajtson végre paraméter alapján történő *szűrést*, visszatérési értéke pedig `List` típusú legyen.
2. Egy metódus tartalmazzon `flatMap` köztes műveletet. A visszatérési értéke legyen `List` típusú.
3. Egy metódus hajtson végre többszintű rendezést. A visszatérési típusa legyen `List`.
4. Egy metódus visszatérési értéke a `Map` interfész egy tetszőleges implementációja kell, hogy legyen. A map értékei legyenek atomi értékek.
5. Egy metódus visszatérési értéke a `Map` interfész egy tetszőleges implementációja kell, hogy legyen. A map értékei legyenek listák.

Unit testing feladat
--------------------

Add hozzá a `JUnit` keretrendszert a projekthez, illetve a [Maven Surefire Plugint](https://maven.apache.org/surefire/maven-surefire-plugin/usage.html).

A `JUnit`-ot használva írj unit teszteket a *Stream feladat*ban implementált metódusaidhoz. A paraméteres metódusokhoz [parametrizált teszteket](https://www.baeldung.com/parameterized-tests-junit-5) írj. A tesztmetódusok felépítésénél kövesd az órán szemléltetett *Given-When-Then* struktúrát.

---

A repó tartalmaz egy olyan *Github Actions workflow*t, amely a tárolóba való pusholás hatására buildeli a projektet, és lefuttatja a unit teszteket. Ezeket a futásokat a repó *Actions* menüjéből tudod elérni. Ennek a segítségével gyors visszajelzést kaphatsz arról, hogy a megoldásod buildhető-e egy független környezetben is.