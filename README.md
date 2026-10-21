# Kierunek — Asystent Doradcy

Aplikacja dla szkolnych doradców zawodowych: scenariusze zajęć, plan działań, podsumowania i eksport do kalendarza. Wersja 1.3.

## Publikacja na GitHub Pages krok po kroku

1. Rozpakuj ZIP na komputerze.
2. Utwórz repozytorium w GitHub, np. `kierunek-doradca`.
3. W repozytorium wybierz **Add file → Upload files**.
4. Wgraj **zawartość rozpakowanego folderu**, w tym folder `vendor`. Plik `index.html` musi być bezpośrednio w głównym katalogu repozytorium, obok `README.md`.
5. Zatwierdź przesłane pliki przyciskiem **Commit changes**.
6. Otwórz **Settings → Pages**.
7. W sekcji **Build and deployment** wybierz **Source: Deploy from a branch**.
8. Wybierz gałąź **main**, katalog **/(root)** i kliknij **Save**.
9. Po zakończeniu publikacji adres aplikacji pojawi się w ustawieniach Pages.

Nie wgrywaj samego ZIP-a. Do działania eksportu Word konieczny jest plik `vendor/docx.js`. Plik `.nojekyll` wyłącza przetwarzanie projektu przez Jekyll; jeżeli menedżer plików go ukrywa, możesz dodać go w GitHub jako pusty plik.

Dostępność Pages zależy od planu konta i ustawień repozytorium. Standardowo opublikowana strona jest dostępna dla osób znających jej adres. Ta paczka nie zawiera logowania ani mechanizmu ograniczania dostępu.

Oficjalna instrukcja: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

## Uruchomienie na komputerze

Możesz otworzyć `index.html` bezpośrednio w aktualnej przeglądarce. Do regularnej pracy zalecany jest lokalny serwer lub GitHub Pages — zapis przy otwieraniu plików lokalnych zależy od przeglądarki.

Jeżeli masz Python 3, w katalogu projektu uruchom:

```bash
python3 -m http.server 8000
```

Następnie otwórz http://localhost:8000. Na Windows zamiast `python3` możesz użyć `py`.

Aplikacja nie wymaga instalacji pakietów, klucza API, bazy danych ani procesu budowania. Biblioteka tworząca DOCX jest dołączona lokalnie. Odnośniki do materiałów zewnętrznych wymagają internetu.

## Funkcje

- Pulpit z planowanymi działaniami i zapisanymi scenariuszami.
- Sześć edytowalnych szablonów zajęć z wariantami czasu 30, 45, 60 i 90 minut.
- Plan działań: klasa, data, godziny, miejsce, odpowiedzialni, partnerzy, forma i notatki.
- Oznaczanie realizacji działań i podsumowanie planu.
- Edytowalne pliki **DOCX**: format A4, nagłówki, marginesy, numeracja stron i osobna karta pracy.
- Podgląd dokumentu z przyciskiem **Drukuj / zapisz PDF**. PDF powstaje w oknie drukowania przeglądarki.
- Zapis lokalny oraz pobieranie i wczytywanie kopii **JSON**.
- Pobieranie pojedynczych wydarzeń i całego planu w formacie **ICS**.
- Katalog źródeł do pracy doradcy.

## Dane i przeniesienie na nowy adres

Dane są przechowywane lokalnie w przeglądarce pod kluczem `kierunek-doradca-v1`. Każdy użytkownik ma własny zapis. Nie ma wspólnej bazy danych ani synchronizacji między urządzeniami.

Regularnie używaj **Pobierz JSON**. Wczytanie kopii zastępuje aktualne dane po potwierdzeniu. Pliki JSON nie są szyfrowane.

**Przeniesienie z dotychczasowej strony:** na poprzedniej stronie pobierz JSON, następnie na nowej stronie GitHub Pages kliknij **Wczytaj** i wybierz ten plik. Dane nie przeniosą się automatycznie między adresami.

Nie umieszczaj kopii danych ani dokumentów uczniów w publicznym repozytorium. Paczka zawiera wyłącznie aplikację, bez danych użytkownika.

## Kalendarz

W **Planie działań** wybierz **Pobierz kalendarz (.ics)**, aby pobrać wszystkie niezrealizowane działania z datą. Wpisy bez daty są pomijane. Przycisk przy pojedynczym działaniu eksportuje wybrane wydarzenie.

- Puste obie godziny: wydarzenie całodniowe.
- Wpisane obie godziny: wydarzenie godzinowe według strefy Europe/Warsaw.
- Wydarzenie godzinowe rozpoczyna się i kończy w tym samym dniu.
- Plik zawiera nazwę, opis i miejsce wydarzenia; nie wysyła zaproszeń.
- Zaimportowany plik jest kopią planu. Zmiany w aplikacji nie aktualizują automatycznie kalendarza.

## Pliki projektu

| Plik | Rola |
| --- | --- |
| `index.html` | Ekran aplikacji i ładowanie skryptów |
| `style.css` | Wygląd i układ responsywny |
| `app.js` | Widoki, zapis lokalny i kopie JSON |
| `document-export.js` | Skład DOCX i podgląd do druku |
| `calendar.js` | Generowanie ICS i obsługa strefy czasowej |
| `vendor/docx.js` | Dołączona biblioteka eksportu Word |
| `vendor/docx-LICENSE.txt` | Licencja biblioteki docx |
| `tests/calendar.test.cjs` | Kontrola eksportu kalendarza |
| `.nojekyll` | Publikacja plików statycznych w Pages |

Szablony scenariuszy znajdują się w tablicy `topics` w `app.js`. To gotowe materiały do dostosowania; aplikacja nie korzysta z AI. Nie wdrożono jeszcze mapy pokrycia wszystkich treści programowych z rozporządzenia.

## Sprawdzenie zmian

Jeżeli masz Node.js:

```bash
node --check app.js
node --check document-export.js
node --check calendar.js
node tests/calendar.test.cjs
```

Po zmianie eksportu sprawdź także wygląd dokumentu w edytorze Word i podglądzie wydruku. Po zmianie wyglądu sprawdź aplikację na komputerze i telefonie.

## Składniki zewnętrzne

Biblioteka `docx` została dołączona z jej licencją w folderze `vendor`. Zachowaj plik licencji przy dalszym udostępnianiu. Ta paczka nie nadaje osobnej licencji otwartej całemu projektowi.
