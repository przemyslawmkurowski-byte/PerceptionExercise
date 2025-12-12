# PerceptionExercise

Celem tego ćwiczenia jest rozpoznanie sposobu działania Perception Component, po kanale Sight.

## Punkt wyjścia:

Aerith i Bob stoją naprzeciwko siebie, patrząc w swoim kierunku. Pomiędzy nimi jest ściana. Controllery obu Characterów mają PerceptionComponent z włączonym zmysłem Sight, oba też są tak spreparowane, aby raportować do blueprinta levelu zmiany w percepcji. Zapominanie jest ustawione na 5 sekund.

## Testy

1. Ukrywam ścianę. W tym momencie Aerith powinna zaraportować, że widzi Boba.

2. Jak wyżej. Następnie odkrywam ścianę. Aerith powinna zaraportować, że nie widzi Boba.

3. Jak wyżej. Następnie czekam 10 sekund. W tym czasie Aerith powinna zaraportować, że zapomniała Boba.

4. Dla pewności: jak wyżej, ale czekam tylko 3 sekundy. Aerith nie powinna zdążyć zapomnieć Boba.

~~5. Każę Bobowi uklęknąć. Następnie obniżam ścianę, ale tylko do takiego stopnia, żeby Boba nie było widać z perspektywy Aerith. Aerith nie powinna zaraportować, że zaobserwowała Boba.~~

~~6. Jak wyżej, ale ściana jest tak ustawiona, że Boba widać od głowy Aerith (ale nie tułowia). Aeirth powinna zauważyć Boba.~~

~~7. Odsłaniam ścianę, ale tak, żeby Bob był częściowo widoczny. Nakazuję Bobomi kucnąć. Aerith powinna zaraportować, że zgubiła Boba.~~

## Wnioski

1. Ukrycie ściany nic nie zmienia, obwiniam to, że ściana nadal koliduje z kanałem visibility. Nie jest to przedmiotem testu, więc zamiast szukać obejścia, po prostu zmieniam metodologię testów z "ukrywam scianę" na "przesuwam ścianę 5 metrów w dół"
2. Zapominanie działa, ale wymaga ustawienia flagi projektowej Forget Stale Actors. Dlaczego tak? Czy Epic zakłada, że zapominanie powinno być robione ręcznie (na co wskazywałby tutorial percepcji)?
3. Test drugi działa, o ile między odblokowaniem, a zablokowaniem LoS jest odpowiednio długi delay (jedna klatka to za mało, 0.2s to dostatecznie dużo). Sugeruje to, że percepcja odświeża się we własnym ticku, rzadszym od gameplay ticku, ale częstszym niż 5Hz. Czyli bez zaskoczeń.
4. Testy numer 5-7 są bezprzedmiotowe. Trace zostaje wypuszczony z okolic szyi Aerith do transformu Boba (nieco poniżej pasa). Oznacza to, że wystarczy zakryć Boba od pasa w dół, aby Aerith nie mogła go zauważyć - chociaż ma w zasięgu wzroku cały korpus i głowę Boba. Ewentualne skradanie, czajenie się za przeszkodami itd trzeba by robić niezależnie od PerceptionComponentu.

## Zamknięcie

Temat zamknięty.