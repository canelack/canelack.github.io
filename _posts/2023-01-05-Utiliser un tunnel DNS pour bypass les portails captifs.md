---
title: Utiliser un tunnel DNS pour bypass les portails captifs
updated: 2023-03-15 22:24:38Z
created: 2023-03-14 21:06:06Z
categories: [HACKSPERIENCE]
tags: [dns, redteam]
img_path: /assets/img/2023-01-05-Utiliser un tunnel DNS pour bypass les portails captifs
---

Test d'une technique pour bypass les portails captifs des hôtels, résidences étudiantes (WiF***k), tel que :

![ee96467cc5873896214a74beb9f8992e.png](ee96467cc5873896214a74beb9f8992e.png)

Mais **également** un très bon moyen d'avoir un ***Command & Control* super discret** et possiblement capable de bypass un firewall !

### Prérequis

- un nom de domaine (à partir de 0.99$ chez quelques registrar)
- un serveur avec une IP publique (Azure c'est bien quand on est étudiant = > 90$ de crédit gratuit)
- L'outil : *[iodine](https://github.com/yarrick/iodine)*

## C'est parti

Domaine **conolo.buzz** acheté chez porkbun.com.

Une VM Azure à 0.01$ de l'heure, qu'on accède par SSH :

`PS C:\Users\Fabien\Documents\Cours\Projets\Azure> ssh -i .\name-srv_key.pem fabien@51.120.122.44`

Zone DNS dans `porkbun.com`

![479f65d2527a6dc188410c4bce160042.png](479f65d2527a6dc188410c4bce160042.png)

On suit le tuto (**spoiler** : ça marche MAIS gros soucis quand même)

Connexion au serveur iodine : OK/KO on sait pas trop

![e2995323deb39d6ac68fcfcf079841b3.png](e2995323deb39d6ac68fcfcf079841b3.png)

![c2f699c779cae30bb8ace030b54effe0.png](c2f699c779cae30bb8ace030b54effe0.png)

Création d'un tunnel SSH sur le port 5000 :

![fc72c7e6ad5cdf342119917d9597e8a4.png](fc72c7e6ad5cdf342119917d9597e8a4.png)

Récupération de données sur internet :

![c1abf7d8f8ab262073701a72125b6791.png](c1abf7d8f8ab262073701a72125b6791.png)

Mais un débit **merdique !**

Par la suite j'ai testé avec ma connexion 4G, les débits étaient équivalents donc ce n'est probablement pas un bridage du point d'accès mais un problème de performance structurel, c'est expliqué dans [la doc de Iodine](https://github.com/yarrick/iodine#performance). On peut pas s'attendre dans cette configuration à plus de 600 kbit/s.

## Conclusion

Pas terrible comme méthode, vaut mieux tenter un brute force sur les comptes identifiés comme valides.

## Références

[https://calebmadrigal.com/dns-tunneling-with-iodine/ ](https://calebmadrigal.com/dns-tunneling-with-iodine/)(le bon tuto)

[https://github.com/yarrick/iodine](https://github.com/yarrick/iodine)

[https://github.com/iagox86/dnscat2/blob/master/doc/authoritative\_dns\_setup.md](https://github.com/iagox86/dnscat2/blob/master/doc/authoritative_dns_setup.md)

[https://www.varonis.com/fr/blog/quest-ce-que-le-dns-tunneling-guide-de-detection](https://www.varonis.com/fr/blog/quest-ce-que-le-dns-tunneling-guide-de-detection)

[https://github.com/iagox86/dnscat2](https://github.com/iagox86/dnscat2) (C2 nous voilà)