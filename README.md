# Netflix-adatok elemzése és osztályozása adatbányászati módszerekkel

Ez a projekt a Netflix filmek és sorozatok adatainak feldolgozását, elemzését és osztályozását mutatja be.  
A cél a teljes adatbányászati folyamat végig vitele:

**Adattisztítás → EDA → hipotézisvizsgálat → gépi tanulás**

---

## Dataset

A felhasznált adathalmaz:

**Netflix Movies and TV Shows (Kaggle)**  
https://www.kaggle.com/datasets/shivamb/netflix-shows

Bemeneti fájl:
- `netflix_titles.csv`

A tisztítás után keletkező fájl:
- **`netflix_cleaned.csv`** ← *minden további elemzés ebből fut*

---

## 1. Adattisztítás

A főbb lépések:

- Tartalomtípusok egységesítése (`Movie` / `TV Show`)
- Játékidő feldarabolása:
  - `duration_minutes`
  - `seasons`
- Ország, korhatár és szereplők egységesítése
- Top 20 műfaj binarizálása (`genre_*`)
- Hiányzó értékek kezelése
- Output fájl mentése → **`netflix_cleaned.csv`**

---

## 2. Feltáró adatelemzés (EDA)

A projekt az alábbi kérdéseket vizsgálja:

- Filmek és sorozatok aránya
- Megjelenési évek eloszlása
- Top korhatár-besorolások
- Országok szerinti megoszlás
- Filmek vs. sorozatok megjelenési évének összehasonlítása
- Numerikus jellemzők korrelációja

Az összes ábra megtalálható a `images/` könyvtárban.

---

## 3. Hipotézisvizsgálat

**Hipotézis:**  
A sorozatok átlagosan újabbak, mint a filmek.

**Módszer:**  
*Mann–Whitney U próba* (nem paraméteres)

**Eredmény:**  
- p-érték: **p ≪ 0.001**
- Következtetés: **szignifikáns különbség**, a sorozatok jellemzően frissebbek.

---

## 4. Osztályozó modell

**Cél:**  
Megjósolni, hogy egy tartalom *Movie* vagy *TV Show*.

**Modell:**  
`LogisticRegression`

**Előfeldolgozás (Pipeline):**

- medián imputáció (numerikus mezők)
- standardizálás (`StandardScaler`)
- kategóriák One-Hot Encode-olása
- műfajindikátorok kezelése

**Használt jellemzők:**

- `release_year`
- `duration_minutes`
- `seasons`
- `cast_count`
- `rating_clean`
- `country_main`
- `genre_*` (top 20 műfaj)

**Eredmények:**

- Pontosság: **~0.95**
- ROC–AUC: **~0.97**
- Keresztvalidáció (5-fold): **0.996 átlagpontosság**
- Konfúziós mátrix: megtalálható a `images/plot_confusion_matrix.png` fájlban

---

## Futtatás

```bash
pip install -r requirements.txt
python netflix_analysis.py
