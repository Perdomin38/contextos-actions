# contextos-actions

Workflow de ejemplo sobre los contextos de GitHub Actions (práctica 10 de TSCD).

- `.github/workflows/contextos.yml`: usa los contextos `github`, `env`, `vars`, `job`, `steps`, `runner`, `secrets`, `strategy`, `matrix`, `needs` e `inputs`.
- `.github/workflows/reutilizable.yml`: workflow reutilizable que publica su salida con el contexto `jobs`.

## Lanzamiento manual

```bash
gh workflow run contextos.yml -f entorno=produccion -f nivel=detallado -f matriz=false -f mensaje='texto libre'
```

## Configuración necesaria

| Tipo | Nombre | Dónde |
|---|---|---|
| Variable | `EQUIPO` | Repositorio |
| Variable | `API_ENDPOINT` | Entornos `desarrollo` y `produccion` |
| Secreto | `DEPLOY_TOKEN` | Entornos `desarrollo` y `produccion` |

## Qué no se imprime en los logs

- **Secretos** (`secrets.*`) y el token del workflow (`github.token`): solo se comprueba si existen.
- **Datos personales**: `github.actor`, `github.triggering_actor`, `github.actor_id` y los correos y nombres del payload del evento.
- **El payload completo** (`github.event` o `toJSON(github)`): mezcla todo lo anterior.
- **Texto libre** (inputs de tipo string, mensajes de commit, títulos de PR): se imprime solo como dato, pasado por `env`, y nunca se interpola en un script con `${{ }}`.
