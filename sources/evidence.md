# Evidence Notes

Retrieved 2026-09-30 (Europe/Berlin). These notes preserve conclusions and pointers, not copies of third-party source material.

## Primary sources

1. **GlassBench repository** — https://github.com/davidalmeida90/glassbench
   - GlassBench is an Apache-2.0 UI/workbench around unmodified TradingAgents and AI Hedge Fund runs.
   - It records run events and metadata in SQLite, exposes an honest backtest simulator, and supports paper-only Interactive Brokers / Alpaca integrations.
   - Its own documented pilot had level-based agent trades lose money while buy-and-hold and a moving-average baseline gained.
   - It pins TradingAgents v0.5.1.

2. **GlassBench backtest method** — https://github.com/davidalmeida90/glassbench/blob/main/docs/backtest-method.md
   - The simulator uses weekly decisions, next-session-open fills, trading costs, long-only positions, and comparison with buy-and-hold, moving-average, and shuffled-rating placebo baselines.
   - Its initial pilot is a methodology check, not evidence of skill.

3. **TradingAgents repository** — https://github.com/TauricResearch/TradingAgents
   - Core multi-agent framework: analyst roles, bull/bear debate, trader, risk team, and portfolio manager.
   - Current checked release: v0.5.2, published 2026-09-29.
   - Supports global equities and crypto symbols that Yahoo Finance covers; its documented market examples do not make it a dedicated FX/futures or intraday price-action framework.
   - Its own reproducibility section says same ticker/date runs may differ and that news/social inputs can change over time.

4. **Creator video transcript** — https://youtu.be/Bvucb9BpJ1U
   - 02:05: the creator calls TradingAgents a harness rather than the LLM itself.
   - 05:03: shown run: 12 agents, about 19 model calls, around 8 minutes and $0.06.
   - 10:02: two Microsoft runs, two minutes apart, gave opposite ratings.
   - 10:27–12:21: the broker demonstration is paper-only, long-only, and proves plumbing rather than returns.
   - 12:59: the creator frames the work as structured experimentation with important limitations.

## Interpretation rule

Source claims establish what the tools do. Statements about suitability for this workspace are the report author's assessment, based on the workspace's TradingView/vectorbt-oriented data practices and price-action / FX / gold / futures interests.

## Backtesting workspace assessment

Reviewed 2026-09-30. The review covered first-party source, test, configuration,
brief, and report files across `/Backtesting`, while excluding virtual
environments, vendored libraries, caches, raw market data, and other binary
artifacts. The semantic inventory contained 2,560 relevant files.

- `AGENTS.md` makes TradingView through VectorBT Pro `TVData` the preferred
  data source and documents CME front-contract access; `utils/get_data.py`
  additionally resolves FX/CFD and futures exchanges with their natural
  timezones.
- `breakout_levels` is the strongest integration boundary. Its `PROGRESS.md`
  records 2016–2026 EUR/USD M5 and US500 M5 data, DST-aware CME sessions,
  54 passing tests, reproducible trial metadata, a locked holdout, and a
  strict intrabar-ambiguity policy. Its current EUR/USD campaign is explicitly
  `needs-better-data`, not production-ready.
- Existing specialised work includes the Bob Volman EUR/USD M5 mission, Al
  Brooks price-action backtests, First Strike FX/indices cross-pair research,
  custom VectorBT Pro order-function examples, and causal/robustness/
  reconciliation validation in the Algorithmic Short-Selling bundle.
- The proposal in `report.html` therefore retains these deterministic layers.
  TradingAgents is restricted to a version-pinned, structured, repeatable
  shadow-review role; GlassBench is a reference for run observability and
  comparison, not an adopted trading or execution platform.
