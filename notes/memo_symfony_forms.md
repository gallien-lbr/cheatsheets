# Symfony les évenemtns de formulaires


*    FormEvents::PRE_SET_DATA => Déclenché avant que les valeurs de l'entity soient passées au formulaire (null si c'est en création).
*    FormEvents::POST_SET_DATA => Déclenché juste avant la fin du setData  du formulaire.
*    FormEvents::PRE_SUBMIT => Déclenché avant que les valeurs soumises de l'utilisateur soient passées au formulaire (le composant form).
*    FormEvents::SUBMIT => Déclenché avant que les donnees sont passer à l'entité.
*    FormEvents::POST_SUBMIT => Déclenché  apres avoir remplir l'entité.
