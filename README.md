# Netflix-adatok elemzése és osztályozása adatbányászati módszerekkel

Ez a projekt a Netflix filmek és sorozatok adatainak feldolgozását, elemzését és osztályozását mutatja be.  
A cél a teljes adatbányászati folyamat végig vitele: **adattisztítás → EDA → hipotézisvizsgálat → gépi tanulás**.

---

## Dataset
A felhasznált adathalmaz:  
**Netflix Movies and TV Shows (Kaggle)**  
https://www.kaggle.com/datasets/shivamb/netflix-shows

Input fájl: `netflix_titles.csv`

---

## 1. Adattisztítás
- Típusok egységesítése (`Movie` / `TV Show`)
- Játékidő szétbontása: `duration_minutes`, `seasons`
- Ország, korhatár és szereplők normalizálása
- Műfajok binarizálása (Top 20)
- Hiányzó értékek kezelése

 Eredmény: **`netflix_cleaned.csv`**

---

## 2. Feltáró adatelemzés (EDA)
- Típusok megoszlása  
- Megjelenési évek eloszlása  
- Leggyakoribb korhatár-besorolások  
- Top országok  
- Filmek vs. sorozatok megjelenési évének összehasonlítása  

---

## 3. Hipotézisvizsgálat
**Hipotézis:** a sorozatok újabbak, mint a filmek  
Teszt: *Mann–Whitney U*  
Eredmény: **szignifikáns különbség (p ≪ 0.001)**

---

## 4. Osztályozó modell
**Cél:** előjelezni, hogy egy tartalom film vagy sorozat

Modell: *Logistic Regression*  
Előfeldolgozás:
- medián imputáció  
- standardizálás  
- One-Hot Encoding  

**Eredmények:**
- Pontosság: ~95%
- ROC–AUC: ~0.97
- Konfúziós mátrix a repo-ban

---

## Futtatás
```bash
pip install -r requirements.txt
python netflix_analysis.py
