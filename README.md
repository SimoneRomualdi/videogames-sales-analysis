# Video Games Sales — Analisi Esplorativa

## Executive Summary

- **Problema di Business**: Il dataset sulle vendite di videogiochi presentava dati grezzi con duplicati, valori nulli, colonne non standardizzate e outlier che rendevano impossibile ricavare insight affidabili direttamente dalla sorgente.
- **Soluzione**: Pipeline completa di data cleaning e analisi esplorativa in Python (Pandas, Matplotlib, Seaborn) che trasforma i dati grezzi in un dataset pulito e pronto per il reporting, completata da quattro visualizzazioni chiave.
- **Risultati**: Dataset ridotto da 5.909 a 5.893 righe dopo la rimozione di 16 duplicati; tutti i 39 valori nulli risolti con strategie di imputazione contestuale; colonna `NA_Sales` convertita da stringa a numerico; outlier cappati al 95° percentile per preservare la distribuzione; quattro visualizzazioni prodotte su vendite regionali, distribuzione per genere, quota di mercato e andamento temporale.
- **Prossimi Passi**: Collegare il dataset pulito a una dashboard interattiva (Power BI o Tableau); approfondire l'analisi con modelli predittivi sulle vendite future; estendere la segmentazione ai publisher.

---

## Problema di Business

I dati di vendita di videogiochi provenivano da una sorgente unica ma disomogenea: nomi di paese non standardizzati (`"United States"` vs `"USA"`), valori di vendita formattati come stringhe con simbolo valuta, regioni mancanti e righe duplicate. Rispondere a domande come *"Qual è la regione con le vendite più alte?"* o *"Quali generi dominano il mercato?"* era impossibile senza prima pulire e strutturare il dato. L'obiettivo era costruire un dataset affidabile su cui condurre analisi concrete di mercato.

---

## Metodologia

1. **Esplorazione iniziale** → Ispezione della struttura (5.909 righe × 15 colonne), tipi di dato, prime righe e conteggio valori nulli per colonna.
2. **Rimozione duplicati** → Identificate e rimosse 16 righe duplicate; dataset ridotto a 5.893 righe.
3. **Gestione valori nulli** → `Publisher`: 12 nulli sostituiti con `"Unknown"`. `Region`: 27 nulli risolti con imputazione a cascata — prima tramite mapping città → regione, poi paese → regione come fallback.
4. **Normalizzazione colonne** → `NA_Sales` ripulita dal simbolo `$` e convertita in `float64`; colonne rinominate per coerenza (`NA_Sales` → `National Sales`, ecc.); `"United States"` normalizzato in `"USA"`.
5. **Gestione outlier** → Capping al 95° percentile per `National Sales` (soglia: 2.07) e `Global Sales` (soglia: ~4.04) per eliminare valori estremi senza perdere righe.
6. **Analisi e visualizzazioni** → Quattro grafici su vendite regionali, distribuzione nei top 3 generi, quota di mercato per paese e andamento temporale.

---

## Competenze

- **Python**: Pandas (`groupby`, `fillna`, `replace`, `rename`, `quantile`, `drop_duplicates`), NumPy (`where` per il capping)
- **Visualizzazione**: Matplotlib, Seaborn (barplot, boxplot, pie chart, line chart)
- **Data Cleaning**: gestione valori nulli con strategie di imputazione contestuale, normalizzazione stringhe, conversione di tipo, capping outlier

---

## Risultati & Raccomandazioni

- **Vendite regionali**: La regione West degli USA guida le vendite nazionali (801M), seguita da West Australia (687M) ed East USA (673M) — il mercato americano è dominante e va presidiato con priorità.
- **Top generi**: Action, Sports e Shooter sono i tre generi con le vendite nazionali più alte; la distribuzione per paese mostra che l'Australia ha una varianza maggiore, segnalando mercati meno prevedibili.
- **Quota di mercato**: Gli USA concentrano la maggior parte delle vendite sia nazionali che globali, con l'Australia come unico altro mercato significativo nel dataset — suggerisce di espandere la raccolta dati ad altri paesi per un'analisi più completa.
- **Andamento temporale**: Le vendite mostrano un picco nell'anno coperto dal dataset, con un trend leggibile; un'analisi multi-anno più granulare permetterebbe di identificare stagionalità e cicli di prodotto.
- **Nota tecnica**: La colonna `Region` per l'Australia presentava valori non allineati con quelli USA (es. `"North"`, `"Other"` non presenti negli USA). La strategia adottata — imputazione tramite mapping città/paese — è una soluzione pragmatica che andrebbe validata con il team di business prima di usarla in produzione.

---

## Prossimi Passi

1. Collegare il dataset pulito a Power BI o Tableau per dashboard interattive su vendite e quota di mercato.
2. Approfondire la segmentazione per publisher per identificare i player dominanti per genere e regione.
3. Estendere il dataset con dati di altri paesi per superare il bias geografico attuale (solo USA e Australia).
4. Costruire un modello predittivo semplice (es. regressione lineare) sulle vendite globali a partire da genere, piattaforma e anno.

---

## Struttura della Repository

```
VideoGamesSales-EDA/
├── VideoGamesSales.csv          # Dataset sorgente
├── VideoGamesProject.ipynb      # Notebook principale (cleaning + analisi)
└── README.md
```

**Stack**: Python · Pandas · NumPy · Matplotlib · Seaborn
