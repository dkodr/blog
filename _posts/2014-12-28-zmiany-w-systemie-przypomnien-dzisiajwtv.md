---
published: true
title: Zmiany w systemie przypomnień @dzisiajwtv
tags: 'dzisiajwtv, przypomnienia, twitter'
---
### tl;dr

* System przypomnień już prawidłowo indeksuje wszystkie tweety; powinien działać dla każdego.
* Załatane zostały drobne błędy oraz dodane reakcje skryptu na literówki w komendzie oraz wysyłanie komend w odpowiedzi na tweety z minionych dni.
* Dodano możliwość indywidualnego wyznaczania czasu przypomnień. Składnia: _/przypomnij XX_, gdzie „XX” to czas wyrażony w minutach.
* Jeśli Twitter nie pozwala Ci wysłać kilku przypomnień jednego dnia, po komendzie dodaj dowolny ciąg znaków, aby tweet nie został potraktowany jako duplikat.

### Wersja rozszerzona (dla wytrwałych)

Nieco ponad tydzień temu wzbogaciłem konto [@dzisiajwtv](https://twitter.com/dzisiajwtv) o możliwość wysyłania przypomnień na chwilę przed rozpoczęciem wybranego filmu. Mechanizm działania miał być stosunkowo prosty.

Każdego dnia na konto trafiają, ze stosownymi interwałami, tweety z informacjami o ciekawych filmach emitowanych w telewizji. Osoba obserwująca konto może w odpowiedzi na takiego tweeta wysłać komendę _/przypomnij_ i otrzymuje informację zwrotną (od utworzonego na potrzeby działania przypomnień konta [@dzisiajwtvalert](https://twitter.com/dzisiajwtvalert)) w postaci potwierdzenia dodania przypomnienia. Następnie, na chwilę przed rozpoczęciem filmu, otrzymuje drugiego tweeta z przypomnieniem.

Cały proces oczywiście jest zautomatyzowany i, spodziewając się pewnych trudności, zapobiegawczo ostrzegłem followersów, że jest to dopiero faza testowa. Ku mojej uciesze sporo osób prędko zabrało się za intensywne testy i już po kilku minutach udało się wyłapać większość mniejszych błędów, które starałem się na bieżąco łatać. Niestety po pierwszym dniu działania okazało się, że bez większych zmian się nie obejdzie.

### Problemy z indeksowanie tweetów przez wyszukiwarkę Twittera

Proces wyłapywania tweetów z komendami w pierwotnej postaci bazował na wynikach wyszukiwania Twittera. Prędko wyszło na jaw, że mogło to jednak nie być najlepsze rozwiązanie, gdyż wyszukiwarka Twittera niektóre tweety najnormalniej w świecie gubiła – z jakiegoś powodu nie były one przez nią indeksowane. Czy to przez zamierzoną optymalizację wyszukiwania, czy przez wykluczanie niektórych osób z wyników z powodu podejrzanej aktywności – nie ma to większego znaczenia; sęk w tym, że nie byłem w stanie serwować usługi wszystkim chcącym z niej korzystać, a to oznaczało konieczność wprowadzenia zmian.

Najlepszym rozwiązaniem okazał się dostęp do wzmianek (_statuses/mentionstimeline_) poprzez API i filtrowanie ich w oparciu o słowa kluczowe (w naszym przypadku komendę _/przypomnij_). Dzięki temu w tej chwili nie gubię już żadnych danych i dodatkowo mam większą swobodę w przetwarzaniu ich. Skoro największy problem został rozwiązany, mogłem się zabrać za kilka mniejszych.

### Korzystanie z usługi niezgodnie z przeznaczeniem

Na początku opracowany przeze mnie proces nie był w pełni kuloodporny; nie udało mi się przewidzieć wszystkich sytuacji, w których może dojść do nieprawidłowości, co pozostawiło małą szczelinę, przez którą mogły się pewne błędy prześlizgnąć.

Skrypt nie do końca wiedział co zrobić, gdy:

1. tweet z komendą został usunięty w czasie między rozpoczęciem przetwarzania danych, a wysyłką potwierdzenia dodania przypomnienia,
2. tweet z komendą nie był odpowiedzią, a samotnym tweetem zaczynającym się od wzmianki _@dzisiajwtv_ i zawierającym komendę,
3. tweet z komendą pojawiał się zbyt daleko w dyskusji – nie był bezpośrednią odpowiedzią na tweeta z informacją o filmie,
4. tweet z komendą był odpowiedzią na tweeta nie zawierającego informacji o filmie,
5. tweet z komendą był odpowiedzią na rekomendację z minionego dnia,
6. komenda zawierała błąd, przy czym pozostałe warunki były spełnione.

Wszystkie powyższe scenariusze zostały załatane i tak: na cztery pierwsze skrypt w ogóle nie reaguje, a na dwa pozostałe wysyła stosowną odpowiedź podając przyczynę nie ustawienia przypomnienia.

### Poprawki poprawkami, ale co z nowościami?

Pierwotny proces przetwarzania danych nie należał do najbardziej żwawych i precyzyjnych w odniesieniu do czasu. Przypomnienia wysyłane były w zakresie pomiędzy 10 a 50 minut przed rozpoczęciem filmu. Sprawiło to, że przed wdrożeniem usługi musiałem zrezygnować z pewnej dodatkowej opcji – **indywidualnego wyznaczania czasu przypomnień**. W związku z tym, że udało mi się całość solidnie zoptymalizować, opcja ta jest już w tej chwili dostępna.

Aby z niej skorzystać, należy bezpośrednio po komendzie _/przypomnij_ dodać czas wyrażony w minutach, określający wyprzedzenie, z jakim ma zostać wysłane przypomnienie. Komenda i czas muszą zostać rozdzielone spacją.

**Przykład:** _/przypomnij 60_

Stosując powyższy przykład, przypomnienie zostanie wysłane na godzinę przed rozpoczęciem filmu. Jeśli w odpowiedzi nie umieścicie czasu, to przypomnieniu zostanie przyporządkowana wartość domyślna – 15 minut, a więc stosowanie tej funkcji jest całkowicie opcjonalne.

### Jakich utrudnień w dalszym ciągu można się spodziewać

Okazuje się, że Twitter nie przepada za powielaniem tweetów. Możecie więc napotkać pewne problemy próbując ustawić kilka przypomnień jednego dnia. Aby temu zaradzić, proponuję, abyście po komendzie dodali dowolny ciąg znaków, dzięki czemu Twitter nie potraktuje danego tweeta jako duplikat. Może to być oczywiście całkowicie przypadkowa treść, ale możecie również wykazać się inwencją twórczą. Proponowane przykłady:

* /przypomnij xyz
* /przypomnij bo uwielbiam ten film!
* /przypomnij 30 ton lista, lista, lista przebojów!

W dwóch pierwszych przykładach przypomnieniu zostanie przyporządkowany domyślny czas (15 minut), a w trzecim zostanie wysłane na 30 minut przed rozpoczęciem filmu.

Te same ograniczenia dotyczące powielania treści obowiązują podczas wysyłania przeze mnie przypomnień, więc przestrzegam przed próbami dodawania kilku przypomnień do tego samego filmu (np. o różnych czasach), ponieważ i tak dotrze do Was tylko pierwsze, a pozostałe będą potraktowane przez Twittera jako duplikaty i nie zostaną wysłane.

Na chwilę obecną nie mam lepszego rozwiązania tego problemu, ale wydaje mi się, że nie powinno ono być dla nas aż tak bardzo kłopotliwe. Jeśli natraficie na jakiekolwiek problemy, koniecznie dajcie mi znać na Twitterze! Staram się działanie przypomnień monitorować, ale niewykluczone, że coś czasem umknie mojej uwadze, a bardzo bym chciał, aby z tego rozwiązania korzystało Wam się przyjemnie.

Jeśli dzielnie przebrnęliście przez całą tę lekturę, serdecznie dziękuję i życzę, abyście okres świąteczny spędzili radośnie i pogodnie w towarzystwie najbliższych. Trzymajcie się ciepło! :-)