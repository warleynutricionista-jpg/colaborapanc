# Territorial prioritization

## Current implementation
Service: `mapping/services/priorizacao_territorial.py`.

Main function: `calcular_score_prioridade(point, climate_snapshot=None, density_validacoes=0)`.

## Formula implemented
`final_score = 0.30*incidence + 0.25*climate + 0.25*reliability + 0.20*recency`

Components:
- **incidence**: local density of validations (simple proxy).
- **climate**: climate risk received in the snapshot (default 0.3).
- **reliability**: favors points already approved/validated.
- **recency**: recent observations are given greater weight.

## Output
Object with:
- `score` (0 to 1),
- `components` (details for audit),
- textual `explanation`.

## Limitations
- Heuristics not yet calibrated with extensive historical series.
- Dependence on external climate snapshot when available.
- Current usage in sample dashboard (not full batch pipeline).