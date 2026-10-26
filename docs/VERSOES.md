# Versões aprovadas

Levantamento em 2026-10-26 no servidor 10.144.128.58 (racktables.aom.org.br).
Alterações nesta tabela exigem aprovação do coordenador técnico.

| Componente | Versão | Observação |
|---|---|---|
| Ubuntu | 24.04.5 LTS | |
| PHP (CLI e FPM) | 8.3.6 | Pool FPM dedicado `racktables` |
| Apache | 2.4.58 | VirtualHost `racktables.aom.org.br`, porta 80; TLS no proxy reverso |
| MySQL | 8.0.46 (pacote Ubuntu) | Decisão pendente: manter 8.0 ou migrar para 8.4 LTS antes da produção |
| Composer | 2.10.3 | |
| Node | 22.23 | Usado apenas para build de assets (Vite), se necessário |
| Laravel | 13.38 | `laravel/framework ^13.17` |
| Livewire | 4.4 | |
| Pest | 4.7 | Testes rodam hoje em SQLite em memória; migrar para MySQL de teste |
| Larastan | 3.13 | Nível 5 (`phpstan.neon`) |
| Pint | 1.32 | Padrão Laravel |
| Fuso horário | America/Cuiaba | `config/app.php` |
