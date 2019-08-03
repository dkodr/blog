---
published: true
title: Przypomnienia @dzisiajwtv - changelog
---
Po zeszłotygodniowych zmianach w działaniu przypomnień @dzisiajwtv, czas na kolejne poprawki.

Najważniejszą rzeczą, którą chciałbym Wam dzisiaj przekazać, jest to, że od poniedziałku, 5 stycznia, zmianie ulegnie komenda używana do ustawiania przypomnień. Zamiast dotychczasowej **/przypomnij** zaczniemy korzystać z hashtaga **#przypomnij**. Reszta pozostanie bez zmian, więc w przypadku chęci dodania przypomnienia np. na 30 minut przed rozpoczęciem filmu, będzie należało w odpowiedzi napisać: **#przypomnij 30**.

Zmiana ta motywowana jest powszechną rozpoznawalnością hashtagów, co powinno przełożyć się na łatwiejsze przyswojenie metody ustawiania przypomnień. Niestety komenda z ukośnikiem okazała się zbyt kłopotliwa. Dodatkowo, formatowanie hashtagów stosowane przez Twittera (traktowanie ich jako odnośniki i ukazywanie w innym kolorze) również niesie za sobą pewne korzyści – zwiększa się widoczność takiego tweeta oraz łatwiej odnaleźć (w celach statystycznych) najbardziej popularne filmy, o rozpoczęciu których użytkownicy chcą być powiadamiani.

Mam nadzieję, że migracja okaże się bezproblemowa. Osoby, które w poniedziałek będą próbowały skorzystać ze starej komendy, otrzymają w odpowiedzi tweeta informującego o zmianie.

Poniżej znajdziecie najświeższy changelog (2015-01-02). Jeśli napotkacie jakieś niepożądane działania bota, uprzejmie proszę, dajcie mi znać na Twitterze.

### Zmiany:

* zmieniono nazwę bota @dzisiajwtvalert na @dzisiajwtvbot,
* wprowadzono ograniczenia czasowe; użytkownik nie może dodać przypomnienia, jeśli film rozpoczyna się w czasie krótszym niż 30 minut od momentu wysłania komendy

### Poprawki:

* wprowadzono do komunikatów o błędach zmienne w postaci tytułów filmów, aby uniknąć zostania potraktowanym przez Twittera jako tweet o identycznej treści,
* naprawiono opóźnienia (sięgające 1h) w wysyłce potwierdzeń spowodowane kłopotami w pobraniu najświeższych tweetów podczas przetwarzania danych,
* wprowadzono weryfikację ustawianego przez użytkownika czasu przypomnień; jeśli jest zbyt długi, użytkownik zostaje poproszony o jego skrócenie,
* dodano komunikat zwrotny informujący użytkownika o próbie dodania przypomnienia do tweeta nie zawierającego informacji o filmie,
* dodano komunikat zwrotny informujący użytkownika o próbie dodania przypomnienia o filmie, który już się rozpoczął
