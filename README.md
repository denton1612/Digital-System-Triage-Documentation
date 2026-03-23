# Digital Triage System (DTS)

## 🩺 Prezentare Generală
**Digital Triage System (DTS)** este o aplicație web inteligentă concepută pentru a automatiza și îmbunătăți procesul de triaj medical, cu un focus special pe spitalele din România. Soluția își propune să reducă timpii lungi de așteptare, erorile în clasificarea urgențelor și presiunea asupra personalului medical, înlocuind triajul complet manual cu unul asistat de Inteligența Artificială.

Sistemul colectează datele vitale, simptomele și istoricul medical ale pacienților și estimează nivelul de urgență folosind algoritmi AI avansați. Personalul medical poate vizualiza apoi un tablou de bord (dashboard) actualizat în timp real, cu lista pacienților așezați în ordinea priorităților.

### ✨ Funcționalități Principale
1. **Formular digital de triaj** - Colectare automată de simptome, semne vitale și istoric medical.
2. **Algoritm AI pentru clasificarea urgențelor** - Estimarea nivelului de urgență pe baza datelor.
3. **Medical Dashboard** - Afișarea pacienților în ordinea priorității, cu actualizări live.
4. **Autentificare și Role Management** - Acces securizat pentru medici, asistente și admini.
5. **Integrare HIS/EMR** - Sincronizare cu sistemele existente ale spitalului.

### 🛠 Tehnologii Utilizate
* **Backend:** Python (FastAPI) - pentru API și logica de triaj AI.
* **Frontend:** React + TypeScript - pentru o interfață web responsivă.
* **Bază de Date:** PostgreSQL - pentru stocarea securizată.
* **AI/ML Layer:** Modele predictive bazate pe NLP (Natural Language Processing) folosind arhitecturi Transformer.

---

## 🧠 Implementarea AI (Arhitectură și Modele)

Subsistemul de Inteligență Artificială a fost dezvoltat și testat pe baza setului de date **MIMIC-III** (cu peste 40.000 de pacienți de la terapie intensivă). Inputul principal al rețelelor neurale constă în note clinice textuale (precum simptomele principale - *Chief Complaint* și istoricul bolii curente - *History of Present Illness*).

Sistemul AI este compus din două module majore:
1. **Routing Module (Modulul de Direcționare):** Extrage entitățile medicale și direcționează pacientul către una dintre cele 9 specializări medicale (ex. Cardiologie, Neurologie).
2. **Risk Assessment Module (Modulul de Evaluare a Riscului):** Evaluează severitatea pentru a prezice nevoia internării (*Discharge Disposition*).

### Modele Evaluate și Performanțe
Pentru a naviga prin complexitatea textelor medicale scrise liber (fără formatare strictă, cu abrevieri și zgomot) au fost antrenate și comparate patru arhitecturi bazate pe Transformer:

1. **ClinicalBERT:**
   * **Bază:** Antrenat pe documente clinice MIMIC-III.
   * **Performanță (Proof-of-Concept):** ~58% acuratețe. S-a descurcat bine pe clasele majoritare ("Acasă"), dar a întâmpinat dificultăți la cazurile foarte rare din cauza setului de date inițial dezechilibrat. 
2. **PubMedBERT:**
   * **Bază:** Pre-antrenat exclusiv pe literatură biomedicală (abstracte PubMed).
   * **Performanță:** ~63% acuratețe (F1-score 0.59). A demonstrat că modelele specializate direct pe limbaj medical extrag mult mai bine sensul din notițele de triaj comparativ cu cele generale.
3. **RoBERTa:**
   * **Bază:** Model NLP de uz general.
   * **Performanță:** Folosit pe post de control ("negative control"). A obținut doar 51.6% acuratețe, arătând că lipsa vocabularului medical duce la performanțe slabe în clasificările de specialitate. Ulterior, a fost optimizat și curățat pentru prezicerea setului de 101 proceduri chirurgicale.
4. **BioBERT:**
   * **Bază:** Creat pentru procesarea de texte biomedicale.
   * **Performanță & Optimizare:** A fost folosit în principal pentru **Modulul de Direcționare** (clasificarea pe cele 9 specializări: Cardiologie, Pneumologie, etc.). A fost rafinat pentru a înțelege și negațiile (ex. *denies chest pain*) și testat folosind funcții de pierdere ponderate (*Weighted Cross-Entropy Loss*) pentru a reduce bias-ul claselor majoritare.

### Concluzii AI
Testele efectuate demonstrează capabilitatea sistemului de a înțelege *chief complaints* și a face asocierea cu o clasificare corectă, fie că este vorba despre gradul de risc sau de direcționarea spre un specialist. **PubMedBERT** și **BioBERT** cu funcții de pierdere ponderate s-au dovedit a fi alegerile optime.

---

## 👩‍💻 Contribuția Mea

<!-- 
AICI TREBUIE SĂ COMPLETEZI CU CONTRIBUȚIA TA EFECTIVĂ LA PROIECT.
Idei de completat:
- Ce module ai dezvoltat (ex: Frontend, Backend API, antrenarea unui anumit model de AI, baza de date)?
- Ce funcționalități specifice ai implementat?
- Probleme întâlnite de tine și cum le-ai rezolvat?
-->

* [Adaugă aici detalii despre rolul tău în cadrul echipei]
* [Exemple: Am integrat modelul X în API-ul de FastAPI / Am creat dashboard-ul în React / Am lucrat la curățarea datelor din MIMIC-III, etc.]
* [ ... ]

---

## 👥 Echipa de Dezvoltare
Acest proiect de echipă a fost realizat de:
* Țăpuc Delia
* Titieni Paul
* Știube Denis
* Costan Alex