# Matrice de Flux (Modèle Générique)

Les flux ci-dessous illustrent une politique de filtrage orientée moindre privilège et cloisonnement entre zones. Les ports et adresses doivent être adaptés à chaque environnement.

| Flux | Source | Destination | Protocole / Port | Objectif & Sécurité |
| :--- | :--- | :--- | :--- | :--- |
| **Accès Bastion** | Postes Admin / VPN dédiés | Bastion (Zone Admin) | TCP/443 ou SSH dédié | Accès authentifié (MFA) sur un point d'entrée unique et journalisé. |
| **Admin Cibles** | Bastion (IP dédiée) | Serveurs / VMs (Zones Cibles) | SSH (TCP/22) / RDP (TCP/3389) | Interdiction des accès directs ; traçabilité nominative des actions. |
| **Envoi Logs SIEM** | Hôtes Cibles / Bastion / Équipements | Collecteur Graylog | Syslog TLS / Beats / GELF | Centralisation sécurisée et chiffrée des événements pour corrélation. |
| **Supervision** | Serveur Supervision | Agents / Hôtes Cibles | SNMPv3 / Agent chiffré | Contrôle de disponibilité, capacité et santé des services. |
| **Sauvegarde** | Hôtes / Clusters Cibles | Cible de Sauvegarde | Protocole chiffré dédié | Sauvegardes planifiées, chiffrées et isolées (logique 3-2-1). |
