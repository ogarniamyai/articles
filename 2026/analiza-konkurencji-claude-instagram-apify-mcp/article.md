---
slug: "analiza-konkurencji-claude-instagram-apify-mcp"
title: "Przeanalizuj konkurencję na Instagramie z Claude i Apify"
excerpt: "Pokażę Ci, jak połączyć Claude z Apify, zebrać publiczne dane z Instagrama i zamienić je w konkretną analizę konkurencji."
cover: "./assets/cover-v2.jpg"
category: "Automatyzacja"
---

W tym artykule pokażę Ci, jak połączyć Claude z Apify i przeprowadzić analizę konkurencji na Instagramie bez ręcznego przepisywania danych do arkusza. Całość możesz przetestować bezpłatnie, korzystając z darmowych planów obu narzędzi.

## Spis treści

- [Po co analizować konkurencję](#po-co-analizować-konkurencję)
- [Czym jest Apify](#czym-jest-apify)
- [Krok 1: załóż konto w Apify](#krok-1-załóż-konto-w-apify)
- [Krok 2: zainstaluj Claude](#krok-2-zainstaluj-claude)
- [Krok 3: połącz Claude z Apify](#krok-3-połącz-claude-z-apify)
- [Krok 4: ustaw uprawnienia](#krok-4-ustaw-uprawnienia)
- [Krok 5: zezwól na dostęp do domen](#krok-5-zezwól-na-dostęp-do-domen)
- [Krok 6: zainstaluj skill do analizy](#krok-6-zainstaluj-skill-do-analizy)
- [Krok 7: uruchom analizę (prompt)](#krok-7-uruchom-analizę)
- [O czym warto pamiętać](#o-czym-warto-pamiętać)
- [Na koniec](#na-koniec)

## Po co analizować konkurencję

Obserwacja innych kont to jeden z pierwszych kroków przy rozwijaniu firmy albo marki osobistej na Instagramie. Pozwala sprawdzić, jakie tematy i formaty pojawiają się w danej niszy, co przyciąga uwagę oraz gdzie zostaje miejsce na coś, czego inni jeszcze nie robią.

Nie chodzi o kopiowanie. Dobra analiza ma pomóc zrozumieć rynek, znaleźć niewykorzystane obszary i podejmować decyzje na podstawie danych. Ręczne zbieranie materiału z kilku kont jest mozolne i zajmuje wiele godzin. Tutaj tę pracę przejmą Claude i Apify.

## Czym jest Apify

[Apify](https://apify.com) to platforma z gotowymi narzędziami do pobierania publicznych danych z internetu. Takie narzędzia nazywają się tam **Actors**, czyli aktorzy. Każdy jest przygotowany do innego zadania: może zbierać dane z konkretnego serwisu albo automatyzować określony proces. Instagram Scraper jest jednym z nich, ale w Apify Store znajdziesz też wiele innych aktorów, które możesz później podłączyć do Claude i wykorzystać w podobny sposób.

W tym poradniku skorzystam z dwóch aktorów, których Claude będzie uruchamiał bezpośrednio z rozmowy przez connector MCP:

- [Instagram Scraper](https://apify.com/apify/instagram-scraper) — do ogólnych danych profili i szerszego kontekstu konta,
- [Instagram Post Scraper](https://apify.com/apify/instagram-post-scraper) — do pobierania publikacji, bo lepiej radzi sobie z wyciąganiem postów. Pierwszy aktor czasami nie zwraca ich wszystkich.

Darmowy plan Apify daje obecnie **5 dolarów kredytu miesięcznie**. Oba scrapery mają osobny cennik i pobierają opłatę za każdy zwrócony wynik. Instagram Scraper na planie darmowym kosztuje obecnie **2,70 dolara za 1000 wyników**, a Instagram Post Scraper zaczyna się od **1 dolara za 1000 postów**. Przy podstawowej analizie kilku kont darmowa pula powinna wystarczyć. Aktualne warunki sprawdzisz w [cenniku planów Apify](https://apify.com/pricing), [cenniku Instagram Scrapera](https://console.apify.com/actors/shu8hvrXbJbY3Eb9W/info/pricing?build=latest) oraz na stronie [Instagram Post Scrapera](https://apify.com/apify/instagram-post-scraper/pricing).

![Instagram Scraper w Apify wraz z opisem i ceną za tysiąc wyników](./assets/instagram-scraper-apify.png)

![Instagram Post Scraper w Apify wraz z opisem i ceną za tysiąc postów](./assets/instagram-posts-scraper-apify.png)

## Krok 1: załóż konto w Apify

Wejdź na [apify.com](https://apify.com) i utwórz darmowe konto. Nie musisz ręcznie konfigurować scrapera. Potrzebujesz jedynie aktywnego konta, z którego connector będzie mógł korzystać.

## Krok 2: zainstaluj Claude

Pobierz aplikację Claude na komputer z oficjalnej strony:

[Pobierz Claude Desktop](https://claude.com/download)

Na moment przygotowywania tego poradnika connector Apify **wymaga aplikacji Claude Desktop**. W przeglądarce Claude wyświetla informację, że trzeba zainstalować wersję na komputer, dlatego nie pomijaj tego kroku. Integracje zmieniają się jednak dość szybko, więc jeśli czytasz ten artykuł później, możesz sprawdzić w **Customize → Connectors**, czy obsługa Apify w przeglądarce nie została już dodana.

Do testu wystarczy darmowe konto Claude. Przy większej analizie polecam plan **Pro**, ponieważ cały proces zużywa sporo limitu i na darmowym planie może zatrzymać się w połowie (wtedy trzeba czekać 5h na reset limitów).

## Krok 3: połącz Claude z Apify

1. Otwórz Claude i przejdź do **Customize → Connectors**.
2. Kliknij **Add → Browse connectors**.

   ![Sekcja Connectors w Claude Desktop z otwartym menu Add](./assets/claude-connectors-add.png)

3. Wyszukaj **Apify** i otwórz znaleziony connector.

   ![Apify znalezione w katalogu connectorów Claude](./assets/claude-connectors-directory.png)

4. W polu **Apify API token** wklej token [ze swojego konta w Apify](https://console.apify.com/settings/integrations).

   ![Pole Apify API token i Enabled tools w konfiguracji connectora](./assets/apify-api-token.png)

5. Pole **Enabled tools** pozostaw bez zmian i kliknij **Save**.

### Gdzie znaleźć API token

W oknie konfiguracji connectora, tuż nad polem **Apify API token**, znajduje się gotowy link prowadzący do właściwej strony w Apify. Kliknij go albo skopiuj do przeglądarki, a następnie skopiuj swój token i wklej go w pole w Claude. Możesz też znaleźć go ręcznie w Apify Console w **Settings → API & Integrations**. Token działa podobnie jak hasło, dlatego nie udostępniaj go ani nie pokazuj na zrzutach ekranu.

## Krok 4: ustaw uprawnienia

W tym samym oknie przejdź do **Tool permissions** i ustaw:

- **Interactive tools** na **Always allow**,
- **Read-only tools** na **Always allow**,
- **Write/delete tools** na **Needs approval**.

Dzięki temu Claude nie będzie pytał o zgodę przy każdym odczycie, ale operacje mogące coś zmienić nadal będą wymagały zatwierdzenia. W nowej rozmowie kliknij jeszcze **+ → Connectors** i sprawdź, czy Apify jest włączone.

![Ustawienia Tool permissions connectora Apify](./assets/connector-settings.png)

## Krok 5: zezwól na dostęp do domen

Wejdź w **Settings → Capabilities**. Upewnij się, że masz włączone **Code execution and file creation** oraz **Allow network egress**, a w **Domain allowlist** wybierz **All domains**.

To ustawienie pozwala Claude'owi dociągnąć obrazy z serwerów Instagrama. Są one potrzebne do analizy spójności wizualnej profilu.

![Ustawienie Domain allowlist na All domains w Capabilities](./assets/allow-domains.png)

## Krok 6: zainstaluj skill do analizy

Do tego procesu sam przygotowałem skill, którego używałem podczas własnych analiz. Jest to instrukcja mówiąca Claude'owi, jak poprowadzić pracę od pierwszych pytań do gotowego raportu. Dzięki temu nie musisz za każdym razem opisywać całego procesu od nowa.

Najpierw pobierz skill:

**Skill do pobrania:** [instagram-competitor-analysis.zip](https://ogarniamy.ai/files/WyUEB4trd3_COp2EuMYhEob0kriCGgix)

Bez włączonej funkcji **Code execution and file creation** skille mogą nie pojawić się w ustawieniach, dlatego upewnij się, że zrobiłeś to w poprzednim kroku.

1. Przejdź do **Customize → Skills**.
2. Kliknij znak **+**, a następnie **Create skill**.
3. Wybierz **Upload a skill**.
4. Wgraj pobrany plik ZIP.
5. Sprawdź, czy nowy skill jest włączony na liście.

![Menu Upload a skill w ustawieniach Skills aplikacji Claude Desktop](./assets/claude-skill-upload.png)

Skille działają również na darmowym planie Claude. Możesz później zmodyfikować ten plik i dopasować instrukcję precyzyjniej pod siebie.

## Krok 7: uruchom analizę

Otwórz nową rozmowę i napisz, że chcesz przeprowadzić analizę konkurencji na Instagramie. Najlepiej od razu podaj konkretne profile, które chcesz uwzględnić. Masz wtedy pewność, że analizowane konta są dla Ciebie wartościowe, a Claude nie musi przeszukiwać całego Instagrama w poszukiwaniu kandydatów. To przyspiesza pracę i zmniejsza zużycie tokenów. Jeżeli nie masz jeszcze własnej listy, możesz wkleić adres swojego konta, opisać niszę i pozostawić wybór Claude'owi.

Przygotowałem też gotowy prompt startowy. Uzupełnij pola dotyczące swojej marki i wklej go do nowej rozmowy:

```
Zrób mi pełną analizę konkurencji na Instagramie.

Moje konto: [np. @twojanazwa]
Nisza / branża: [np. narzędzia AI dla początkujących, dietetyka kliniczna, automatyzacja małych firm, zagraniczne kursy językowe]
Odbiorca, do którego mówię: [np. osoby na etacie i marki osobiste, które boją się AI i nie wiedzą, od czego zacząć]
Konkurencja, którą znam: [wymień konta, jeśli masz listę, albo napisz "nie mam listy, znajdź kandydatów"]
Cel analizy: [np. podniesienie zaangażowania / pomysły na treści / start nowego konta / zrozumienie pozycjonowania rywali]
Format raportu: Stwórz trzy oddzielne raporty: markdown, PDF ze statyczynmi wykresami i obrazami, interaktywny HTML
Kolory PDF / HTML: [podaj kolor akcentu w formacie #RRGGBB, podaj skill do identyfikacji wizualnej albo napisz "wybierz sam"]
Dodatkowe wymagania: [tutaj podaj jakieś szczególne wymagania dotyczące analizy, jeśli je masz]
```

Claude zada kilka pytań doprecyzowujących, a w kolejnych etapach będzie pytał, czy ma przejść dalej. To dobry moment, żeby doprecyzować wcześniejsze odpowiedzi, dodać własne uwagi albo rozszerzyć zakres analizy. Następnie Claude rozpocznie pobieranie i analizę danych. **Samo wygenerowanie końcowego raportu może potrwać nawet około godziny**, a przy większym zakresie cały proces będzie jeszcze dłuższy. Nie zamykaj więc aplikacji i nie zakładaj, że raport będzie gotowy po kilkunastu minutach. Po zakończeniu możesz dalej zadawać pytania i zlecać kolejne zadania na podstawie informacji zgromadzonych w tej rozmowie.

W Apify Console możesz w każdej chwili sprawdzić historię uruchomień, liczbę wyników i koszt każdej operacji:

![Historia uruchomień Instagram Scrapera w Apify z liczbą wyników i kosztami](./assets/apify-runs-costs.png)

## O czym warto pamiętać

Analiza zużywa jednocześnie kredyty Apify oraz limit Claude. **Im więcej kont i publikacji zlecisz do sprawdzenia, tym dłużej potrwa cały proces i tym szybciej wykorzystasz oba limity.** Każdy kolejny post to dodatkowy wynik pobrany przez Apify oraz więcej danych, które Claude musi przeczytać i porównać. Zacznij więc od kilku kont i niewielkiej liczby publikacji, a większe zadanie uruchamiaj najlepiej tuż po odnowieniu limitu Claude.

Do większości procesu polecam model klasy **Sonnet 5** z ustawieniem **Reasoning: High**. Zapewnia dobry poziom analizy, ale nawet w tej konfiguracji trzeba przygotować się na duże zużycie limitu. W moim przypadku wygenerowanie raportu wykorzystało **69% całego limitu dostępnego w pięciogodzinnym oknie** na planie Pro.

Jeżeli zależy Ci na jeszcze dokładniejszych wnioskach i możesz poświęcić więcej czasu oraz limitu, przed generowaniem końcowego raportu możesz przełączyć się na mocniejszy model. Trzeba jednak liczyć się z tym, że takie zadanie może zużyć cały pozostały limit. Wtedy Claude zatrzyma pracę i trzeba będzie poczekać na jego odnowienie.

Korzystaj wyłącznie z publicznie dostępnych informacji i pamiętaj, że raport jest punktem wyjścia do własnych decyzji, a nie nieomylną instrukcją. Instagram nie pokazuje publicznie wszystkich statystyk, dlatego Claude analizuje tylko tę część obrazu, którą da się zebrać z zewnątrz jako zwykły użytkownik.

## Na koniec

Po jednorazowym skonfigurowaniu Apify, connectora i skilla kolejne analizy sprowadzają się już głównie do opisania celu oraz wskazania kont. Najbardziej mozolną część pracy przejmują narzędzia, a Ty dostajesz uporządkowany materiał, do którego możesz wracać z kolejnymi pytaniami.

Zacznij od małego testu, sprawdź jakość raportu i dopiero później zwiększaj zakres. Nie traktuj wniosków Claude'a jak gotowej recepty na rozwój profilu, ale jak punkt wyjścia do podejmowania lepszych decyzji i planowania własnych eksperymentów. Największą przewagę daje nie samo posiadanie danych, lecz umiejętność zauważenia w nich miejsca, którego inni jeszcze nie zagospodarowali.
