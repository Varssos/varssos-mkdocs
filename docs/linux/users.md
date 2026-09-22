# Users

1. Utwórz konto dla użytkownika Kermit wraz z katalogiem domowym `sudo useradd -d /home/Kermit -m Kermit`
2. Utwórz konto dla użytkownika Piggy, ale katalog domowy ma być ustawiony na /muppety/Piggy. `sudo useradd -d /muppety/Piggy -m Piggy`
3. Utwórz grupę muppety. `sudo groupadd muppety`
4. Dodaj do grupy muppety użytkowników Kermit oraz Piggy. `sudo usermod -G muppety Kermit`
5. Przenieś katalog domowy dla użytkownika Kermit na /muppety/Kermit. `sudo mv /home/Kermit/ /muppety/`
6. Zablokuj hasło użytkownikowi Piggy. `sudo usermod -L Piggy`
7. Odblokuj konto Piggy `sudo usermod -U Piggy`
8. Zmień własne hasło `sudo passwd $USER`
9. Sprawdź własny identyfikator oraz grupy, do których należysz `id`
10. Sprawdź kto jest zalogowany w chwili obecnej w systemie `w/who/finger`
