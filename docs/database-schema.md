# Database Schema – AI Dreams World (V1 – SQLite)

Schema được thiết kế tương thích với Postgres để dễ migrate về sau.

Mỗi world là một SQLite file riêng: `data/world-{name}.db`.

---

## 1. V1 Core Tables (Sprint 1)

Chỉ tạo tables thực sự cần cho MVP path. Xem [LIMITATIONS.md](LIMITATIONS.md) §M4 về rationale.

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

### `events`
- `id`
- `world_id`
- `year`
- `era_id` (nullable)
- `event_type`
- `agent`
- `description`
- `affected_entities` (JSON) — cũng dùng làm **soft reference** cho entities chưa có table riêng (creatures, religions, cultures, resources)
- `is_canonical` (bool)

### `eras`
- `id`
- `world_id`
- `name`
- `start_year`
- `end_year` (nullable)

---

## 2. Observability Tables (Sprint 2)

### `llm_call_log`
- `id`
- `tick_id`
- `agent`
- `prompt_hash` (SHA-256)
- `prompt_text`
- `response`
- `parsed_ok` (bool)
- `validated` (bool, nullable)
- `canonical` (bool, nullable)
- `latency_ms`
- `tokens_in`
- `tokens_out`
- `error` (nullable)
- `created_at`

### `tick_log`
- `id`
- `tick_id`
- `world_year`
- `agents_selected` (JSON)
- `proposals_generated`
- `proposals_accepted`
- `proposals_rejected`
- `reject_reasons` (JSON)
- `events_canonical`
- `total_tokens_in`
- `total_tokens_out`
- `total_latency_ms`
- `estimated_cost_usd`
- `tick_duration_ms`
- `created_at`

---

## 3. V2+ Extension Tables (Sprint 7+)

Tạo khi agent tương ứng được implement. Migration script extract data từ `affected_entities` JSON trong events → backfill tables.

### `creatures`
- `id`
- `world_id`
- `species`
- `description`

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

---

## 4. Schema Version Tracking

### `schema_version`
- `version`
- `applied_at`
- `description`

| Version | Sprint | Tables added |
|---------|--------|-------------|
| 1 | Sprint 1 | Core tables: worlds, regions, locations, civilizations, settlements, events, eras |
| 2 | Sprint 2 | Observability: llm_call_log, tick_log, schema_version |
| 3 | Sprint 7+ | Extension: creatures, religions |
| 4 | Sprint 8+ | Extension: cultures, resources |

---

V2+ có thể thêm bảng phụ (trade_routes, alliances, etc.).
