# U4-W3-D1
esercizi DQL
1 - Estrai tutti i clienti con nome Mario:
SELECT * FROM clienti WHERE nome = 'Mario';

2 - Estrarre il nome e il cognome dei clienti nati nel 1982:
SELECT nome, cognome FROM clienti WHERE EXTRACT(YEAR FROM anno_di_nascita) = 1982;

3 - Estrarre il numero delle fatture con IVA al 20%:
SELECT COUNT(*) FROM fatture WHERE iva = 20;

4 - Estrarre i prodotti attivati nel 2017 e che sono in produzione oppure in commercio:
SELECT * FROM prodotti 
WHERE EXTRACT(YEAR FROM data_attivazione) = 2017 AND (in_produzione = TRUE OR in_commercio = TRUE);

5- Estrarre le fatture con importo inferiore a 1000 e i dati dei clienti ad esse collegate:
SELECT f.*, c.* FROM fatture f 
JOIN clienti c ON f.id_cliente = c.numero_cliente WHERE f.importo < 1000;

6 - Riportare l’elenco delle fatture (numero, importo, iva e data) con in aggiunta il nome del fornitore:
SELECT f.numero_fattura, f.importo, f.iva, f.data_fattura, fo.denominazione 
FROM fatture f JOIN fornitori fo ON f.numero_fornitore = fo.numero_fornitore;

7 -  Considerando soltanto le fatture con IVA al 20 per cento, estrarre il numero di fatture per ogni anno:
SELECT EXTRACT(YEAR FROM data_fattura) AS anno, COUNT(*) AS numero_fatture 
FROM fatture WHERE iva = 20 
GROUP BY anno ORDER BY anno;

8 - Riportare il numero di fatture e la somma dei relativi importi divisi per anno di fatturazione:
SELECT EXTRACT(YEAR FROM data_fattura) AS anno, COUNT(*) AS numero_fatture, SUM(importo) AS totale_importi 
FROM fatture 
GROUP BY anno ORDER BY anno;
