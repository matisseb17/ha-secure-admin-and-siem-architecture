# Vue d'Ensemble de l'Architecture

Ce document présente le découpage logique de l'architecture cible autour de trois principes : **isolation du plan d'administration**, **centralisation de la journalisation/sécurité** et **résilience opérationnelle**.

## Diagramme d'Architecture (Anonymisé)

```mermaid
flowchart TB
    subgraph ADMIN["Zone Administration (Haute Disponibilité)"]
        BASTION["Bastion d'Administration (PAM / MFA / Enregistrement)"]
        PVE_HA["Cluster Virtualisation HA (ex. Proxmox VE + Stockage Résilient)"]
        BASTION --- PVE_HA
    end

    subgraph OBS["Zone Supervision & SIEM"]
        GRAYLOG["SIEM Graylog (Collecte, Normalisation, Corrélation, Alertes)"]
        MON["Supervision & Inventaire (Métriques, État des Services)"]
    end

    subgraph PROD["Zones Hébergement & Production (Durcies)"]
        SEG_A["Segment Critique / Conformité Renforcée"]
        SEG_B["Segment Services & Applications"]
        BACKUP["Sauvegardes 3-2-1 (Chiffrées & Hors Ligne / Isolées)"]
    end

    ADM_USER["Administrateurs & Prestataires (MFA)"] -->|"SSH / RDP contrôlé & tracé"| BASTION
    BASTION -->|"Accès d'administration restreint (IP source Bastion)"| SEG_A
    BASTION -->|"Accès d'administration restreint (IP source Bastion)"| SEG_B
    BASTION -->|"Logs sessions / accès"| GRAYLOG

    SEG_A -->|"Logs système, sécu & applicatifs"| GRAYLOG
    SEG_B -->|"Logs système, sécu & applicatifs"| GRAYLOG
    MON -->|"Alertes / états"| GRAYLOG

    SEG_A -->|"Sauvegardes chiffrées"| BACKUP
    SEG_B -->|"Sauvegardes chiffrées"| BACKUP
