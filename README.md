
# Monitor.Grafana
* 監控系統 Grafana > Prometheus > Node-exporter + process-exporter + Cadvisor
* Grafana+Prometheus只需部屬一台主機即可監控所有節點

## 元件說明
被監控端所需元件:
* Node-exporter → 負責蒐集該主機硬體資訊(需授予root權限)
* process-exporter → 負責蒐集該主機process資訊
* Cadvisor → 負責蒐集該主機Docker容器內執行資訊

監控數據呈現所需元件:
* Prometheus → 負責紀錄各被監控端上的數據
* Grafana → 呈現監控數據與GUI


## 檔案樹說明(File tree)
```bash
.
├── AllinOne #Grafana+Prometheus+Node-exporter+Cadvisor 四合一
│   ├── data/ #數據存放資料夾
│   ├── docker-compose.yml
│   └── etc
│       └── prometheus
│           └── prometheus.yml #prometheus設定檔
├── Data_Source #Node-exporter+Cadvisor : 負責發送Docker主機數據
│   └── docker-compose.yml
├── Monitor #Grafana+Prometheus : 負責收集數據+監控介面
│   ├── data/ #數據存放資料夾
│   ├── docker-compose.yml
│   └── etc
│       └── prometheus
│           └── prometheus.yml #prometheus設定檔
│ 
├── docs #教學文件放置處
│   └── Grafana設定教學(包含prometheus).docx
│ 
├── scan_port.sh #簡易port掃描工具
├── Grafana設定dashboard.png #Grafana設定教學
└── Grafana設定DataSource.png  #Grafana設定教學
```
* AllinOne,Data_Source,Monitor 三者視需求使用


## 建置步驟(Build)
1. 設定各 ``docker-compose.yml``,``prometheus.yml``
2. 依照需求使用 ``docker-compose up`` 即可馬上部屬

## 注意事項(Reference)
1. 被監控端必須具備 ``root`` 權限
2. 被監控端必須設定 ``Docker`` 執行檔路徑



## 告警訊息備份
```
🐳 (From 阿里雲) Grafana Docker 告警 [CPU]
🧮   請留意以下Docker容器CPU使用率過高狀況 ....

🐳 (From 阿里雲) Grafana Docker 告警 [記憶體]
🚨  請留意以下Docker容器記憶體使用率過高狀況 ....

🐳 (From 阿里雲) Grafana Docker 告警 [網路使用量]
📡  請留意以下Docker容器記憶體使用率掉至0狀況 ....

Test
irate(container_network_transmit_bytes_total{job=~"cadvisor-Test",image!=""}[5m])
{{job}} - {{instance}} -Docker > {{name}}

Stage
irate(container_network_transmit_bytes_total{job=~"cadvisor-Stage",image!=""}[5m])
{{job}} - {{instance}} - {{Name}}

Prod
irate(container_network_transmit_bytes_total{job=~"cadvisor-Prod",image!=""}[5m])
{{job}} - {{instance}} - {{Name}}



💔 (From 阿里雲) Grafana Server 硬體告警 [硬碟空間]
🆓   整台 Server 硬碟空間不足20% ....

💔 (From 阿里雲) Grafana Server 硬體告警 [記憶體]
🚨  整台 Server [記憶體使用率超過90%] ....


💔 (From 阿里雲) Grafana Server 硬體告警 [CPU]
🧮  整台 Server [CPU使用率飆升99%] ....
```

