# AI Kihívások


A Mesterséges Intelligencia új lehetőségegket kínál az az elhallgatott információk terjesztésére, amivel az alapítvány élni szeretne.
Az MI-t hosszú távon szeretnénk bevonni Drábik János kutatási anyagainak levéltári feldolgozásába.
A legelső lépés a videók feldolgozása, a technológia mélyebb megismerése.

Egy példavideón keresztül szeretnénk megérteni, hogy az MI jelenleg milyen költségekkel és milyen minőségben képes elvégezni az alább felsorolt feladatokat.

A példavideó:
[Dr Drábik János: Civil a pályán: vita szeptember 11-ről 2006.09.11.](https://www.youtube.com/watch?v=yzcLAEvrcxE)

# Feladatok
video->szöveg
  1. szöveges átirat (akár egy egyszerű txt formátum is jó de legjobb a géppel könnyen feldolgozható, struktúrált verzió: időbélyeg annotációk, beszélő, aggresszív-e?, stb*.)
  2. feliratozás (feliratokat kezelő videóformátum választásával vagy youtube API-val)
  3. adott terjedelmű kivonat készítése

videó->hang

  4. angol verzió elkészítése eredeti hangszínekkel, intonációval

videó->videó

  5. sarkalatosabb kijelentések, érdekesebb részek kikeresése/kivágása (rövidfilmekhez egyéb csatornákra)

szöveg->hang

  6. szöveg felolvasása Drábik János hangszínével.

*Annotációk:
 - beszélő: pannote.audio (de facto standard már)
 - időbélyeg: ?
 - beszéd módja: ?

# Követelmények

Megoldásnak tekintjük az alábbiak bármelyikét:
  - programkód
  - konkrét AI modell és javaslatok a  prompt összeállítására (egy .md fájl javasolt erre)
  - az AI modell kimenete (videók, szövegek, hangsávok)

A megoldások költségeiről is szeretnénk képet kapni. (Idő, pénz főleg, de  memória, tárhely is, ha jelentős.)

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

[Youtube downloader](https://downr.org/)


[Hugging Face Spaces](https://huggingface.co/spaces)
 - [videó feliratozás](https://huggingface.co/spaces/k2-fsa/generate-subtitles-for-videos) kiválaszthatod a nyelvet, feltöltheted a videódat, és a rendszer azonnal elkészíti a letölthető .srt feliratfájlt. Olyan csúcsmodelleket használ, mint a Cohere Transcribe vagy a Qwen3 ASR.

Hugging Face Leaderboars (Adott problémakör megoldásainak összehasonlító oldalai)
 - [Leaderboard overview](https://huggingface.co/spaces/lmarena-ai/arena-leaderboard)
 - [Leaderboard finder](https://huggingface.co/spaces/OpenEvals/find-a-leaderboard)
 - [ASR (Automatic Speech Recognition, beszédfelismerés)](https://huggingface.co/spaces/hf-audio/open_asr_leaderboard) ([ASR blog](https://huggingface.co/blog/open-asr-leaderboard))


 - [Video Generation](https://huggingface.co/spaces/ArtificialAnalysis/Video-Generation-Arena-Leaderboard) (Az Arena összehasonlításnál ember választja ki, hogy két AI kimenete közül melyik a jobb.)
 - [Code generation](TODO)


# Segítség


## Kivonatolás

### Kóddal

Videó kivonatolása két lépésben
```python
from transformers import pipeline # pip install transformers torch

# 1. ASR
asr = pipeline("automatic-speech-recognition", model="openai/whisper-large-v3")
text = asr("video_hang.mp3")["text"]

# 2. Summarization LLM
summarizer = pipeline("summarization", model="facebook/bart-large-cnn")
summary = summarizer(text, max_length=150, min_length=50, do_sample=False)
print(summary[0]['summary_text'])
```

### LLM AI kéréssel:
prompt: "Készíts ebből a szövegből egy strukturált, jól olvasható, pontokba szedett kivonatot magyarul, a legfontosabb gondolatok kiemelésével!"

### Egyéb

Eightify vagy NoteGPT: Kifejezetten YouTube videókhoz fejlesztett bővítmények, amelyek másodpercek alatt készítenek fejezetekre bontott, időbélyeges összefoglalót bármilyen nyilvános videóból.

Alrite AI: Kiváló magyar nyelvű rendszer, amely a videó feliratozása után egyetlen gombnyomásra elkészíti a szöveg rövidített, lényegi kivonatát.

Facebook / BART-large-cnn: Az egyik legstabilabb és legtöbbet letöltött célspecifikus modell [BART and T5](https://github.com/AmirHosseinSoleymani/Text-Summarization-with-HuggingFace)


# Áttekintő

Szabványosított tesztek modellek automatikus összehasonlítására (hard benchmarking): MMLU, GSM8K, MATH


Tesztkeretrendszerek:
  - LM-Evaluation Harness (EleutherAI): de facto standard
  - DeepEval (Confident AI): unit tesztelés
  - Lighteval (Hugging Face): gyors tesztelés (local/cloud)

RAG (saját adatokkal kiegészített modellek) keretrendszerei:
 - Ragas (Retrieval Augmented Generation Assessment): A legnépszerűbb keretrendszer a RAG-pipeline-ok értékelésére. Méri a kontextus relevanciáját, a hűséget (faithfulness) és a válasz pontosságát
Promptfoo
 - TruLens
 - Promptfoo

Biztonsági és sérülékenységi (Red Teaming) keretrendszerek:
 - Garak (LLM Vulnerability Scanner): Olyan az LLM-eknek, mint az nmap vagy a Nessus a hálózatbiztonságban. Sebezhetőségeket, adatvédelmi hibákat és hallucinációs réseket keres
 - Inspect (UK AI Safety Institute): Az Egyesült Királyság AI Biztonsági Intézete által fejlesztett, nagyszabású környezet a modellek alapvető képességeinek, kiberbiztonsági kockázatainak és autonómiájának tesztelésére
 - PyRIT (Python Risk Identification Tool): A Microsoft által nyílttá tett automatizált vörös-csapatos (red teaming) keretrendszer az AI rendszerek kockázatainak proaktív értékelésére




