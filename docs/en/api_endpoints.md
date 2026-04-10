# API endpoints (real state)

> Base local URL: `http://localhost:8000`

## Authentication
- `POST /api/token/login/` – legacy login by token.
- Web account routes: `/accounts/*` via django-allauth.

## PANC points and search
- `GET /api/pontos/` (legacy in `views.api_pontos`).
- `POST /api/pontos/` (DRF `PontoPANCViewSet.create`) with support for:
  - `popular_name`, `scientific_name`, `suggested_scientific_name`, `chosen_scientific_name`
  - `edibility_status`
  - `comestible_part_manual` (or `edible_part`)
  - `frutificacao_manual` (or `frutificacao_meses`)
  - `manual_harvest` (or `period_harvest`)
  - `location` (array `[lng, lat]` or GeoJSON-like)
  - `enrich_automatically` (default: `true`)
- `PUT/PATCH /api/pontos/<id>/` preserves compatibility and allows the same manual fields.
- `GET /api/busca-avancada/` – filters by name, city, state, type, plant, status and bounding box.
- `GET /api/plantas/` – list of referential plants with filters.
- `GET /api/autocomplete-name/?term=<text>` – quick popular name suggestions (compatible with legacy simple list return).
- `GET /api/autocomplete-nome/?term=<texto>&detailed=1` – detailed suggestions with:
  - `popular_name`
  - `scientific_name`
  - `source` (`base_local_validada`, `historico_pontos`, `inaturalist`)
  - `trust`
- `GET /api/nome-cientifico/?nome_popular=<nome>` – resolves scientific name with safe fallback and metadata:
  - `scientific_name`
  - `source`
  - `resolved` (boolean)

## AI scientific core
- `POST /api/cientifico/pontos/<id>/inferencia/` (auth).
- `GET /api/cientifico/revisao/fila/` (revisor/admin).
- `GET /api/cientifico/revisao/pontos/<id>/` (revisor/admin).
- `POST /api/cientifico/pontos/<id>/validacao/` (reviewer/admin).
- `GET /api/cientifico/pontos/<id>/historico/` (revisor/admin).
- `GET /api/cientifico/dashboard/` (auth).

### Example: scientific validation
POST `/api/cientifico/pontos/10/validacao/`

```json
{
  "decisao_final": "validado",
  "especie_final": "Pereskia aculeata",
  "motivo_divergencia": "",
  "observacao": "Confirmação visual em campo"
}
```
## Notifications, messages and preferences (DRF router)
- `/api/notifications/`
- `/api/devices-push/`
- `/api/conversas/`
- `/api/messages/`
- `/api/preferences/`

## Routes, recommendations and e-commerce
- `/api/routes/`
- `/api/recomendacoes/`
- `/api/integracoes-ecommerce/`
- `/api/produtos-semente/`
- `/api/stores/`
- `/api/produtos/`

## AR and advanced identification
- `POST /api/identificar-planta/`
- `GET /api/buscar-plantas/`
- `GET /api/modelos-ar-disponiveis/`
- `/api/plantas-customizados/`
- `/api/modelos-ar/`
- `/api/historico-identificacao/`

## Offline of plants
- `GET /api/plantas-offline/disponiveis/`
- `GET /api/plantas-offline/packages/`
- `POST /api/plantas-offline/packages/<id>/download/`
- `POST /api/plantas-offline/baixar/`
- `GET /api/plantas-offline/minhas/`
- `POST /api/plantas-offline/sincronizar/`

## MapBiomas
- `GET /api/mapbiomas/alerts/`
- `GET /api/mapbiomas/alertas/<alert_code>/`
- `GET /api/mapbiomas/territorios/`
- `GET /api/mapbiomas/property/`
- `GET /api/mapbiomas/ponto/`
- `GET /api/mapbiomas/pontos-panc/<id>/`
- `GET /api/mapbiomas/testar/`

## Integration administration (staff/superuser)
- `GET /api/admin/integracoes/health/` – queries consolidated status of integrations.
- `POST /api/admin/integracoes/testar/` – runs test of one integration (`integration_name`) or all of them.

### Example: test all integrations
POST `/api/admin/integracoes/testar/`

```json
{}
```
### Example: test specific integration
POST `/api/admin/integracoes/testar/`

```json
{
  "integration_name": "Open-Meteo"
}
```
### Expected error for invalid `integration_name`
`400 Bad Request`

```json
{
  "detail": "integration_name inválido",
  "integration_name": "nome-inexistente",
  "valid_options": ["GBIF", "Global Names Verifier", "INMET"]
}
```
### Main return fields
- `success`
- `status` / `detailed_status`
- `response_time_ms`
- `error_type`
- `friendly_message`
- `configured` / `operational`
- `last_successful_test`
- `ultima_falha_em`
- `last_type_problem`
- `latency_level`

## Expected codes and errors (general)
- `200/201`: success.
- `400`: invalid payload or business rule.
- `401/403`: insufficient authentication/permission.
- `404`: non-existent resource.
- `503`: AI provider unavailability.

## UX notes and taxonomic review
- The point response maintains `enrichment_status` for internal operation, but the common UX should prioritize practical fields (edible, edible part, fruiting and harvesting).
- Taxonomic ambiguity detected by the pipeline is recorded in `payload_resumido_validacao.ambiguidade_taxonomica` and can activate `validacao_pendente_revisao_humana`.


## Climate endpoints (unified pipeline)

- `GET /api/alertas-ativas/`
  - Optional query params: `point_id`, `limit`
  - Returns only current alerts (start <= now <= end).
- `GET /api/historico_alertas_api/`
  - Optional query params: `ponto`/`ponto_id`, `limit`
  - Returns complete history including `active|expired` status.
- `POST /api/clima/sincronizar/` (admin)
  - Optional body: `ponto_id`, `only_active`
  - Triggers INMET + Open-Meteo collection, normalizes and persists with deduplication.
- `GET /api/clima/status/` (admin)
  - Returns operational status of Climate/Environmental integrations and alert metrics (total/active/expired).