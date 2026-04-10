# ColaboraPANC (English)

Collaborative platform for geo-referenced PANC mapping with AI-assisted identification, human validation, and territorial analysis.

## Documentation

- **Main English guide:** [`docs/en/README.md`](docs/en/README.md)
- **Portuguese documentation version:** [`docs/pt/README.md`](docs/pt/README.md)
- **Documentation hub:** [`docs/README.md`](docs/README.md)

## Bilingual convention (PT/EN)
PT and EN docs are organized in separate directories and paired by filename:

- `docs/pt/<file>.md` ↔ `docs/en/<file>.md`

Examples:
- `docs/pt/arquitetura_geral.md` ↔ `docs/en/arquitetura_geral.md`
- `docs/pt/api_endpoints.md` ↔ `docs/en/api_endpoints.md`
- `docs/pt/governanca_ia.md` ↔ `docs/en/governanca_ia.md`

## Quick project view

### Stack
- Backend: Django + Django REST Framework + GeoDjango
- Database: PostgreSQL + PostGIS
- Mobile: React Native (Expo)
- Integrations: PlantNet, Plant.id, Open-Meteo, INMET, MapBiomas

### Core capabilities
- Geo-referenced PANC point registration
- AI-assisted identification with human-in-the-loop review
- APIs for notifications, communication, routing, and environmental modules
- Mobile flows for map, registration, review, and offline mode

## Quick setup

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements_core.txt
python manage.py migrate
python manage.py runserver 0.0.0.0:8000
```

Mobile:

```bash
cd mobile
npm install
npm start
```

## Tests

```bash
pytest
```

## Project meta
- [Contributing](CONTRIBUTING.md)
- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Security](SECURITY.md)
- [Changelog](CHANGELOG.md)
- [License](LICENSE)
