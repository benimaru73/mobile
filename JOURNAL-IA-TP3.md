# JOURNAL-IA — Mini-TP 3

- **Bonne ligne :** oui, l’IA désigne bien `MainActivity.kt:29`, dans notre paquet `mg.itu.cycledevie`, pour le crash de la variante présentée dans l’énoncé.
- **Bonne cause :** oui, le code cherche `btnPartage`, qui n’est pas dans le layout chargé. `findViewById` renvoie donc `null`, ce qui provoque la `NullPointerException`.
- **Bonne correction :** oui, il faut remplacer `btnPartage` par `btnPartager`, car le bouton de `activity_main.xml` porte l’identifiant `@+id/btnPartager`. Il manquait simplement le « r » final.
