# oleg

Вот краткие пояснения по основным темам, чтобы разобраться и задавать точные вопросы. Я привел ключевые аспекты, которые можно обсудить на собеседовании.

---

### Linux:

1. **Дистрибутивы Linux**  
   Разные дистрибутивы (например, Ubuntu, CentOS, Debian) отличаются менеджерами пакетов, предустановленными инструментами и настройками. Для серверов часто используют CentOS, а для десктопов — Ubuntu.

2. **Процесс загрузки Linux**  
   Этапы: BIOS/UEFI → Загрузчик (GRUB) → Ядро → init/systemd → Загрузка сервисов и служб → Shell.

3. **Команды и утилиты**  
   - **Информация о системе:** `uname`, `top`, `free`, `df`.  
   - **Обработка текста:** `grep` (поиск строк), `sed` (замена), `vi` (текстовый редактор).

4. **Права на файлы**  
   Права: чтение (r), запись (w), выполнение (x). Они бывают для владельца, группы и всех.

5. **SystemD и логи**  
   `systemctl` — управление сервисами; `journalctl` — просмотр логов.

6. **suid, sgid, sticky bit**  
   - `suid`: выполнение от имени владельца.
   - `sgid`: выполнение от имени группы.
   - `sticky bit`: разрешает удаление файлов только владельцам.

7. **Виртуальная файловая система**  
   - `/dev` — устройства.
   - `/proc`, `/sys` — информация о системе.
   - `/run`, `/tmp` — временные файлы.

8. **RAID**  
   Объединение дисков для отказоустойчивости (RAID 1, 5) или скорости (RAID 0).

9. **LVM**  
   Логическое управление разделами, гибкое изменение размеров томов.

10. **Файловые системы**  
    Ext4, XFS — типы для хранения данных.

11. **mount/fstab**  
    `mount` — монтирование дисков; `fstab` — конфигурация для автоподключения при загрузке.

12. **Устройства, ядро, процессы, память**  
    - **Устройства:** `/dev` для доступа к дискам и другим устройствам.
    - **Ядро:** обеспечивает взаимодействие со всем оборудованием.
    - **Процессы:** управление процессами (`ps`, `top`).
    - **Память:** разделы виртуальной памяти и их диагностика.

13. **Bash-скрипты**  
    Сценарии для автоматизации. Основы: циклы (`for`), условия (`if`), команды (`echo`, `read`).

---

### Сеть:

1. **Базовая настройка**  
   Утилиты: `ifconfig` (старое), `ip` (новое).

2. **Продвинутые настройки**  
   - Маршрутизация: настройка путей для трафика.
   - VLAN: виртуальные сети для изоляции.
   - Bonding: объединение интерфейсов.

3. **Анализ сети**  
   - Основные: `ping` (проверка доступности), `netstat` (состояние сети).
   - `tcpdump`: перехват пакетов.

4. **Файрволы и NAT**  
   - `iptables`/`netfilter` — правила контроля трафика.
   - NAT: переадресация трафика.

---

### Траблшутинг:

1. **Проблемы с железом и прошивкой**  
   Решение аппаратных проблем: восстановление прошивок, сброс NVRAM.

2. **Проблемы при загрузке ОС**  
   Способы устранения ошибок при загрузке (`emergency mode`).

3. **Проблемы с дисками и ФС**  
   Диагностика ошибок дисков, RAID и команд для работы с ними (fsck, lvm).

4. **Проблемы и особенности ПО**  
   Восстановление PostgreSQL, влияние SELinux, задержка SSH.

5. **Проблемы с сетью**  
   Определение ошибок MTU, сетевых интерфейсов, туннели SSH.
