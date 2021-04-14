### Tema 1: Implementarea unui analizor lexical pentru un limbaj de programare (C)

Se vor respecta următoarele indicății de implementare:

- Analizorul lexical va folosi un automat finit determinist, care va avea câte o stare finală pentru fiecare tip de token; Pentru identificarea tokenilor, el va consuma pe rând caractere din fișierul sursă și va face tranziții în automat, până se blochează; 
- Dacă s-a blocat într-o stare nefinală, atunci s-a întâlnit o eroare lexicală și analiza se oprește; Dacă s-a blocat într-o stare finală, se generează tokenul respectiv (tipul său este indicat de starea finală  iar valoarea este șirul consumat pentru a ajunge din starea inițială acolo), după care se trece automat în starea inițială (fără a consumă caractere din sursă) și se reia analiza consumând caractere și făcând tranziții;
- Dacă automatul s-a blocat într-o stare nefinală și pe traseul parcurs de la starea inițială până acolo s-a întâlnit măcar o stare finală, să se întoarcă pe traseu până la ultima stare finală întâlnită (introducând înapoi în bandă de intrare caracterele consumate la tranziții) și se generează tokenul corespunzător; doar dacă pe traseul respectiv nu s-a întâlnit nici o stare finală atunci se generează eroarea;
- Conceptul de token va fi implementat unitar, sub formă unui obiect; El va avea cel puțin următorii membri-dată:
  - Un membru ce indică tipul tokenului;
  - Un membru ce indică valoarea tokenului;
- Analizorul lexical va fi implementat unitar sub forma unui obiect; acesta va conține toate informațiile care descriu analizorul lexical respectiv (automatul, tabela de stringuri și cea de cuvinte cheie, referință la fișierul sursă curent analizat, numărul caracterului curent în acest fișier, etc.); Acesta va oferi cel puțin o metodă publică pe care o vom numi în continuare "getToken" și care la fiecare apelare returnează un nou token din fișierul analizat;
- Programul supus analizei lexicale va fi scris într-un fișier de intrare, iar tokenii rezultați într-un fișier de ieșire; în programul principal se vor face inițializări (de exemplu citirea numelor celor două fișiere), apoi într-un ciclu, la fiecare iteratie, se va apela o dată getToken apoi tokenul rezultat se va scrie în fișierul destinație; atenție că prelucrarea tokenului rezultat (scrierea lui în fișierul destinație) se face în programul principal, nu într-o metodă a analizorului lexical - acesta în principiu nu face decât getToken pentru  a furniza un nou token;
- Analizorul lexical va ignora spațiile albe din fișierul sursă (șiruri maximale de caractere albe și comentarii);
- În cazul întâlnirii unei erori lexicale în fișierul analizat, getToken va returna un token de eroare, al cărui membru-tip va indica tipul erorii și al cărui membru-valoare va indica poziția în fișier unde se află caracterul ce a generat eroarea; în programul principal, la recepționarea unui astfel de token se va scrie în fișierul destinație un mesaj adecvat de eroare și poziția respectivă,  după care analiza se va opri.

Automatul folosit ca model pentru implementarea analizorului:

<img src="D:\GitHub\Uni-Projects\TC\LexerC\DFA.png" style="zoom:50%;" />