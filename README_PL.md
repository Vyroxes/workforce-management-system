🇬🇧 [English version](README.md)

# Workforce Management System

Aplikacja desktopowa do zarządzania pracownikami, grafikami zmian, czasem pracy, zadaniami i nieobecnościami. Lokalny system z relacyjną bazą danych i osobnymi widokami dla administratora oraz pracownika.

---

## Funkcje

- **Konta i logowanie:** indywidualne konta, role `ADMIN` i `EMPLOYEE`, zmiana i resetowanie haseł, dezaktywacja kont oraz zapisywanie ostatniego logowania.
- **Zarządzanie pracownikami:** dane kontaktowe, daty i typ zatrudnienia, działy, stanowiska oraz status aktywności. Dezaktywacja zachowuje dane historyczne.
- **Grafiki zmian:** szablony zmian, przypisywanie pracowników do zmian w konkretnych dniach, widok tygodniowy i miesięczny, kopiowanie grafiku oraz wykrywanie kolizji.
- **Ewidencja czasu pracy:** rozpoczynanie i kończenie pracy, porównywanie godzin planowanych z rzeczywistymi oraz korekty wpisów przez administratora.
- **Zadania:** przypisywanie w ramach konkretnej zmiany pracownika w grafiku, opisy, priorytety, statusy, szacowany czas wykonania i terminy realizacji.
- **Pomiar czasu zadań:** osobne sesje zadania, pozwalające przerwać pracę nad zadaniem i później ją wznowić.
- **Nieobecności:** urlopy, zwolnienia chorobowe i inne nieobecności zarządzane przez administratora, z wykrywaniem konfliktów z grafikiem.
- **Panele i raporty:** statystyki pracowników, czasu pracy, zadań i nieobecności dla administratora; własny grafik, godziny i zadania dla pracownika.
- **Dziennik audytu:** rejestrowanie ważnych operacji dotyczących kont, pracowników, grafików i ewidencji czasu.

Planowany grafik, faktyczny czas pracy i czas wykonywania zadań to osobne dane. Szablon zmiany określa godziny pracy, a wpis w grafiku przypisuje zmianę do pracownika w konkretnym dniu.

---

## Role i uprawnienia

| Rola | Dostęp |
| --- | --- |
| `ADMIN` | Zarządzanie kontami, pracownikami, działami, stanowiskami, zmianami, grafikami, zadaniami i nieobecnościami; korekta ewidencji czasu pracy oraz raporty obejmujące wszystkich pracowników. |
| `EMPLOYEE` | Podgląd własnego grafiku i przypisanych zadań, rejestrowanie czasu pracy i zadań oraz zmiana własnego hasła. |

Uprawnienia są sprawdzane w logice aplikacji. Hasła są przechowywane jako hashe. Walidacja zapobiega nakładaniu się zmian, przypisywaniu zmian podczas nieobecności, tworzeniu kilku aktywnych sesji pracy oraz rozpoczynaniu cudzych zadań lub zadań poza aktywną sesją pracy.

---

## Technologie

| Technologia | Zastosowanie |
| --- | --- |
| Python 3 | Kod aplikacji |
| PySide6 | Interfejs desktopowy |
| SQLAlchemy 2.x | ORM i dostęp do bazy danych |
| SQLite | Lokalna relacyjna baza danych |

---

## Struktura projektu

```text
workforce-management-system/
├── main.py
├── requirements.txt
├── README.md
├── README_PL.md
├── LICENCE
├── .gitignore
├── app/
│   ├── __init__.py
│   ├── database/             # Konfiguracja bazy i dane początkowe
│   │   ├── __init__.py
│   │   ├── database.py
│   │   └── seed.py
│   ├── models/               # Modele ORM
│   │   ├── __init__.py
│   │   ├── user.py
│   │   ├── employee.py
│   │   ├── department.py
│   │   ├── position.py
│   │   ├── shift.py
│   │   ├── schedule_entry.py
│   │   ├── work_time_entry.py
│   │   ├── task.py
│   │   ├── task_time_entry.py
│   │   ├── absence.py
│   │   └── audit_log.py
│   ├── logic/                # Uwierzytelnianie i reguły biznesowe
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── login_window.py
│   │   ├── main_window.py
│   │   ├── pages/            # Panele i strony modułów
│   │   ├── dialogs/          # Formularze dodawania i edycji
│   │   └── widgets/          # Współdzielone elementy interfejsu
│   ├── security/             # Hashowanie i weryfikacja haseł
│   ├── utils/                # Walidacja oraz obsługa dat i czasu
│   └── resources/
│       ├── icons/
│       │   └── icon.ico
│       └── styles/
│           └── main.qss
├── data/
│   └── .gitkeep
└── tests/
    ├── test_auth.py
    ├── test_work_time.py
    ├── test_schedules.py
    └── test_tasks.py
```

Przepływ danych to **interfejs → logika biznesowa → modele SQLAlchemy → SQLite**. Kod interfejsu wywołuje funkcje z `app/logic/`, które wykonują operacje i sprawdzają reguły biznesowe.

Lokalna baza danych SQLite jest przechowywana w `data/workforce.db`. Pliki baz danych są wykluczone z kontroli wersji.

---

## Planowane ulepszenia

---

## Wymagania i instalacja

### Python

Zalecany jest Python 3.12.

### Instalacja zależności

Zainstaluj zależności z `requirements.txt`:

```bash
pip install -r requirements.txt
```

### Uruchomienie ze źródeł

```bash
python main.py
```

---

## Budowanie aplikacji dla Windows

Do utworzenia aplikacji dla Windows można użyć PyInstaller.

Przykładowe polecenia budowania, uruchamiane w katalogu głównym projektu:

```bash
python -m pip install pyinstaller
python -m PyInstaller --windowed --icon="app/resources/icons/icon.ico" --name "Workforce Management System" --add-data "app/resources;app/resources" main.py
```

---

## Testy

Katalog `tests/` zawiera moduły testów obejmujących uwierzytelnianie i ograniczenia dostępu, rozpoczynanie i kończenie pracy, kolizje grafiku i nieobecności oraz przypisanie zadań i pomiar ich czasu.

---

## Licencja

Copyright © 2026 Michał Rusek (Vyroxes), Kacper Kwiatek (vitalyi11) i Aleksandra Tworek (abelxoo). Wszelkie prawa zastrzeżone.

O ile nie zaznaczono inaczej, kod źródłowy jest publicznie dostępny wyłącznie
do użytku prywatnego, niekomercyjnego oraz edukacyjnego.

Użycie komercyjne, redystrybucja, sublicencjonowanie oraz rozpowszechnianie
zmodyfikowanych wersji są zabronione bez uprzedniej pisemnej zgody autorów.

Komponenty zewnętrzne podlegają własnym licencjom.

Treść licencji projektu znajduje się w pliku [LICENCE](LICENCE).

---

**Autorzy:**

- Michał Rusek (Vyroxes)
- Kacper Kwiatek (vitalyi11)
- Aleksandra Tworek (abelxoo)