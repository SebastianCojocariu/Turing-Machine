Sebastian Cojocariu 321CB UPB ACS                    

                                            Multi-track Turing machine 


-functia verifica:functie care verifica daca am ajuns cu stare_curenta intr-o stare finala(1),altfel(0)
-stari_conditii : matrice in care stocam tranzitiile(stari_conditii[2*k]->stari_conditii[2*k+1],pt k=0,(*nr_tranzitii)-1)
-stari_finale : matrice in care stocam starile finale ale MT
-caractere_citite: matrice pt caracterele citite pe cele 2 benzi cu corespondenta (caracter_citit[2*k] pt banda1,caracter_citit[2*k+1] pt banda2,pt k=0,(*nr_tranzitii)-1))
-caracter_schimbat:matrice pt caracterele schimbate pe cele 2 benzi cu corespondenta (caracter_schimbat[2*k] pt banda1,caracter_schimbat[2*k+1] pt banda2,pt k=0,(*nr_tranzitii)-1)
-destinatie:matrice care stocheaza cum se misca MT pe banda(adica L,H,R) cu corespondenta destinatie[2*k] pt banda1,respectiv destinatie[2*k+1] pt banda 2,pt k=0,(*nr_tranzitii)-1))
Algoritm:
Citim  informatiile din fisier si le stocam in locurile corespunzatoare(tranzitiile in stari_tranzitii,caractere citite in caractere_citie,etc).
Folosim o stare_curenta care initial va fi starea initiala citita din fisier
Intram intr-un while care se va executa atata timp cat nu suntem in stare finala(cu stare_curenta) si putem executa o tranzitie din stare curenta(adica daca se potriveste stare_curenta,caracter citit pe prima banda si caracter citit pe a 2a banda cu informatiile corespunzatoare de pe una din liniile de tranzitii din fisier)
Folosim un ok=1 initial pt a intra in while,cu mentiunea ca ok va fi 1 in interiorul while-ului cand se poate face o tranzitie din starea curenta,respectiv 0 invers(moment in care se va iesi din while si se va afisa mesajul de eroare corespunzator).
Daca ok==1 afisam cele 2 benzi,altfel afisam mesajul de eroare


                                         Turing machine to determine the dominant character
                                         
Pas i)Ideea centrala este de a gasi 2 elemente diferite pe care le stergem(le schimbam valoarea in 0) si ne intoarcem din nou la inceput,urmand ca in urma acestui algoritm sa ramanem pe banda doar cu 0 si caracterul dominant(stim ca exista,altfel algoritmul nu ar fi corecta,cu exemplul ababc->00abc->0000c adica c ar fi dominant,fals)(in orice ordine posibila:de exemplu 000aaa... sau 0a00a0aaa...,etc).

Pas ii)Din acest punct ne pozitionam imediat la stanga #-ului cel mai din dreapta al benzii si facem urmatorii pasi:cat timp citim 0 transformam 0-ul in # si mergem la stanga;cand dam de un caracter(a,b,c,d) il lasam intact(citim a si scriem a,de ex) si mergem un pas mai la stanga;de-acum,orice citim diferit de # tranformam in # si mergem la stanga.Cand citim # ne oprim.

Pas 1)Initial suntem in starea init.Cat timp citim 0 scriem 0 ,ramanem in init si facem R.Daca citim a,b,c,d scriem a,b,c sau d(scriem ce citim) mergem in starile qa,qb,qc,respectiv qd si facem R.Din starea qa,cat timp citim a sau 0 scriem a sau 0 ,ramanem in qa si facem R(analog pt celelalte qb,qc,qd);altfel(citim b,c sau d in cazul in care ne aflam in qa,similar in celelalte cazuri) scriem 0 ,facem H si intram in starea sterge.Din starea sterge,cat timp citim 0 scriem 0 facem L si ramanem in starea sterge.Daca citim un caracter {a,b,c,d} scriem 0 facem H si intram in starea final.Din starea asta orice citim diferit de # scriem pe banda ,ramanem in starea curenta si mergem L.Daca citim # scriem # facem R si intram in starea init.

Pas 2)Dupa ce am sters toate elementele diferite 2 cate 2 cu algoritmul de mai sus,din moment ce stim ca exista sigur un element majoritar,se va intra in init si se va citi(eventual dupa 0-urile de la inceput,) un caracter din {a,b,c,d}.Sa zicem ca citim a,deci intram in qa.Acum,din moment ce pe banda exista doar 0 si caracter dominant(deci a in cazul nostru) stim sigur ca din sa se va ajunge la sfarsit de banda(deci se va citi #);asadar din qa,daca citim # ,scriem #,facem L si intram in starea x(similiar daca citim # in cazurile qb,qc,qd scriem # facem L si intram in starea x).Suntem la sfarsit de banda(imediat la stanga #-ului de final).Cat timp citim 0 ,scriem # ,facem L si ramanem in x.Daca citim un caracter {a,b,c,d} il scriem inapoi,facem L si intram intr-o stare q.Din aceasta stare,cat timp citim caractere diferite de # scriem # facem L si ramanem in q.Daca citim # inseamna ca am ajuns la sfarsit-ul benzii,deci scriem #,intram in starea F(de final) si facem H.
