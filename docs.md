# Plateforme de gestion medicale

## Microservice 1 : ms_profile

## Microservice 2 : ms_recherche

## Microservice 3 : ms_rendez_vous

### creation du calendrier

#### create a day creud

// http://localhost:8083/calendrier/medecin/2/createCreuds, method = post, 2 sends for id_medecin

```json
{
  "dayStart": "2024-05-23T08:00:00",
  "workingSessionLong": 15,
  "workingHours": 8,
  "pauseStart": "2024-05-23T12:00:00",
  "pauseEnd": "2024-05-23T13:00:00"
}
```

### demande de rendezvous

### Gets

## Microservice 4 : ms_dossier_medicale

### Ajout de documents