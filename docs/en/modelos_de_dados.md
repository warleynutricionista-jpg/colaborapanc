# Data models

## Domain Core

### `PontoPANC`
- Purpose: georeferenced record of PANC observation.
- Key fields: `plan`, `created_by`, `location`, `photo`, `identification_status`, `valid_status`, `flow_status`.
- Rules: geographic validation for approximate coordinates of Brazil in `clean()`.

### `ReferencePlan`
- Purpose: basic botanical catalogue.
- Fields: popular/scientific name, edible part, biome, origin, source.

### `HistoryIdentification`
- Purpose: to track identification attempts (method, score, success, error, time).

### `PredicationIA`
- Purpose: persist structured prediction (top-k and confidence) linked to the point.

### `Expert Validation`
- Purpose: final human decision by reviewer.
- Fields: `final_decision`, `final_species`, `divergence_reason`, `observation`.

### `HistoryValidation`
- Purpose: audit trail of scientific flow events.

## Other relevant domains
- **Gamification**: `Badge`, `Missao`, `MissaoUsuario`, `PontuacaoUsuario`, `HistoricoGamificacao`, `RankingRevisor`.
- **Communication**: `Notification`, `DevicePush`, `Conversation`, `Message`.
- **Territory and risk**: `AlertaClimatico`.
- **Routes and visits**: `Rota`, `RotaPonto`, `RoteiroPANC`, `RoteiroPANCItem`.
- **Offline**: `PacotePlantasOffline`, `PlantaOfflineUsuario`, `ConfiguracaoOffline`, `CacheOffline`.
- **AR and customization**: `CustomPlant`, `ModeloAR`, `ReferenceAR`.

## Status and traceability
- `flow_status` of the point controls scientific cycle (`draft`, `submitted`, `in_revision`, `validated`, `rejected`, `needs_revision`).
- `status_validacao` maintains operational layer (`pending`, `approved`, `failed`, `pending`).