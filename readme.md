# Warehouse Maintenance API (Flask + SQLite)

A small teaching API for warehouse maintenance logs with a hardcoded API key that students embed in their client apps.

## Quick start

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python init_db.py
python app.py
```

The API runs at `http://localhost:5000` and uses `warehouse.db` in the project root.

## API key

Use the same hardcoded key in your client apps:

```
api_warehouse_student_key_1234567890abcdef
```

Send it as either:

- `X-API-Key: api_warehouse_student_key_1234567890abcdef`
- `Authorization: Bearer api_warehouse_student_key_1234567890abcdef`

All `/logs` endpoints require the API key. `/users` endpoints are open for teaching purposes.

## Example requests

Create a user:

```bash
curl -X POST http://localhost:5000/users \
  -H "Content-Type: application/json" \
  -d '{"username":"alex","password":"secret","role":"manager"}'
```

Log in:

```bash
curl -X POST http://localhost:5000/users/login \
  -H "Content-Type: application/json" \
  -d '{"username":"alex","password":"secret"}'
```

Create a maintenance log (API key required):

```bash
curl -X POST http://localhost:5000/logs \
  -H "Content-Type: application/json" \
  -H "X-API-Key: api_warehouse_student_key_1234567890abcdef" \
  -d '{"title":"Replace filter","description":"HVAC filter replacement","priority":"high","status":"open","user_id":1}'
```
