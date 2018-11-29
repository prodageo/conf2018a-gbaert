# D'une architecture Web MVC à une architecture Clean Hexagonale

## Cartouche d'identification

 - Manifestation : CodeursEnSeine 2018
 - Lieu : Kindarena Rouen
 - Conférence : D'une architecture Web MVC à une architecture Clean Hexagonale
 - Horaire de la conférence : 11h00
 - Durée de la conférence : 1h
 - Conférencière :
   - Céline Gilet : https://twitter.com/celinegilet, https://www.github.com/celinegilet
 - Audience : environ 100 personnes
 - Auteur du billet : Gaétan BAERT
 - Mots-clés : Architecture Clean, Architecture Hexagonale, Ports et Adapteurs, Data Providers
 - URL de l'illustration : ![https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture](CleanArchitecture.jpg)
   - Quelques sources : https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture
## Support
 - Lien vers le support (diapos) présenté en conférence : https://speakerdeck.com/celinegilet/dune-architecture-web-mvc-a-une-architecture-clean-hexagonale-4cef6e93-0e4a-46ba-a235-3499bde6c773
 - Nombre de diapos du support : 43
 - Plan du support : 
   - 01 - Prise en main du sujet
   - 02 - Maintenabilité et évolutivité du code
   - 03 - Vers une architecture Clean Hexagonale
   - 04 - Clean Architecture - Step by step
   - 05 - Hexagonale Architecture

## Résumé
La présentation a consisté en la transformation d'une application simple (https://github.com/celinegilet/happy-town/tree/start) construite selon une architecture MVC standard en cette même application, mais avec une architecture Clean Hexagonale. 

Tout d'abord, a été montré les pricipales limitations de l'architecture MVC : Au niveau des tests, il est nécessaire de connfigurer un serveur mail, ce qui rend les tests difficiles à réaliser. EN effet, la majorité des tests se trouvent au niveau des tests d'intégration, ce qui donne une mauvaise répartition des tests (l'idéal étant d'avoir une base de tests unitaires). De plus, le code métier se retrouve couplé avec des frameworks, ce qui peut poser des problèmes lors de la mise à jour de ces frameworks. 

La solution présentée pour dépasser ces limitations est l'utilisation soit d'une architecture Clean, soit d'une architecture Hexagonale. Est alors présenté le passage de l'architecture MVC à l'architecture Clean (https://github.com/celinegilet/happy-town/tree/cleanArchi). Le principe est : 
  - de nettoyer la partie modèle pour la transformer en partie entité, en supprimant les annotations et les frameworks ;  
  - regrouper les méthodes du code métier disséminé dans la partie services dans des classes dans un package usecases ; 
  - réaliser des interfaces d'accès aux données (data providers) , une interface par type de donnée différent, et dont l'implémentation dépendra de la manière dont sont stockées les données. Le code métier ne fera qu'appeler les méthodes décrites dans les interfaces sans se préoccuper des techniques de stockage ;
  - Séparer le modèle : modèle métier, modèle d'accès aux données, modèle de présentation des données. Ajouter différents entrypoints qui peuvent appeler le code métier, ceci par type de données différent.
  
L'intérêt est de permettre, par exemple, de réaliser des tests unitaire sur le code métier en mockant facilement les données et ainsi se passer d'un serveur mail. Aussi, si le choix du stockage de données vient à changer durant la vie du projet, il suffira de changer l'implémentation du data provider associé. 

Enfin, les différences entre une architecture Clean et une architecture hexagonale se résume principalement à un changement de vocabulaire.  


## Architecture et facteur qualité
Maintenabilité : testabilité. En effet, il devient bien plus facile de tester unitairement le code métier quand celui-ci est exempt de tout couplage avec les différentes technologies de stockage de données. Ceci permet donc d'avoir une bonne base de tests unitaires avant de se lancer dans des tests d'intégration ou des tests fonctionnels.
