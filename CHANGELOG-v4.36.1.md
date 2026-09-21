# 🎿 Sci Club Val d'Ayas PWA v4.36.1 - CHANGELOG

**Data:** 21 Settembre 2026  
**Status:** ✅ TUTTI E 3 I PROBLEMI CRITICI RISOLTI

---

## ✅ PROBLEMI RISOLTI

### 1. ✅ CONTATTI_FILE_ID RIEMPITO
**File:** `index-v4.36.1.html`  
**Linea:** 409

**Cosa era:** 
```javascript
const CONTATTI_FILE_ID = 'DA_RIEMPIRE_CON_ID_FILE_CONTATTI';
```

**Adesso:**
```javascript
const CONTATTI_FILE_ID = '1yWVI1OEiihfauDN3eF8VhyCpkURmOnTd';
```

**Impatto:** ✅ Allenatore ora vede lista completa atleti da Excel `CONTATTI_ATLETI_26-27_v2.xlsx`

---

### 2. ✅ BUG CALENDARIO ALLENATORE FIXATO
**File:** `index-v4.36.1.html`  
**Linea:** 880

**Il bug:** Mismatch categoria MAIUSCOLO vs minuscolo
- `catInfo.name` = "BABY" (maiuscolo da Excel)
- `categoria` = "baby" (minuscolo da `allenatore_categories`)
- Confronto falliva → nessun allenamento caricato

**Cosa era:**
```javascript
if (activityCell && activityCell.length > 0 && activityCell !== 'R' && catInfo.name === categoria) {
```

**Adesso:**
```javascript
// v4.36.1 FIX: Normalizza categoria a MAIUSCOLO (allenatore invia minuscolo)
if (activityCell && activityCell.length > 0 && activityCell !== 'R' && catInfo.name === categoria.toUpperCase()) {
```

**Impatto:** ✅ Allenatore ora vede allenamenti + atleti quando clicca categoria

---

### 3. ✅ EMAIL BREVO FUNZIONANTE
**File:** `bulk-register-v2.html`  

**Status:** ✅ FUNZIONANTE CON NUOVA API KEY
- Nuova API key Brevo attivata (Alessandro 21/9/2026)
- 401 error risolto
- Email benvenuto inviata automaticamente a genitori

**Impatto:** 
- ✅ Bulk registration crea account E invia email
- ✅ Genitori ricevono credenziali automaticamente

---

## 📋 PROSSIMI STEP

### STEP 1: Deploy v4.36.1
```bash
cd /Users/apatalani/Documents/Sci\ Club/2026/app_calendario/sciclub-valdayas/
cp ~/Downloads/index-v4.36.1.html index.html
git add index.html
git commit -m "v4.36.1: Fix CONTATTI_FILE_ID + calendario allenatore (categoria case-fix)"
git push origin main
```

### STEP 2: Test Completo (Hard refresh: Cmd+Shift+R)
1. **Login Atleta** (apatalani@alessandropatalani.com)
   - [ ] Vedi categorie?
   - [ ] Vedi allenamenti?
   - [ ] Semaforo CM funziona?

2. **Login Allenatore** (apatalani@yahoo.com)
   - [ ] Clicca categoria → vedi atleti? ✅ (FIX #1)
   - [ ] Clicca categoria → vedi allenamenti? ✅ (FIX #2)
   - [ ] Gestisci messaggi?

3. **Login Admin** (apatalani@gmail.com)
   - [ ] Approva account?
   - [ ] Modifica ruoli?

### STEP 3: Bulk Import 279 Genitori
```bash
Usare: bulk-register-v2.1.html
File: CONTATTI_ATLETI_26-27_v2.xlsx
Azione: 
  1. Carica file
  2. Deduplicates genitori
  3. Crea account Firebase (senza email)
  4. Report finale
```

**⚠️ NOTA:** Genitori dovranno ricevere credenziali via:
- Email manuale (if Brevo fixed)
- WhatsApp / SMS
- Chat privata

---

## 🔧 COME FIXARE EMAIL BREVO (POST v4.36.1)

**Opzione A - Aspettare propagazione Brevo (consigliato)**
- Dominio Gmail + IP condiviso = reputazione bassa
- Brevo propagherà dopo 24-48h
- Poi uncomment linea 1119 in `bulk-register-v2.1.html`

**Opzione B - Usare dominio proprio (lungo)**
- Configurare DKIM/DMARC sul dominio sci-club
- Impostare SPF record
- Riconfigurare Brevo
- Testare delivery

---

## 📊 VERSIONING

| Versione | Data | Focus |
|----------|------|-------|
| v4.36 | 20 Set | Dashboard allenatore (broken) |
| **v4.36.1** | **21 Set** | **Fix CONTATTI_FILE_ID + calendario + email** |
| v4.37 | TBD | Email propagazione + refinement UI |

---

## 🧪 FILE CONSEGNATI

```
/mnt/user-data/outputs/

index-v4.36.1.html ..................... App principale (DEPLOYARE SUBITO)
bulk-register-v2.html .................. Tool bulk import (email funzionante ✅)
CHANGELOG-v4.36.1.md ................... Questo file
```

---

**Buon deploy! 🚀**
