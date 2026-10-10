# Weekly Standup - Concierge Partner

**Week of:** 19.10.2026 
**Participants:** Nikolas

---

## Status Pitanja - Recapitulation

| # | Pitanje | Status | Napomena |
|---|---------|--------|----------|
| 1 | Exely API (reservations + webhook/polling) | Cekam | Trebam potvrdu |
| 2 | Export baze (JSON + opis polja) | Cekam | Trebam sample + opis od partnera |
| 3 | Brojevi (rezervacije/mesec, vreme/rezervaciju) | Cekam | Osnova za cenu |
| 4 | Prijem novih objekata (onboarding) | Nejasno | Ide preko API? Poruka se upisuje u bazu? |
| 5 | Jezici (engleski zasad) | OK | Production > ostali jezici auto |
| 6 | Starenje razgovora (T1/T2 pragovi) | Cekam | Potrebni pragovi po temi |

**Dodatno #7:** Trebaju SVE poruke koje su dosad klijenti poslali - potrebne za update baze

---

## Sta je Uradeno Ove Nedelje
Zoran - dobio pristup Exely
      - treba da uradi detaljnu analizu API
A: radila na exportu poruka


### Razvoj opsti
Z:API kratka analiza ponuda (umesto Exely API):
   1. Channex- $130/month, plus $7 per connected hotel OR $0.50 per vacation rental unit
   2. Rentals United-Nema javne cene, kontakt za quote
   3. WebBookingPro - "most competitive prices" — ali nema javne cene, treba kontakt

A:Formular za onboarding
SVI: implemantacija onboardinga

KA:Starenje razgovora: Ponasanje bota kad gost prekine razgovor:dokumentacija
Z:implementacija
KAZ:test


### Testing
  - Najmanje 2+ klijenta + 1 dispecer
  - Bot mora pratiti vise klijenata nezavisno (BITNO!)
  - onboarding sistem

## Plan za Sledecu Nedelju
1. Raditi na pitanju #7 kad se dobiju poruke (analiza i eventualna dopuna 'STRUJE' scenarija)

### Prioritet 1 (Blocker)
**#7:** Trebaju SVE poruke koje su dosad klijenti poslali - potrebne za update baze

4. ko i kako priprema dokumentaciju za test scenarije, mora dokumentovano


### Prioritet 2 (Razvoj)
- Poboljšanja na bot logici - odluka nakon testa
- Dodatni test scenariji
- Dokumentovati ovo : Ponasanje bota kad gost prekine razgovor:

### Prioritet 3 (Infrastruktura)
- (TBD nakon test rezultata)
K:Z razmisljati o platformi za DEPLOY

---

## Za Kasnije (Backlog - Faza 2+)

- **WhatsApp integracija** (čekamo provider odluku)
- **Drugi jezici** (kada preiđemo u production)
- **Load balancing za workere** (sada je "prvi dostupan")
- **LLM fallback** za van-teme pitanja (proof of concept)
- **Mobile app** za dispečere (post-MVP)

---

## Partner Decisions - Aktivni

### Hitno sada
- [ ] **Pitanje #1**: Exely API - potvrda webhook/polling
- [ ] **Pitanje #2**: Export baze - sample + opis polja
- [ ] **Pitanje #3**: 
- [ ] **Pitanje #4**: 
- [ ] **Pitanje #6**: Pragovi po temi (T1, T2 vremenske vrednosti)


### Za sledeci standup


---

## Diskusija / Napomene

### Starenje razgovora - Model

Ponasanje bota kad gost prekine razgovor:

**Mehanizam - dvostepeno starenje:**

1. **Prag T1 (prvi podsetnik)**
   - Posle T1 vremena od poslednje poruke gosta, bot posalje ONE blag podsetnik
   - Primer: "Jos ste tu? Je l' pomogao restart Wi-Fi-ja?"
   - Tacno jednom - ne ponavlja se, da ne bude spam
   - Korisno: gost se vrati i bot ga pokupi gde su stali

2. **Prag T2 (parkiranje)**
   - Ako i nakon T1 nema odgovora tokom T2 vremena, bot oznaci kao "no_response"
   - Razgovor se parkira iz aktivne logike

3. **Izuzetak - rad koji je vec u toku**
   - Ako je majstor vec poslat, gostova tisina NE otkazuje posao
   - Majstor dolazi; bot samo parkira ono sto ceka od gosta
   - Status: `context.worker_notified = true`

**Potrebni pragovi od partnera po temi:**

- **Hitne** (brave, kljuc): T1 = 2-5 min, T2 = 15-30 min
- **Srednje** (WiFi, voda, struja): T1 = 30 min, T2 = 4 sata
- **Lagane** (jastuki, preporuke): T1 = 1-2 sata, T2 = 24 sata

---

## Sledeci Standup

**Datum:** [DD.MM.YYYY]
**Vreme:** [HH:MM]
**Format:** [Zoom/meet link ili opis]

---

## Attachments / References

- [[pitanja-za-partnera]] - detaljna pitanja sa kontekstom
- [[architecture]] - tehnicka dokumentacija
- [[CLAUDE.md]] - repo konvencije i komande
