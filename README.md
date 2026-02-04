[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)]
(https://colab.research.google.com/github/modobasic/Racunalni-vid---projekt/blob/main/Multiscale_Morphological_Gland_Segmentation.ipynb)


# Višeskalna analiza žlijezdanih struktura pomoću morfoloških operacija

Ovaj repozitorij sadrži projekt iz područja računalnog vida koji se bavi segmentacijom žlijezdanih struktura na histopatološkim slikama korištenjem matematičke morfologije i višeskalne analize.  
Projekt je izrađen u okviru praktičnog zadatka kolegija i demonstrira utjecaj veličine strukturnih elemenata na detekciju malih i velikih žlijezdanih struktura.

---

## Cilj projekta

Cilj projekta je implementirati višeskalni morfološki pristup za segmentaciju žlijezda te analizirati kako izbor skale (veličine strukturnog elementa) utječe na kvalitetu segmentacije u kvantitativnom i vizualnom smislu.

Poseban naglasak stavljen je na:
- detekciju malih i velikih žlijezdanih struktura
- smanjenje šuma morfološkim operacijama
- usporedbu rezultata pomoću numeričkih metrika

---

## Dataset

Korišten je skup podataka:

**Warwick-QU (GlaS Challenge – MICCAI 2015)**  
- Tip: Histopatološke H&E obojene slike kolorektalnog tkiva  
- Rezolucija: 20× (0.62005 μm/piksel)  
- Format: BMP  
- Broj slika: 165  
- Oznake: Ground truth maske izradili patolozi  

Za svaku sliku postoji odgovarajuća binarna maska s oznakom žlijezdanih struktura (`*_anno.bmp`).

> Zbog ograničenja veličine i licence, dataset nije uključen u ovaj repozitorij.

---

## Metodologija

Segmentacijski sustav temelji se na matematičkoj morfologiji i sastoji se od sljedećih koraka:

1. Pretvorba slike u sivu razinu
2. Binarizacija slike primjenom Otsu metode
3. Morfološko otvaranje za uklanjanje šuma
4. Morfološko zatvaranje za popunjavanje rupa u strukturama
5. Višeskalna analiza s različitim veličinama strukturnih elemenata
6. Kombinacija rezultata svih skala logičkom OR operacijom
7. Evaluacija rezultata pomoću IoU i Dice koeficijenta

---

## Višeskalni pristup

Korištene su sljedeće konfiguracije skala:
- Mala skala: 3×3
- Srednja skala: 7×7
- Velika skala: 15×15
- Kombinacija: 3×3, 7×7 i 15×15

Na taj način omogućena je analiza utjecaja skale na:
- detekciju sitnih žlijezdanih struktura
- očuvanje većih regija
- razinu šuma u segmentiranoj slici

---

## Evaluacija

Rezultati segmentacije evaluirani su pomoću sljedećih metrika:

- **IoU (Intersection over Union)**  
  Omjer preklapanja predviđene maske i ground truth maske u odnosu na njihovu uniju.

- **Dice koeficijent**  
  Mjera sličnosti između dviju binarnih maski, osjetljivija na preklapanje manjih struktura.

Evaluacija je provedena na slučajnom uzorku slika iz skupa podataka za različite konfiguracije skala.

---

## Pokretanje u Google Colab-u

Projekt se može pokrenuti direktno u Google Colab okruženju klikom na gumb **Open in Colab** na vrhu ove stranice.

### Učitavanje dataseta
1. Preuzmi dataset s Kaggle platforme
2. Uploadaj ZIP datoteku u Google Drive ili direktno u Colab
3. U bilježnici pokreni sljedeće naredbe:

```python
from google.colab import drive
drive.mount('/content/drive')

!mkdir -p data
!unzip "/content/drive/MyDrive/datasets/Warwick_QU_Dataset.zip" -d data
