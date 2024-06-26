# Plateforme de gestion medicale

## Microservice 1 : ms_profile

## Microservice 2 : ms_recherche

## Microservice 3 : ms_rendez_vous

### creation du calendrier

#### create a day creud

http://localhost:8083/calendrier/medecin/2/createCreudsWithPause, method = post, 2 sends for id_medecin

```json
{
  "dayStart": "2024-05-23T08:00:00",
  "workingSessionLong": 15,
  "workingHours": 8,
  "pauseStart": "2024-05-23T12:00:00",
  "pauseEnd": "2024-05-23T13:00:00"
}
```

#### create day creud without pause

http://localhost:8083/calendrier/medecin/2/createCreudsWithoutPause, method = post, 2 sends for id_medecin

```json
{
  "dayStart": "2024-05-24T08:00:00",
  "workingSessionLong": 15,
  "workingHours": 8,
}
```

#### create month creud with pause

http://localhost:8083/calendrier/medecin/1/createMonthCreudsWithPause, method = post, 2 sends for id_medecin

```json
{
    "dayStart": "09:00:00",
    "workingSessionLong": 30,
    "workingHours": 8,
    "pauseStart": "12:00:00",
    "pauseEnd": "13:00:00",
    "days": [1, 2, 3, 4, 5],
    "month": 6,
    "year": 2024
}
```

#### create month creud without pause

http://localhost:8083/calendrier/medecin/1/createMonthCreudsWithoutPause, method = post, 2 sends for id_medecin

```json
{
    "dayStart": "09:00:00",
    "workingSessionLong": 30,
    "workingHours": 8,
    "days": [11, 12, 13, 14, 15],
    "month": 6,
    "year": 2024
}
```

#### update month creud without pause : the new one will be created without a pause, the old one can be both (with or without pause)

http://localhost:8083/calendrier/medecin/1/updateMonthCreudsWithoutPause , method = put , 1 = id_medecin

```json
{
    "dayStart": "08:00:00",
    "workingSessionLong": 25,
    "workingHours": 8,
    "days": [1, 2, 3, 4, 5],
    "month": 6,
    "year": 2024
}
```

#### update month creud with pause : the new one will be created with a pause, the old one can be both (with or without pause)

http://localhost:8083/calendrier/medecin/1/updateMonthCreudsWithPause , method = put , 1 = id_medecin

```json
{
    "dayStart": "08:00:00",
    "workingSessionLong": 25,
    "pauseStart" : "12:00:00",
    "pauseEnd" : "13:00:00",
    "workingHours": 8,
    "days": [1, 2, 3, 4, 5],
    "month": 6,
    "year": 2024
}
```

#### delete day creud (both options: with and without pause)

http://localhost:8083/calendrier/medecin/1/delete, method : delete , 1 = id_medecin

```json
{
    "days": [1, 2, 3, 4, 5],
    "month": 6,
    "year": 2024
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

```json
{
    "oldStartTime": "2024-05-23T08:00:00",
    "newStartTime": "2024-05-23T08:30:00",
    "demandeType" : "EMERGENCY"
}
```

### get all patient rendez_vous(past && future)

http://localhost:8083/rendezvous/patient/1  , method = get

### get all medecin rendez_vous(past && future)

http://localhost:8083/rendezvous/medecin/2  , method = get

### get all patient past rendez vous

http://localhost:8083/rendezvous/patient/past/1 , method = get

### get all medecin past rendez vous

http://localhost:8083/rendezvous/medecin/past/2 , method = get

### get all patient today rendez vous

http://localhost:8083/rendezvous/patient/today/1 , method = get

### get all medecin today rendez vous

http://localhost:8083/rendezvous/medecin/today/2 , method = get

### get all patient future rendez vous

http://localhost:8083/rendezvous/patient/future/1 , method = get

### get all medecin future rendez vous

http://localhost:8083/rendezvous/medecin/future/2 , method = get

## Microservice 4 : ms_dossier_medicale

j'assume ici que si le dossier medicale n'est pas créer il serait créer de facon automatique.

we should insert some medicaments first using mysql teminal

```sql
INSERT INTO medicament (description, dosage, generique, nom) VALUES
('Pain reliever', 500.0, 'Acetaminophen', 'Tylenol'),
('Antihistamine', 10.0, 'Loratadine', 'Claritin'),
('Antacid', 250.0, 'Calcium carbonate', 'Tums'),
('Muscle relaxant', 50.0, 'Cyclobenzaprine', 'Flexeril'),
('Antibiotic', 200.0, 'Amoxicillin', 'Amoxil'),
('Anti-inflammatory', 100.0, 'Ibuprofen', 'Advil'),
('Antidepressant', 20.0, 'Sertraline', 'Zoloft'),
('Antifungal', 150.0, 'Fluconazole', 'Diflucan'),
('Antiemetic', 5.0, 'Ondansetron', 'Zofran'),
('Bronchodilator', 50.0, 'Albuterol', 'Ventolin');
```

### Ajout de d'une orodnnance

http://localhost:8084/create/medecin/2/patient/1/create_ordonnace , method = post , 2 = id_medecin , 1 = id_patient

```json
{
  "description": "List of Medicaments",
  "medicaments": [
    {
      "description": "Pain reliever",
      "nom": "Tylenol"
    },
    {
      "description": "Antihistamine",
      "nom": "Claritin"
    },
    {
       "nom": "Tums",
      "description": "Antacid"
    }
  ]
}
```

### Ajout d'une radio

http://localhost:8084/create/medecin/2/patient/1/add_radio , method = post , 1 = id_patient , 2 = id_medecin

```json
{
  "description": "Description of the image",
  "image": [10, 20, 30, 40, 50]
}

```

### Ajout d'analyse

http://localhost:8084/create/medecin/2/patient/1/add_analyse, method = post, 2 = id_medecin , 1 = id_patient

```json
{
  "description": "Description of the test results",
  "testResultList": [
    {
      "id": 1,
      "testName": "Test 1",
      "personResult": 10.5,
      "startNormalRange": 5.0,
      "endNormalRange": 15.0
    },
    {
      "id": 2,
      "testName": "Test 2",
      "personResult": 7.8,
      "startNormalRange": 6.0,
      "endNormalRange": 10.0
    },
    {
      "id": 3,
      "testName": "Test 3",
      "personResult": 20.0,
      "startNormalRange": 12.0,
      "endNormalRange": 25.0
    }
  ]
}
```

### Gets

#### Get ordonnace by id

http://localhost:8084/get/ordonnace/1 , method = get , 1 = id_ordonnace

#### Get ordonnances by id patient

http://localhost:8084/get/ordonnace/me/1 , method = get , 1 = id_patient

#### Get ordonnaces by id medecin

http://localhost:8084/get/ordonnace/medecin/1 , method = get , 1= id_medecin

#### Get radio by id

http://localhost:8084/get/radio/1 , method = get , 1= id_radio

#### Get radios by id patient

http://localhost:8084/get/radio/me/1 , method = get , 1 = id_patient

#### Get radios by id medecin

http://localhost:8084/get/radio/medecin/1 , method = get , 1= id_medecin

#### Get analyse by id

http://localhost:8084/get/analyse/1 , method = get , 1 = id_analyse

#### Get analyses by id patient

http://localhost:8084/get/analyse/me/1 , method = get , 1 = id_patient

#### Get analyses by id medecin

http://localhost:8084/get/analyse/medecin/1 , method = get , 1 = id_medecin

#### Get dossier medical by id

http://localhost:8084/get/dossier/1 , method = get , 1 = id_dossier

#### Get dossier medical by id patient

http://localhost:8084/get/dossier/me/1 , method = get , 1 = id_dossier

#### Get dossier medical by id medecin

http://localhost:8084/get/dossier/medecin/1 , method = get , 1 = id_dossier

## microservice 5 : ms_notifications

### Get notification (the frontent should send a request every minute , and every two hours a cron job is executed to get the new rendez vous for the next 2 hours)

http://localhost:8085/api/medecin/1/rendezvous , method = get , 1 = id_medecin