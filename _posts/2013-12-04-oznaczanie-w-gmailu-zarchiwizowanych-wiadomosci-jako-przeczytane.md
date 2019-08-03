---
published: false
layout: post
title: Jak w Gmailu automatycznie oznaczyń zarchiwizowane wiadomości jako przeczytane
---
Nie potrafię wytłumaczyć dlaczego (może to nerwica natręctw), ale nie lubię archiwizować w Gmailu nieprzeczytanych wiadomości. Niektórych maili nie muszę czytać, gdyż wiem co zawierają (potwierdzenia przelewów, zakupów w Play Store itp.), chcę zachować je w archiwum, ale nie lubię pozostawiać ich zaznaczonych jako nieprzeczytane.

Zarówno interfejs webowy, jak i aplikacja na Androida nie pozwalają **jednym kliknięciem** zaznaczyć wiadomości jako przeczytaną oraz zarchiwizować ją. Tutaj z pomocą przychodzą Skrypty Google. Wchodzimy na https://script.google.com/, tworzymy nowy projekt, w którym umieszczamy następujący kod:

```
function archiveAsRead() {
  // Finds unread messages in the archive and marks them as read
  var threads = GmailApp.search('label:unread -label:"inbox" -label:"trash" -label:"sent" -label:"spam" -label:"chats"');
  for (var i = 0; i < threads.length; i++) {
    threads[i].markRead();
  }
}
```

Zapisujemy skrypt, uruchamiamy i udzielamy mu dostępu do naszego konta Gmail. Klikając w ikonę z zegarem możemy ustawić jak często skrypt ma być automatycznie uruchamiany (np. co godzinę).

Teraz, gdy zobaczymy na smartfonie rozszerzone powiadomienie o mailu, który ma jako przeczytany trafić do archiwum, klikamy akcję „Archiwizuj” i problem z głowy. Można również wybrać się do psychiatry i wyleczyć się z takich paranoi, ale wybór pozostawiam Wam.