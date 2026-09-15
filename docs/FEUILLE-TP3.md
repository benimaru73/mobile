# MINI-TP 3 — Anatomie Android

## 1. Modèle de prédictions

Je n’ai pas noté de prédictions avant de lancer l’application, ni pour le scénario A (rotation), ni pour le scénario B (accueil puis retour). Je ne peux donc pas comparer les observations à une prédiction initiale. Les explications ci-dessous ont été rédigées après l’exécution, avec l’aide de l’IA pour analyser les captures et mettre en forme la feuille.

### Scénario A — Rotation : compréhension après l’exécution

Séquence attendue dans ce projet, à partir d’une activité au premier plan : onPause → onStop → onDestroy pour l’ancienne instance, puis onCreate → onStart → onResume pour la nouvelle.

Réponse « + » : un compteur conservé uniquement dans un champ de l’Activity est réinitialisé à la recréation, sauf si sa valeur est sauvegardée et restaurée.

### Scénario B — Accueil puis retour : compréhension après l’exécution

Séquence attendue si le processus reste vivant : onPause → onStop, puis onRestart → onStart → onResume au retour.

Réponse « + » : contrairement à la rotation, l’Activity est ici arrêtée puis reprise sans être recréée ; ses champs restent en mémoire tant que son instance est conservée.

## 2. Tableau d’observation

| Scénario | Séquence visible dans les captures | Écart avec ma prédiction et explication |
| --- | --- | --- |
| A — Rotation | Aucune séquence complète de rotation identifiable dans les deux captures. La fin de tp3_1 montre onPause → onStop → onDestroy, mais pas de recréation ensuite. Cela ne suffit pas à confirmer une rotation. | Comparaison impossible : aucune prédiction initiale et capture de rotation manquante. |
| B — Accueil puis retour | Dans tp3_2 : onPause (17:42:20.193) → onStop (17:42:24.036) → onRestart (17:42:30.857) → onStart (17:42:30.857) → onResume (17:42:30.858). Cette séquence correspond à un arrêt puis une reprise de l’activité, compatible avec le scénario B. | Aucune prédiction initiale. Dans cet intervalle, il n’y a ni onDestroy ni onCreate : l’activité reprend sans recréation visible. |

## 3. Question d’observation

Question de l’énoncé : à la rotation, le numéro d’instance affiché par onCreate change ; qu’est-ce que cela prouve et qu’arriverait-il à un compteur stocké dans l’Activity ?

Réponse : le changement de numéro indique qu’une nouvelle instance de l’Activity a été créée ; un compteur stocké uniquement dans l’ancienne instance retrouverait sa valeur initiale, sans sauvegarde et restauration de son état.

Cette réponse explique le comportement attendu ; les captures fournies ne montrent pas deux numéros d’instance avant et après une rotation.

## 4. Bonus — Ouverture du second écran

Dans tp3_2, MainActivity (CYCLE) passe en onPause à 17:41:59.273, avant le onCreate de SecondActivity (CYCLE-2) à 17:41:59.299. Le second écran passe ensuite en onStart puis onResume à 17:41:59.306. MainActivity passe enfin en onStop à 17:41:59.858.

La première activité se met donc en pause avant la création de la seconde. Elle ne passe en onStop qu’après le onResume de la seconde dans cette observation.

## 5. Partage

Le code du projet utilise ACTION_SEND, le type text/plain, le texte « Collecte du jour : 4,5 kg de vanille » et Intent.createChooser. Les captures Logcat seules ne prouvent pas que le sélecteur affiche ce texte : la validation visuelle reste à confirmer.

## 6. JOURNAL-IA — Verdict sur la variante de l’énoncé

- Bonne ligne : oui, MainActivity.kt:29 appartient bien à notre paquet mg.itu.cycledevie dans la stack trace fournie.
- Bonne cause : oui, findViewById cherche btnPartage, absent du layout chargé, et renvoie null, d’où la NullPointerException.
- Bonne correction : oui, il faut utiliser btnPartager, qui correspond à l’identifiant @+id/btnPartager déclaré dans activity_main.xml.
