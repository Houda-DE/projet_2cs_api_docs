# Plateforme de gestion medicale

## Microservice 1 : ms_profile

## Microservice 2 : ms_recherche

## Microservice 3 : ms_rendez_vous

### creation du calendrier

#### create a day creud

http://localhost:8083/calendrier/medecin/2/createCreuds, method = post, 2 sends for id_medecin

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

http://localhost:8083/demande_rendezvous/medecin/2/patient/1/demande_rdv, method post, 2 = id_medecin, 1 = id_patient

```json
{
  "startTime": "2024-05-23T08:00:00",
  "demandeType" : "EMERGENCY"
}
```

### Update Rendez Vous Status

http://localhost:8083/rendezvous/medecin/2/rendezvous/1/setstatus, method = put, 1 = id_rendezvous, 2 = id_medecin

```json
{
    "status" : "RATE"
}
```

### Update Rendez vous start time and type

http://localhost:8083/rendezvous/medecin/2/rendezvous/1/update , 1 = id_patient , 2 = id_medecin , method = put

{
    "oldStartTime": "2024-05-23T08:00:00",
    "newStartTime": "2024-05-23T08:30:00",
    "demandeType" : "EMERGENCY"
}

### get all patient rendez_vous(past && future)

http://localhost:8083/rendezvous/patient/1  , method = get

### get all medecin rendez_vous(past && future)

http://localhost:8083/rendezvous/medecin/2  , method = get

### get all patient past rendez vous

http://localhost:8083/rendezvous/patient/past/1 , method = get

### get all medecin past rendez vous

http://localhost:8083/rendezvous/medecin/past/2 , method = get

### get all patient future rendez vous

http://localhost:8083/rendezvous/patient/future/1 , method = get

### get all medecin future rendez vous

http://localhost:8083/rendezvous/medecin/future/2 , method = get

## Microservice 4 : ms_dossier_medicale

j'assume ici que si le dossier medicale n'est pas créer il serait créer de facon automatique

### Ajout de d'une orodnnance

### Ajout d'une radio

### Ajout d'analyse