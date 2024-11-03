По материалам видео:
https://www.youtube.com/watch?v=AmrnejpU4-0

Калькулятор параметров PG (PGTune)
https://pgtune.website.yandexcloud.net/

Рекомендации от Microsoft по тюнингу параметров ядра:
https://learn.microsoft.com/ru-ru/azure/azure-netapp-files/performance-linux-filesystem-cache

Параметры из калькулятора:
ALTER SYSTEM SET max_connections = '100';
ALTER SYSTEM SET shared_buffers = '6GB';
ALTER SYSTEM SET effective_cache_size = '18GB';
ALTER SYSTEM SET maintenance_work_mem = '1536MB';
ALTER SYSTEM SET checkpoint_completion_target = '0.9';
ALTER SYSTEM SET wal_buffers = '16MB';
ALTER SYSTEM SET default_statistics_target = '100';
ALTER SYSTEM SET random_page_cost = '1.1';
ALTER SYSTEM SET effective_io_concurrency = '200';
ALTER SYSTEM SET work_mem = '20971kB';
ALTER SYSTEM SET min_wal_size = '2GB';
ALTER SYSTEM SET max_wal_size = '8GB';
ALTER SYSTEM SET max_worker_processes = '6';
ALTER SYSTEM SET max_parallel_workers_per_gather = '3';
ALTER SYSTEM SET max_parallel_workers = '6';
ALTER SYSTEM SET max_parallel_maintenance_workers = '3';

Собственные:
ALTER SYSTEM SET parallel_setup_cost = '500';
ALTER SYSTEM SET cpu_operator_cost = '0.0025';
ALTER SYSTEM SET cpu_tuple_cost = '0.01';
ALTER SYSTEM SET autovacuum_work_mem = '1GB';
ALTER SYSTEM SET autovacuum_naptime = '5s';
ALTER SYSTEM SET autovacuum_vacuum_cost_limit = '8000';
ALTER SYSTEM SET autovacuum_vacuum_cost_delay = '2ms';
ALTER SYSTEM SET autovacuum_vacuum_scale_factor = '0';
ALTER SYSTEM SET autovacuum_analyze_scale_factor = '0';
После скольки мертвых записей в таблице начинать её автовакуумить (подбираете сами):
ALTER SYSTEM SET autovacuum_vacuum_threshold = '10000';
После скольки мертвых записей в таблице начинать сбор статистики (подбираете сами):
ALTER SYSTEM SET autovacuum_analyze_threshold = '500';
ALTER SYSTEM SET synchronous_commit = 'off';
ALTER SYSTEM SET wal_compression = 'on';
ALTER SYSTEM SET full_page_writes = 'on';
ALTER SYSTEM SET log_autovacuum_min_duration = '500ms';

Выборка параметров с фильтром:
SELECT name, setting FROM pg_settings where name like '%autovac%';

Включение больших страниц памяти в GRUB:
default_hugepagesz=1G hugepagesz=1G hugepages= transparent_hugepage=never

Рекомендации от Microsoft по тюнингу параметров ядра:
https://learn.microsoft.com/ru-ru/azu...

Мои параметры ядра:
VM
vm.dirty_background_ratio = 0
vm.dirty_ratio = 0
vm.dirty_background_bytes = 104857600
vm.dirty_bytes = 1073741824
vm.dirty_expire_centisecs = 3000
vm.dirty_writeback_centisecs = 1000
vm.overcommit_memory=2
vm.overcommit_ratio=100
vm.swappiness = 1

Kernel
kernel.numa_balancing = 0
kernel.sched_autogroup_enabled = 0
kernel.sched_migration_cost_ns = 50000000
kernel.sched_nr_migrate = 2
kernel.sched_min_granularity_ns = 100000000
kernel.sched_wakeup_granularity_ns = 10000000

Network
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
net.core.rmem_max = 1073741824
net.core.wmem_max = 1073741824
net.ipv4.tcp_rmem = 1048576 16777216 1073741824
net.ipv4.tcp_wmem = 1048576 16777216 1073741824
net.ipv4.tcp_fin_timeout = 30
net.ipv4.tcp_keepalive_intvl = 30
net.ipv4.tcp_reordering = 20
net.ipv4.tcp_mem = 1048576 16770216 1073741824