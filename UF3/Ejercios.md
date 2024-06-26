```mysql
-- Ex1

SELECT e.nom, e.cognoms, d.nom
FROM empleats e
INNER JOIN departaments d ON d.departament_id = e.departament_id
ORDER BY d.nom, e.nom,e.cognoms;

-- Ex2

SELECT * FROM departaments;

SELECT d.departament_id, d.nom, l.adreca, l.codi_postal, l.ciutat
FROM departaments d
INNER JOIN localitzacions l ON l.localitzacio_id = d.localitzacio_id;

-- Ex3

SELECT d.departament_id, d.nom, l.adreca, l.codi_postal, l.ciutat
FROM departaments d
INNER JOIN localitzacions l ON l.localitzacio_id = d.localitzacio_id
WHERE d.nom = "Marketing";

-- Ex4

SELECT l.localitzacio_id ,l.estat_provincia, l.ciutat, p.nom AS Provincia, r.nom AS Regio
FROM localitzacions l
INNER JOIN paisos p ON l.pais_id = p.pais_id
INNER JOIN regions r ON r.regio_id = p.regio_id
-- WHERE l.localitzacio_id = 1400 OR l.localitzacio_id = 1700 OR l.localitzacio_id = 2500;
WHERE l.localitzacoi_id IN (1400,1700,2500);

-- Ex5

SELECT d.nom AS Departament, l.ciutat, COUNT(e.empleat_id) AS Num_empleats, round(AVG(e.salari),2) AS Salari_mig
FROM departaments d
INNER JOIN localitzacions l ON d.localitzacio_id = l.localitzacio_id
INNER JOIN empleats e ON e.departament_id = d.departament_id
GROUP BY d.departament_id
HAVING Salari_mig>6000
ORDER BY d.nom;

-- Ex6 

SELECT e.empleat_id, e.nom, e.cognoms, COUNT(h.feina_codi) AS NumFeines
FROM historial_feines h
INNER JOIN empleats e ON e.empleat_id = h.empleat_id
GROUP BY e.empleat_id
HAVING NumFeines > 1;

-- Ex7 

SELECT e.empleat_id, e.nom, e.cognoms, d.nom AS Departament, e.salari 
FROM empleats e
INNER JOIN departaments d ON d.departament_id = e.departament_id
WHERE e.salari IS NOT NULL
ORDER BY e.salari
LIMIT 1;

-- Ex8

SELECT e.empleat_id, e.nom, e.cognoms, e.data_contractacio,d.nom
FROM empleats e
INNER JOIN departaments d ON d.departament_id = e.departament_id
WHERE e.salari BETWEEN 10000 AND 20000 
	AND YEAR(e.data_contractacio) < 1999
    AND d.nom IN ("Compres","Vendes");

-- Ex9

SELECT e.nom, e.cognoms, d.nom AS Departament
FROM empleats e
LEFT JOIN departaments d ON d.departament_id = e.departament_id
ORDER BY d.nom, e.cognoms, e.nom;

-- Ex10

SELECT d.departament_id, d.nom, COUNT(e.empleat_id)
FROM empleats e
RIGHT JOIN departaments d ON d.departament_id = e.departament_id
GROUP BY d.departament_id;

-- Ex11

SELECT d.nom AS Departament, COUNT(e.empleat_id)
FROM empleats e
INNER JOIN departaments d ON d.departament_id = e.departament_id
GROUP BY d.departament_id;

-- Ex12

SELECT d.nom AS Departament, COUNT(e.empleat_id)
FROM empleats e
RIGHT JOIN departaments d ON d.departament_id = e.departament_id
GROUP BY d.departament_id;

-- Ex13

SELECT e.nom, e.cognoms, e.empleat_id, f.nom_treball, e.salari, f.salari_min
FROM feines f
INNER JOIN empleats e ON f.feina_codi = e.feina_codi
WHERE (f.nom_treball = "Programador" OR f.nom_treball = "Venedor")
		AND e.salari > f.salari_min;

-- Ex14

SELECT e.nom, e.cognoms, e.empleat_id, f.nom_treball, e.salari, f.salari_min
FROM feines f
INNER JOIN empleats e ON f.feina_codi = e.feina_codi
WHERE (f.nom_treball = "Programador" OR f.nom_treball = "Venedor") AND e.salari > f.salari_min+1000;

-- Ex15

SELECT e.nom, e.cognoms, h.data_inici, h.data_fi, f.nom_treball, d.nom AS departament
FROM historial_feines h
INNER JOIN empleats e ON e.empleat_id = h.empleat_id
INNER JOIN feines f ON h.feina_codi = f.feina_codi
INNER JOIN departaments d ON d.departament_id = h.departament_id;

-- Ex16

SELECT e.empleat_id, e.nom,e.cognoms,e.salari, f.nom_treball, d.nom AS departament, p.nom AS pais, r.nom AS regio
FROM empleats e
INNER JOIN feines f ON f.feina_codi = e.feina_codi
INNER JOIN departaments d ON d.departament_id = e.departament_id
INNER JOIN localitzacions l ON l.localitzacio_id = d.localitzacio_id
INNER JOIN paisos p ON p.pais_id = l.pais_id
LEFT JOIN regions r ON r.regio_id = p.regio_id; 

-- Ex17 AND 18

SELECT e.empleat_id, e.nom,e.cognoms,e.salari, f.nom_treball, d.nom AS departament, p.nom AS pais, r.nom AS regio
FROM empleats e
LEFT JOIN feines f ON f.feina_codi = e.feina_codi
LEFT JOIN departaments d ON d.departament_id = e.departament_id
INNER JOIN localitzacions l ON l.localitzacio_id = d.localitzacio_id
INNER JOIN paisos p ON p.pais_id = l.pais_id
INNER JOIN regions r ON r.regio_id = p.regio_id; 

-- Ex19

SELECT e1.empleat_id, e1.nom, e1.cognoms, e1.id_cap, e2.nom AS nomCap, e2.cognoms AS cognomsCap
FROM empleats e
INNER JOIN empleats jefes ON e.id_cap = jefe.empleat_id;

-- Ex20

SELECT e1.empleat_id, e1.nom, e1.cognoms, e1.data_contractacio, e1.id_cap, e2.nom AS nomCap, e2.cognoms AS cognomsCap, e2.data_contractacio
FROM empleats e1
INNER JOIN empleats e2 ON e1.id_cap = e2.empleat_id
WHERE e1.data_contractacio < e2.data_contractacio
```
