# Helm Chart: Grafana Resources (GitOps Ready)

Этот Helm-чарт предназначен для управления инфраструктурой мониторинга на базе **Grafana Operator (v5+)** в парадигме *Monitoring-as-Code* и *GitOps*. 

Чарт позволяет декларативно описывать сам инстанс Grafana, папки, источники данных (Data Sources), правила алертинга (Alerting Groups) и дашборды, минимизируя дублирование системного YAML-кода.

---

## 🚀 Возможности чарта

* **Инстанс Grafana**: Настройка реплик, Ingress (Traefik/Nginx), интеграция с внешней СУБД (PostgreSQL) и Google OAuth.
* **Автоматические папки**: Динамическое создание логических пространств (`GrafanaFolder`).
* **Умный Алертинг (Grafana Alerting)**: Описание правил в лаконичном формате. Шаблон сам генерирует сложную структуру `data` (PromQL запросы, Thresholds, `refId` связки) и избавляет от копипасты.
* **Гибкие Дашборды**: Возможность вставлять JSON как инлайн-строку в `values.yaml`, так и читать сырые JSON-файлы из отдельной директории чарта.
* **Безопасность**: Полная совместимость с *External Secrets Operator (ESO)* для безопасного проброса паролей баз данных и токенов (например, Telegram Bot Token).

---

## 📂 Структура проекта

```text
grafana-resources/
├── Chart.yaml
├── README.md
├── values.yaml
├── dashboards/             # Папка для сырых JSON-файлов дашбордов
│   └── node-exporter.json
└── templates/              # Шаблоны манифестов K8s (CRD Grafana)
    ├── _helpers.tpl
    ├── alert-contact-points.yaml
    ├── alert-notification-policies.yaml
    ├── alert-rule-groups.yaml
    ├── dashboards.yaml
    ├── datasources.yaml
    ├── folders.yaml
    └── grafana-instance.yaml
