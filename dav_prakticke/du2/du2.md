# Domáca úloha č. 2 (15 bodov)

V rámci e-learningového systému môžu učitelia vytvárať testy, prideľovať ich študentom a sledovať, ako sa študentom v teste darilo. Pre jednoduchosť budeme uvažovať len testy s výberom odpovede (možnosti ABCD, v každej otázke 1 správna a 3 nesprávne odpovede). Chceme evidovať nasledujúce údaje:
* Pre každého študenta a učiteľa meno a priezvisko.
* Učiteľ môže vytvoriť test pozostávajúci z niekoľkých otázok (ľubovoľne veľa); potrebujeme evidovať názov testu, autora (učiteľ) a otázky, ktoré daný test obsahuje.
* Otázka pozostáva z textu zadania a textov správnej odpovede a nesprávnych odpovedí. Jedna otázka môže byť súčasťou viacerých testov.
* Pri pridelení testu žiakovi (daný test možno danému žiakovi prideliť jediný raz) treba evidovať, ktorý učiteľ test pridelil a čas, kedy bol test pridelený.
* Po vypracovaní prideleného testu chceme zaznamenať študentove odpovede: potrebujeme vedieť, o ktoré pridelenie testu ide, čas vypracovania testu a odpovede na tie otázky, pre ktoré si žiak vybral niektorú z možných odpovedí (študent môže v rámci jedného pridelenia absolvovať test ľubovoľne veľa ráz). Nie je prípustné evidovať dve vypracovania pre jedného študenta v tom istom čase (v rovnakom čase však môžu byť vypracované testy rôznych študentov).

---

1. Navrhnite štruktúru vyššie popísanej databázy a vytvorte súbor `testy.sql`, ktorý bude obsahovať SQL príkazy, ktoré vytvoria potrebné tabuľky.
Pred každý príkaz `CREATE TABLE` (alebo na začiatok súboru) doplňte aj zodpovedajúci príkaz `DROP TABLE IF EXISTS`, aby bolo možné súbor `testy.sql` spúšťať viackrát za sebou bez chýb. Požiadavky:
	* aspoň jedna relácia s iba kompozitnými kľúčmi vrátane primárneho (každý kľúč tejto relácie má viac ako 1 atribút) --- čiže môžete používať umelé id (surrogate keys), kde sa to hodí, ale skúste aspoň jednu tabuľku navrhnúť inak;
	* relácie v BCNF (alebo 3NF + zdôvodnenie, že dekompozícia do BCNF neexistuje --- môžete využívať online nástroje);
	* nanajvýš 10 tabuliek.

2. Konzistentnosť dát strážte vhodne nastavenými cudzími kľúčmi (`FOREIGN KEY`, vrátane `ON DELETE` / `ON UPDATE`) a ďalšími obmedzeniami.

3. Popíšte platné funkčné závislosti pre všetky jednotlivé relácie. Posúďte, či sa relácie vašej dekompozície spájajú bezstratovo a či ste zachovali všetky funkčné závislosti (t.j. či pri dekompozícii do 3NF/BCNF nedošlo k zlomeniu nejakej FZ). Dokážte, že vaše relácie sú v BCNF, resp. 3NF (ak BCNF neexistuje).

4. Učitelia majú požiadavku na doplnenie informácie, dokedy môže študent pridelený test vypracovať. Napíšte dotaz, ktorý upraví existujúcu štruktúru tabuliek tak, aby pre každé pridelenie bolo možné evidovať termín, dokedy študent musí test vypracovať.

5. Doplňte na koniec súboru `testy.sql` vytvorenie `VIEW student_results`, ktoré sprístupňuje výsledky študentov v podobe sedmíc `Meno, Priezvisko, NazovTestu, CasPridelenia, CasVypracovania, VysledokPercenta, ZodpovedaneOtazky`, kde
	* `NazovTestu` je názov testu, ktorý bol v čase `CasPridelenia` pridelený študentovi s daným menom a priezviskom;
	* ak študent test už robil, `CasVypracovania` je čas posledného vypracovania testu, `VysledokPercenta` je podiel správnych odpovedí k celkovému počtu otázok testu v tomto čase (zaokrúhlený na celé percentá), a `ZodpovedaneOtazky` je počet otázok, ktoré študent zodpovedal (správne či nesprávne);
	* ak študent test ešte nerobil, `CasVypracovania`, `VysledokPercenta` a `ZodpovedaneOtazky` su `NULL`.


### Technické pokyny

* Termín na odovzdanie: **02. 12. 2024**.
* Používajte korektnú syntax SQL podporovanú databázou SQLite 3.34 alebo Postgresql 13.17 (overiť si to môžete trebárs na serveri `cvika.dcs.fmph.uniba.sk`). **Pred voľbou DBMS** si pozrite [zadanie úlohy 3](../du3/du3.md).
* Riešenia so syntaktickými chybami budú hodnotené len malým počtom bodov.
* Súbor `testy.sql` odošlite ako prílohu e-mailu s predmetom `DAV-DU2` na adresu `jan.mazak@fmph.uniba.sk`.
