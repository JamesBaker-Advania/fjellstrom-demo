# Fjellstrøm Energi – demosida för CX Forum

En påhittad "Min side" för elbolaget Fjellstrøm Energi, med Genesys Cloud Web Messenger. Ingrid Haugen är inloggad, och sidan skickar `customer_id` och `customer_first_name` som custom attributes. Message flow-et läser dem och skickar dem vidare till AVA:n.

| Del | Värde |
| --- | --- |
| Messenger-deployment | Fjellstrøm Energi Demo (`847dcad8-e98f-4edc-933b-bed37c858022`) |
| Messenger-konfiguration | Fjellstrøm Energi Messenger (v2, startar konversationen automatiskt) |
| Region | prod-euc1 (`apps.mypurecloud.de`) |
| Inbound message flow | Fjellstrøm Energi Inbound Message |
| Demokund | FS-100234, Ingrid |

## Köra lokalt

```bash
cd fjellstrom-demo-site
python3 -m http.server 8765
```

Öppna sedan http://localhost:8765. Messenger fungerar inte från `file://`, så sidan måste serveras över http eller https.

## Publicera på GitHub Pages

1. Skapa ett nytt repo på GitHub, till exempel `fjellstrom-demo`. Det kan vara privat om ditt konto har Pages för privata repon, annars publikt. Sidan innehåller bara fiktiva uppgifter och deployment-id:t, som inte är hemligt.
2. Ladda upp `index.html` (och gärna den här README:n), antingen via **Add file → Upload files** på GitHub eller med git:

   ```bash
   cd fjellstrom-demo-site
   git init -b main
   git add index.html README.md
   git commit -m "Fjellstrøm demosida"
   git remote add origin https://github.com/<ditt-konto>/fjellstrom-demo.git
   git push -u origin main
   ```
3. Gå till repot och välj **Settings → Pages**. Under *Build and deployment* väljer du **Deploy from a branch**, branch `main` och mappen `/ (root)`. Klicka **Save**.
4. Vänta 1–2 minuter. Adressen visas överst på samma sida: `https://<ditt-konto>.github.io/fjellstrom-demo/`.
5. Lås deploymenten till din domän: **Admin → Message → Messenger Deployments → Fjellstrøm Energi Demo**. Slå av *Allow all domains* och lägg till `<ditt-konto>.github.io` (och gärna `localhost` för lokal körning). Spara. Deploymenten tillåter just nu alla domäner så att den fungerar direkt.

## Under demot

- **Chat med oss** eller den gröna knappen öppnar Messenger. AVA:n hälsar "Hej Ingrid! Jag ser att du är inloggad".
- **Ny demo-chat** (nere till vänster) avslutar konversationen och rensar sessionen, så att nästa körning börjar om från hälsningen.
- **Visa som gäst** (`?guest` i adressen) visar en kund som inte är inloggad. AVA:n frågar då efter kundnummer.
- Presentatörsrutan döljs på smala skärmar.

## Alternativ till GitHub Pages

Netlify Drop (app.netlify.com/drop) är snabbast: dra mappen dit så får du en https-adress på några sekunder, utan git. Lägg då till den domänen i deploymenten i stället.
