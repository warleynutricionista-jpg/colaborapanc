# ColaboraPANC

Plataforma colaborativa para mapeamento georreferenciado de PANCs com identificação assistida por IA, validação humana e análise territorial.

Collaborative platform for geo-referenced PANC mapping with AI-assisted identification, human validation, and territorial analysis.

## Documentação / Documentation

- 🇧🇷 **Português (guia principal):** [`docs/pt/README.md`](docs/pt/README.md)
- 🇺🇸 **English (main guide):** [`docs/en/README.md`](docs/en/README.md)
- 🌐 **Hub bilíngue:** [`docs/README.md`](docs/README.md)

### Associação entre versões PT/EN
As versões PT e EN estão separadas em diretórios próprios e associadas por **mesmo nome de arquivo**:

- `docs/pt/<arquivo>.md` ↔ `docs/en/<arquivo>.md`

Exemplos:
- `docs/pt/arquitetura_geral.md` ↔ `docs/en/arquitetura_geral.md`
- `docs/pt/api_endpoints.md` ↔ `docs/en/api_endpoints.md`
- `docs/pt/governanca_ia.md` ↔ `docs/en/governanca_ia.md`

## Visão rápida do projeto / Quick project view

### Stack
- Backend: Django + Django REST Framework + GeoDjango
- Banco de dados / Database: PostgreSQL + PostGIS
- Mobile: React Native (Expo)
- Integrações / Integrations: PlantNet, Plant.id, Open-Meteo, INMET, MapBiomas

### Funcionalidades centrais / Core capabilities
- Cadastro georreferenciado de pontos PANC
- Inferência de identificação por IA com revisão humana (human-in-the-loop)
- APIs de notificações, comunicação, rotas e módulos ambientais
- Fluxos mobile para mapa, cadastro, revisão e modo offline

## Setup rápido / Quick setup

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

## Testes / Tests

```bash
pytest
```

## Arquivos institucionais / Project meta
- [Contributing](CONTRIBUTING.md)
- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Security](SECURITY.md)
- [Changelog](CHANGELOG.md)
- [License](LICENSE)
