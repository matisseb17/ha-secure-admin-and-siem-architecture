# Alignement Gouvernance & Conformité (ISO 27001 / HDS / RGPD)

Ce document relie les choix techniques de l'architecture aux exigences organisationnelles d'un SMSI en démarche d'amélioration continue (PDCA).

## Principes Clés

* **Maîtrise des accès et des privilèges :** centralisation via le bastion, principe du moindre privilège, revues périodiques des droits et désactivation des comptes inactifs.
* **Journalisation et détection d'incidents :** centralisation des journaux dans Graylog, règles d'alerte sur comportements suspects, qualification et procédures d'escalade/réponse.
* **Protection des données :** chiffrement en transit (TLS) et au repos (chiffrement des disques/sauvegardes, gestion rigoureuse des clés), aligné avec les enjeux RGPD et d'hébergement sensible.
* **Continuité et reprise d'activité (PCA/PRA) :** redondance des composants critiques, sauvegardes 3-2-1 avec contrôles d'intégrité et tests périodiques de restauration.
* **Preuves et amélioration continue :** maintien à jour de la documentation d'architecture, des procédures d'exploitation, des registres de risques/changements et des plans d'actions issus des audits.
