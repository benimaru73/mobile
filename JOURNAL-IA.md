# Journal IA — Mini-TP 2

* Écart choisi : Programme 3 — je pensais que les deux tâches s’exécuteraient en même temps, mais la durée obtenue est d’environ 1866 ms.
* La première tâche est attendue avant même que la deuxième soit lancée à cause du premier `await`.
* Les deux temps s’additionnent donc ; pour les exécuter en parallèle, il faut lancer les deux `async` avant de faire les `await`.
