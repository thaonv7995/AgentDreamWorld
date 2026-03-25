# Database Schema – AI Dreams World (V1 – SQLite)

Schema được thiết kế tương thích với Postgres để dễ migrate về sau.

---

## 1. Tables (simplified)

### `worlds`
- `id`
- `name`
- `created_at`

### `regions`
- `id`
- `world_id`
- `name`
- `biome`

### `locations`
- `id`
- `region_id`
- `kind` (island, mountain, settlement_site, dungeon, ...)
- `name`

### `civilizations`
- `id`
- `world_id`
- `name`
- `stage` (tribe, village, town, city_state, kingdom, empire)

### `settlements`
- `id`
- `civilization_id`
- `location_id`
- `name`
- `kind` (village, town, city)
- `population_estimate`

### `creatures`
- `id`
- `world_id`
- `species`
- `description`

### `events`
- `id`
- `world_id`
- `year`
- `era_id` (nullable)
- `event_type`
- `agent`
- `description`
- `affected_entities` (JSON)
- `is_canonical` (bool)

### `religions`
- `id`
- `world_id`
- `name`

### `cultures`
- `id`
- `civilization_id`
- `name`

### `resources`
- `id`
- `location_id`
- `kind`

### `eras`
- `id`
- `world_id`
- `name`
- `start_year`
- `end_year` (nullable)

---

V1 chỉ cần subset này; V2+ có thể thêm bảng phụ (trade_routes, alliances, etc.).
