# BuildDraft.gr — φωτογραφίες προϊόντων

Οι φωτογραφίες προϊόντων του [BuildDraft.gr](https://github.com/TeoAmpatzis/gpu-prices-gr), μία ανά μοντέλο, σε WebP 96 και 320 px. Τις κατεβάζει το workflow `images` (κώδικας: `scraper/images.py` στο κύριο repo) μετά από κάθε ενημέρωση τιμών και δημοσιεύονται εδώ μέσω GitHub Pages· το site τις σερβίρει από το δικό του domain (`/img/…`, Vercel).

- `img/<κατηγορία>/<id>-96.webp`, `-320.webp`: φωτογραφίες προϊόντων (από τις σελίδες των BestPrice, Shopflix, Skroutz, Snif). Ανήκουν στους κατόχους τους (κατασκευαστές και καταστήματα).
- `index.json`: ποια μοντέλα έχουν φωτογραφία και από πού. `failed.json`: μοντέλα χωρίς χρήσιμη φωτογραφία (νέα προσπάθεια μετά από 7 ημέρες).
- `blocklist.json`: μοντέλα που δεν κατεβαίνουν ποτέ.

## Αφαίρεση φωτογραφίας (αίτημα κατόχου)

1. Προσθέστε το μοντέλο στο `blocklist.json`:
   ```json
   [{ "cat": "gpu", "model": "RTX 5060 8GB", "reason": "αίτημα κατόχου", "date": "2026-10-01" }]
   ```
   (`model` = το κλειδί του μοντέλου, όπως στο `public/data/<cat>/image_urls.json` του κύριου repo· εναλλακτικά `{ "id": "<id>" }`).
2. Διαγράψτε τα `img/<cat>/<id>-96.webp` και `-320.webp`. Το id: `python scraper/images.py --id gpu "RTX 5060 8GB"`. (Αν το ξεχάσετε, το επόμενο workflow τα διαγράφει μόνο του μαζί με την εγγραφή στο `index.json`.)
3. Commit. Η φωτογραφία φεύγει από το site μέσα σε 24 ώρες (cache), ή αμέσως με «Purge CDN cache» στο Vercel.

Product photos belong to their respective owners and are removed on request (contact: see the site's Contact page).
