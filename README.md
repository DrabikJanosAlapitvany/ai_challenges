# AI Kihívások


A Mesterséges Intelligencia új lehetőségegket kínál az az elhallgatott információk terjesztésére, amivel az alapítvány élni szeretne.
Az MI-t hosszú távon szeretnénk bevonni Drábik János kutatási anyagainak levéltári feldolgozásába.
A legelső lépés a videók feldolgozása, a technológia mélyebb megismerése.

Egy példavideón keresztül szeretnénk megérteni, hogy az MI jelenleg milyen költségekkel és milyen minőségben képes elvégezni az alább felsorolt feladatokat.

A példavideó:
[Dr Drábik János: Civil a pályán: vita szeptember 11-ről 2006.09.11.](https://www.youtube.com/watch?v=yzcLAEvrcxE)

# Feladatok
video->szöveg
  1. szöveges átirat (akár egy egyszerű txt formátum is jó de legjobb a géppel könnyen feldolgozható, struktúrált verzió: időbélyeg annotációk, beszélő, aggresszív-e?, stb.)
  2. feliratozás (feliratokat kezelő videóformátum választásával vagy youtube API-val)
  3. adott terjedelmű kivonat készítése

videó->hang

  4. angol verzió elkészítése eredeti hangszínekkel, intonációval

videó->videó

  5. sarkalatosabb kijelentések, érdekesebb részek kikeresése/kivágása (rövidfilmekhez egyéb csatornákra)

szöveg->hang

  6. szöveg felolvasása Drábik János hangszínével.

# Megoldás

Megoldásnak tekintjük az alábbiak bármelyikét:
  - programkód
  - konkrét AI modell és javaslatok a  prompt összeállítására (egy .md fájl javasolt erre)
  - az AI modell kimenete (videók, szövegek, hangsávok)

(A kiterjesztésből látszódni fog, hogy melyik opcióról van szó.
Példák: `1.txt`, `1.json`, `4.mp3`, `4.md`, `5.py`)

A publikus megoldásokat egy-egy git branch-be várjuk ide, hogy mindenki tanulhasson belőle. 
Privát megoldásokat a drabikjanosalapitvany@gmail.com címre kérjük küldeni.

A megoldásokból szeretnénk egy automatizált folyamatot építeni, minden videóra lefuttatni.


(Az 5. feladat kivételével a kimenetek mind kis méretű állományok. Az 5. feladat kimeneti formátuma legyen timestamp-elt youtube linkek listája időtartammal(sec).
Pl. `["https://www.youtube.com/watch?v=yzcLAEvrcxE&t=13m30s", 30.4]`)

Részmegoldásokat is örömmel fogadunk. A feladat sorszáma minden esetben legyen feltüntetve akár a fájlok szintjén, akoár egy fájlon belül.

Köszönjük, hogy időt szán ránk!
Drábik János Alapítvány

# Hasznos linkek

[Hugging Face Spaces](https://huggingface.co/spaces)
[Youtube downloader](https://downr.org/)
