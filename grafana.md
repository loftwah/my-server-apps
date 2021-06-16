prometheus/prometheus.yml


```yaml
global:
  scrape_interval: 15s
  scrape_timeout: 10s
  evaluation_interval: 15s
alerting:
  alertmanagers:
  - scheme: http
    timeout: 10s
    api_version: v1
    static_configs:
    - targets:
      - alertmanager:9093
rule_files:
- /etc/prometheus/rules/*.yaml
scrape_configs:
- job_name: prometheus
  honor_timestamps: true
  scrape_interval: 15s
  scrape_timeout: 10s
  metrics_path: /metrics
  scheme: http
  static_configs:
  - targets:
    - localhost:9090
- job_name: grafana
  honor_timestamps: true
  scrape_interval: 15s
  scrape_timeout: 10s
  metrics_path: /metrics
  scheme: http
  static_configs:
  - targets:
    - grafana:3000
- job_name: node_exporter
  honor_timestamps: true
  scrape_interval: 15s
  scrape_timeout: 10s
  metrics_path: /metrics
  scheme: http
  static_configs:
  - targets:
    - node_exporter:9100
- job_name: traefik
  honor_timestamps: true
  scrape_interval: 15s
  scrape_timeout: 10s
  metrics_path: /metrics
  scheme: http
  static_configs:
  - targets:
    - traefik:8080
- job_name: cadvisor
  honor_timestamps: true
  scrape_interval: 15s
  scrape_timeout: 10s
  metrics_path: /metrics
  scheme: http
  static_configs:
  - targets:
    - cadvisor:8080
- job_name: alertmanager
  honor_timestamps: true
  scrape_interval: 15s
  scrape_timeout: 10s
  metrics_path: /metrics
  scheme: http
  static_configs:
  - targets:
    - alertmanager:9093
```

grafana-dashboard.json

```json
// 20210617082516
// https://raw.githubusercontent.com/tomMoulard/make-my-server/master/grafana/grafana-dashboard.json

{
  "__inputs": [
    {
      "name": "DS_PROMETHEUS",
      "label": "Prometheus",
      "description": "",
      "type": "datasource",
      "pluginId": "prometheus",
      "pluginName": "Prometheus"
    }
  ],
  "__requires": [
    {
      "type": "grafana",
      "id": "grafana",
      "name": "Grafana",
      "version": "7.2.2"
    },
    {
      "type": "panel",
      "id": "graph",
      "name": "Graph",
      "version": ""
    },
    {
      "type": "datasource",
      "id": "prometheus",
      "name": "Prometheus",
      "version": "1.0.0"
    },
    {
      "type": "panel",
      "id": "singlestat",
      "name": "Singlestat",
      "version": ""
    },
    {
      "type": "panel",
      "id": "table-old",
      "name": "Table (old)",
      "version": ""
    }
  ],
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": "-- Grafana --",
        "enable": true,
        "hide": true,
        "iconColor": "rgba(0, 211, 255, 1)",
        "name": "Annotations & Alerts",
        "type": "dashboard"
      }
    ]
  },
  "description": "A simple overview of the most important Docker host and container metrics. (cAdvisor/Prometheus)",
  "editable": true,
  "gnetId": 893,
  "graphTooltip": 1,
  "id": null,
  "iteration": 1603635126503,
  "links": [
    
  ],
  "panels": [
    {
      "cacheTimeout": null,
      "colorBackground": false,
      "colorValue": false,
      "colors": [
        "rgba(245, 54, 54, 0.9)",
        "rgba(237, 129, 40, 0.89)",
        "rgba(50, 172, 45, 0.97)"
      ],
      "datasource": "${DS_PROMETHEUS}",
      "decimals": 0,
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "format": "s",
      "gauge": {
        "maxValue": 100,
        "minValue": 0,
        "show": false,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 4,
        "w": 4,
        "x": 0,
        "y": 0
      },
      "height": "",
      "id": 24,
      "interval": null,
      "links": [
        
      ],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "nullText": null,
      "postfix": "",
      "postfixFontSize": "30%",
      "prefix": "",
      "prefixFontSize": "20%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "sparkline": {
        "fillColor": "rgba(31, 118, 189, 0.18)",
        "full": false,
        "lineColor": "rgb(31, 120, 193)",
        "show": false
      },
      "tableColumn": "",
      "targets": [
        {
          "expr": "time() - node_boot_time_seconds{}",
          "hide": false,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "A",
          "step": 1800
        }
      ],
      "thresholds": "",
      "title": "Uptime",
      "type": "singlestat",
      "valueFontSize": "80%",
      "valueMaps": [
        {
          "op": "=",
          "text": "N/A",
          "value": "null"
        }
      ],
      "valueName": "current"
    },
    {
      "cacheTimeout": null,
      "colorBackground": false,
      "colorValue": false,
      "colors": [
        "rgba(245, 54, 54, 0.9)",
        "rgba(237, 129, 40, 0.89)",
        "rgba(50, 172, 45, 0.97)"
      ],
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "format": "none",
      "gauge": {
        "maxValue": 100,
        "minValue": 0,
        "show": false,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 4,
        "w": 4,
        "x": 4,
        "y": 0
      },
      "id": 31,
      "interval": null,
      "links": [
        
      ],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "nullText": null,
      "postfix": "",
      "postfixFontSize": "50%",
      "prefix": "",
      "prefixFontSize": "50%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "sparkline": {
        "fillColor": "rgba(31, 118, 189, 0.18)",
        "full": false,
        "lineColor": "rgb(31, 120, 193)",
        "show": false
      },
      "tableColumn": "",
      "targets": [
        {
          "expr": "count(rate(container_last_seen{name=~\".+\"}[$interval]))",
          "intervalFactor": 2,
          "refId": "A",
          "step": 1800
        }
      ],
      "thresholds": "",
      "title": "Containers",
      "type": "singlestat",
      "valueFontSize": "120%",
      "valueMaps": [
        {
          "op": "=",
          "text": "N/A",
          "value": "null"
        }
      ],
      "valueName": "current"
    },
    {
      "cacheTimeout": null,
      "colorBackground": false,
      "colorValue": false,
      "colors": [
        "rgba(50, 172, 45, 0.97)",
        "rgba(237, 129, 40, 0.89)",
        "rgba(245, 54, 54, 0.9)"
      ],
      "datasource": "${DS_PROMETHEUS}",
      "decimals": 1,
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "format": "percentunit",
      "gauge": {
        "maxValue": 1,
        "minValue": 0,
        "show": true,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 4,
        "w": 4,
        "x": 8,
        "y": 0
      },
      "id": 26,
      "interval": null,
      "links": [
        
      ],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "nullText": null,
      "postfix": "",
      "postfixFontSize": "50%",
      "prefix": "",
      "prefixFontSize": "50%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "sparkline": {
        "fillColor": "rgba(31, 118, 189, 0.18)",
        "full": false,
        "lineColor": "rgb(31, 120, 193)",
        "show": false
      },
      "tableColumn": "",
      "targets": [
        {
          "expr": "min((node_filesystem_size_bytes{fstype=~\"xfs|ext4\"} - node_filesystem_free_bytes{fstype=~\"xfs|ext4\"} )/ node_filesystem_size_bytes{fstype=~\"xfs|ext4\"})",
          "hide": false,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "A",
          "step": 1800
        }
      ],
      "thresholds": "0.75, 0.90",
      "title": "Disk space",
      "type": "singlestat",
      "valueFontSize": "80%",
      "valueMaps": [
        {
          "op": "=",
          "text": "N/A",
          "value": "null"
        }
      ],
      "valueName": "current"
    },
    {
      "cacheTimeout": null,
      "colorBackground": false,
      "colorValue": false,
      "colors": [
        "rgba(50, 172, 45, 0.97)",
        "rgba(237, 129, 40, 0.89)",
        "rgba(245, 54, 54, 0.9)"
      ],
      "datasource": "${DS_PROMETHEUS}",
      "decimals": 0,
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "format": "percent",
      "gauge": {
        "maxValue": 100,
        "minValue": 0,
        "show": true,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 4,
        "w": 4,
        "x": 12,
        "y": 0
      },
      "id": 25,
      "interval": null,
      "links": [
        
      ],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "nullText": null,
      "postfix": "",
      "postfixFontSize": "50%",
      "prefix": "",
      "prefixFontSize": "50%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "sparkline": {
        "fillColor": "rgba(31, 118, 189, 0.18)",
        "full": false,
        "lineColor": "rgb(31, 120, 193)",
        "show": false
      },
      "tableColumn": "",
      "targets": [
        {
          "expr": "((node_memory_MemTotal_bytes{} - node_memory_MemAvailable_bytes{}) / node_memory_MemTotal_bytes{}) * 100",
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "A",
          "step": 1800
        }
      ],
      "thresholds": "70, 90",
      "title": "Memory",
      "type": "singlestat",
      "valueFontSize": "80%",
      "valueMaps": [
        {
          "op": "=",
          "text": "N/A",
          "value": "null"
        }
      ],
      "valueName": "current"
    },
    {
      "cacheTimeout": null,
      "colorBackground": false,
      "colorValue": false,
      "colors": [
        "rgba(50, 172, 45, 0.97)",
        "rgba(237, 129, 40, 0.89)",
        "rgba(245, 54, 54, 0.9)"
      ],
      "datasource": "${DS_PROMETHEUS}",
      "decimals": 0,
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "format": "decbytes",
      "gauge": {
        "maxValue": 500000000,
        "minValue": 0,
        "show": true,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 4,
        "w": 4,
        "x": 16,
        "y": 0
      },
      "id": 30,
      "interval": null,
      "links": [
        
      ],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "nullText": null,
      "postfix": "",
      "postfixFontSize": "50%",
      "prefix": "",
      "prefixFontSize": "50%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "sparkline": {
        "fillColor": "rgba(31, 118, 189, 0.18)",
        "full": false,
        "lineColor": "rgb(31, 120, 193)",
        "show": false
      },
      "tableColumn": "",
      "targets": [
        {
          "expr": "(node_memory_SwapTotal_bytes{} - node_memory_SwapFree_bytes{})",
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "A",
          "step": 1800
        }
      ],
      "thresholds": "400000000",
      "title": "Swap",
      "type": "singlestat",
      "valueFontSize": "80%",
      "valueMaps": [
        {
          "op": "=",
          "text": "N/A",
          "value": "null"
        }
      ],
      "valueName": "current"
    },
    {
      "cacheTimeout": null,
      "colorBackground": false,
      "colorValue": false,
      "colors": [
        "rgba(245, 54, 54, 0.9)",
        "rgba(237, 129, 40, 0.89)",
        "rgba(50, 172, 45, 0.97)"
      ],
      "datasource": "${DS_PROMETHEUS}",
      "decimals": 0,
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "format": "percentunit",
      "gauge": {
        "maxValue": 100,
        "minValue": 0,
        "show": false,
        "thresholdLabels": false,
        "thresholdMarkers": true
      },
      "gridPos": {
        "h": 4,
        "w": 4,
        "x": 20,
        "y": 0
      },
      "id": 27,
      "interval": null,
      "links": [
        
      ],
      "mappingType": 1,
      "mappingTypes": [
        {
          "name": "value to text",
          "value": 1
        },
        {
          "name": "range to text",
          "value": 2
        }
      ],
      "maxDataPoints": 100,
      "nullPointMode": "connected",
      "nullText": null,
      "postfix": "",
      "postfixFontSize": "50%",
      "prefix": "",
      "prefixFontSize": "50%",
      "rangeMaps": [
        {
          "from": "null",
          "text": "N/A",
          "to": "null"
        }
      ],
      "sparkline": {
        "fillColor": "rgba(50, 189, 31, 0.18)",
        "full": false,
        "lineColor": "rgb(69, 193, 31)",
        "show": true
      },
      "tableColumn": "",
      "targets": [
        {
          "expr": "node_load1{} / count by(job, instance)(count by(job, instance, core)(node_cpu_core_throttles_total{}))",
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "A",
          "step": 1800
        }
      ],
      "thresholds": "0.8,0.9",
      "title": "Load",
      "type": "singlestat",
      "valueFontSize": "80%",
      "valueMaps": [
        {
          "op": "=",
          "text": "N/A",
          "value": "null"
        }
      ],
      "valueName": "avg"
    },
    {
      "aliasColors": {
        "SENT": "#BF1B00"
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 1,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 6,
        "w": 4,
        "x": 0,
        "y": 4
      },
      "hiddenSeries": false,
      "id": 19,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": false,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 1,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "targets": [
        {
          "expr": "sum(rate(container_network_receive_bytes_total{id=\"/\"}[$interval])) by (id)",
          "intervalFactor": 2,
          "legendFormat": "RECEIVED",
          "refId": "A",
          "step": 600
        },
        {
          "expr": "- sum(rate(container_network_transmit_bytes_total{id=\"/\"}[$interval])) by (id)",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "SENT",
          "refId": "B",
          "step": 600
        }
      ],
      "thresholds": [
        
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "Network Traffic",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 0,
        "value_type": "cumulative"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": false,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "bytes",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": false
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "aliasColors": {
        "{id=\"/\",instance=\"cadvisor:8080\",job=\"prometheus\"}": "#BA43A9"
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 1,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 6,
        "w": 4,
        "x": 4,
        "y": 4
      },
      "hiddenSeries": false,
      "id": 5,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": false,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": true,
      "steppedLine": false,
      "targets": [
        {
          "expr": "sum(rate(container_cpu_system_seconds_total[1m]))",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "a",
          "refId": "B",
          "step": 120
        },
        {
          "expr": "sum(rate(container_cpu_system_seconds_total{name=~\".+\"}[1m]))",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "nur container",
          "refId": "F",
          "step": 10
        },
        {
          "expr": "sum(rate(container_cpu_system_seconds_total{id=\"/\"}[1m]))",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "nur docker host",
          "metric": "",
          "refId": "A",
          "step": 20
        },
        {
          "expr": "sum(rate(process_cpu_seconds_total[$interval])) * 100",
          "hide": false,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "host",
          "metric": "",
          "refId": "C",
          "step": 600
        },
        {
          "expr": "sum(rate(container_cpu_system_seconds_total{name=~\".+\"}[1m])) + sum(rate(container_cpu_system_seconds_total{id=\"/\"}[1m])) + sum(rate(process_cpu_seconds_total[1m]))",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "D",
          "step": 120
        }
      ],
      "thresholds": [
        
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "CPU Usage",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 0,
        "value_type": "cumulative"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": false,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "percent",
          "label": "",
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": false
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "alert": {
        "conditions": [
          {
            "evaluator": {
              "params": [
                1.25
              ],
              "type": "gt"
            },
            "query": {
              "params": [
                "A",
                "5m",
                "now"
              ]
            },
            "reducer": {
              "params": [
                
              ],
              "type": "avg"
            },
            "type": "query"
          }
        ],
        "executionErrorState": "alerting",
        "frequency": "60s",
        "handler": 1,
        "name": "Panel Title alert",
        "noDataState": "keep_state",
        "notifications": [
          {
            "id": 1
          }
        ]
      },
      "aliasColors": {
        
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "decimals": 0,
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 1,
      "fillGradient": 0,
      "gridPos": {
        "h": 6,
        "w": 4,
        "x": 8,
        "y": 4
      },
      "hiddenSeries": false,
      "id": 28,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": false,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "links": [
        
      ],
      "nullPointMode": "connected",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "targets": [
        {
          "expr": "node_load1{} / count by(job, instance)(count by(job, instance, core)(node_cpu_core_throttles_total{}))",
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "A",
          "step": 600
        }
      ],
      "thresholds": [
        {
          "colorMode": "critical",
          "fill": true,
          "line": true,
          "op": "gt",
          "value": 1.25
        }
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "Load",
      "tooltip": {
        "msResolution": false,
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": false,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "percentunit",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": false
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "alert": {
        "alertRuleTags": {
          
        },
        "conditions": [
          {
            "evaluator": {
              "params": [
                2000000000000
              ],
              "type": "gt"
            },
            "query": {
              "params": [
                "A",
                "5m",
                "now"
              ]
            },
            "reducer": {
              "params": [
                
              ],
              "type": "avg"
            },
            "type": "query"
          }
        ],
        "executionErrorState": "alerting",
        "for": "0m",
        "frequency": "60s",
        "handler": 1,
        "name": "Free/Used Disk Space alert",
        "noDataState": "keep_state",
        "notifications": [
          {
            "id": 1
          }
        ]
      },
      "aliasColors": {
        "Belegete Festplatte": "#BF1B00",
        "Free Disk Space": "#7EB26D",
        "Used Disk Space": "#7EB26D",
        "{}": "#BF1B00"
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 1,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 6,
        "w": 4,
        "x": 12,
        "y": 4
      },
      "hiddenSeries": false,
      "id": 13,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": false,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        {
          "alias": "Used Disk Space",
          "yaxis": 1
        }
      ],
      "spaceLength": 10,
      "stack": true,
      "steppedLine": false,
      "targets": [
        {
          "expr": "min(node_filesystem_size_bytes{}) - min(node_filesystem_free_bytes{})",
          "hide": false,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "Used Disk Space",
          "refId": "A",
          "step": 600
        }
      ],
      "thresholds": [
        {
          "colorMode": "critical",
          "fill": true,
          "line": true,
          "op": "gt",
          "value": 2000000000000
        }
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "Used Disk Space",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": false,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "bytes",
          "label": "",
          "logBase": 1,
          "max": null,
          "min": 0,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": false
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "alert": {
        "conditions": [
          {
            "evaluator": {
              "params": [
                10000000000
              ],
              "type": "gt"
            },
            "query": {
              "params": [
                "A",
                "5m",
                "now"
              ]
            },
            "reducer": {
              "params": [
                
              ],
              "type": "avg"
            },
            "type": "query"
          }
        ],
        "executionErrorState": "alerting",
        "frequency": "60s",
        "handler": 1,
        "name": "Available Memory alert",
        "noDataState": "keep_state",
        "notifications": [
          {
            "id": 1
          }
        ]
      },
      "aliasColors": {
        "Available Memory": "#7EB26D",
        "Unavailable Memory": "#7EB26D"
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 1,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 6,
        "w": 4,
        "x": 16,
        "y": 4
      },
      "hiddenSeries": false,
      "id": 20,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": false,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": true,
      "steppedLine": false,
      "targets": [
        {
          "expr": "container_memory_rss{name=~\".+\"}",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "D",
          "step": 20
        },
        {
          "expr": "sum(container_memory_rss{name=~\".+\"})",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "A",
          "step": 20
        },
        {
          "expr": "container_memory_usage_bytes{name=~\".+\"}",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "B",
          "step": 20
        },
        {
          "expr": "container_memory_rss{id=\"/\"}",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "C",
          "step": 20
        },
        {
          "expr": "sum(container_memory_rss)",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "E",
          "step": 20
        },
        {
          "expr": "node_memory_Buffers_bytes",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "node_memory_Dirty",
          "refId": "N",
          "step": 30
        },
        {
          "expr": "node_memory_MemFree_bytes",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "F",
          "step": 20
        },
        {
          "expr": "node_memory_MemAvailable_bytes",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "Available Memory",
          "refId": "H",
          "step": 20
        },
        {
          "expr": "node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes",
          "hide": false,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "Unavailable Memory",
          "refId": "G",
          "step": 600
        },
        {
          "expr": "node_memory_Inactive_bytes",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "I",
          "step": 30
        },
        {
          "expr": "node_memory_KernelStack_bytes",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "J",
          "step": 30
        },
        {
          "expr": "node_memory_Active_bytes",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "K",
          "step": 30
        },
        {
          "expr": "node_memory_MemTotal_bytes - (node_memory_Active_bytes + node_memory_MemFree_bytes + node_memory_Inactive_bytes)",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "Unknown",
          "refId": "L",
          "step": 40
        },
        {
          "expr": "node_memory_MemFree_bytes + node_memory_Inactive_bytes",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "M",
          "step": 30
        },
        {
          "expr": "container_memory_rss{name=~\".+\"}",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{__name__}}",
          "refId": "O",
          "step": 30
        },
        {
          "expr": "node_memory_Inactive_bytes + node_memory_MemFree_bytes + node_memory_MemAvailable_bytes",
          "hide": true,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "P",
          "step": 40
        }
      ],
      "thresholds": [
        {
          "colorMode": "critical",
          "fill": true,
          "line": true,
          "op": "gt",
          "value": 10000000000
        }
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "Available Memory",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": false,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "bytes",
          "label": "",
          "logBase": 1,
          "max": 16000000000,
          "min": 0,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": false
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "aliasColors": {
        "IN on /sda": "#7EB26D",
        "OUT on /sda": "#890F02"
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 1,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 6,
        "w": 4,
        "x": 20,
        "y": 4
      },
      "hiddenSeries": false,
      "id": 3,
      "legend": {
        "avg": false,
        "current": false,
        "max": false,
        "min": false,
        "show": false,
        "total": false,
        "values": false
      },
      "lines": true,
      "linewidth": 1,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "targets": [
        {
          "expr": "-sum(rate(node_disk_read_bytes_total[$interval])) by (device)",
          "hide": false,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "OUT on /{{device}}",
          "metric": "node_disk_bytes_read",
          "refId": "A",
          "step": 600
        },
        {
          "expr": "sum(rate(node_disk_written_bytes_total[$interval])) by (device)",
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "IN on /{{device}}",
          "metric": "",
          "refId": "B",
          "step": 600
        }
      ],
      "thresholds": [
        
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "Disk I/O",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 0,
        "value_type": "cumulative"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": false,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "Bps",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": false
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "aliasColors": {
        
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 1,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 7,
        "w": 12,
        "x": 0,
        "y": 10
      },
      "hiddenSeries": false,
      "id": 8,
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": true,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "sort": "current",
        "sortDesc": true,
        "total": false,
        "values": true
      },
      "lines": true,
      "linewidth": 2,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "targets": [
        {
          "expr": "sum(rate(container_network_receive_bytes_total{name=~\".+\"}[$interval])) by (name)",
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "A",
          "step": 240
        },
        {
          "expr": "- rate(container_network_transmit_bytes_total{name=~\".+\"}[$interval])",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "B",
          "step": 10
        }
      ],
      "thresholds": [
        
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "Received Network Traffic per Container",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 2,
        "value_type": "cumulative"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": true,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "Bps",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "aliasColors": {
        
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 1,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 7,
        "w": 12,
        "x": 12,
        "y": 10
      },
      "hiddenSeries": false,
      "id": 9,
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": true,
        "hideEmpty": false,
        "hideZero": false,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "sort": "current",
        "sortDesc": true,
        "total": false,
        "values": true
      },
      "lines": true,
      "linewidth": 2,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": false,
      "steppedLine": false,
      "targets": [
        {
          "expr": "sum(rate(container_network_transmit_bytes_total{name=~\".+\"}[$interval])) by (name)",
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "A",
          "step": 240
        },
        {
          "expr": "rate(container_network_transmit_bytes_total{id=\"/\"}[$interval])",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "",
          "refId": "B",
          "step": 10
        }
      ],
      "thresholds": [
        
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "Sent Network Traffic per Container",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 0,
        "value_type": "cumulative"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": true,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "Bps",
          "label": "",
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "format": "short",
          "label": "",
          "logBase": 10,
          "max": 8,
          "min": 0,
          "show": false
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "aliasColors": {
        
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 5,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 7,
        "w": 12,
        "x": 0,
        "y": 17
      },
      "hiddenSeries": false,
      "id": 1,
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": true,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "sort": "current",
        "sortDesc": true,
        "total": false,
        "values": true
      },
      "lines": true,
      "linewidth": 1,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": true,
      "steppedLine": false,
      "targets": [
        {
          "expr": "sum(rate(container_cpu_usage_seconds_total{name=~\".+\"}[$interval])) by (name) * 100",
          "hide": false,
          "interval": "",
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "metric": "",
          "refId": "F",
          "step": 240
        }
      ],
      "thresholds": [
        
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "CPU Usage per Container",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": true,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "percent",
          "label": "",
          "logBase": 1,
          "max": null,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": false
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "aliasColors": {
        
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 3,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 7,
        "w": 12,
        "x": 12,
        "y": 17
      },
      "hiddenSeries": false,
      "id": 34,
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": true,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "sort": "current",
        "sortDesc": true,
        "total": false,
        "values": true
      },
      "lines": true,
      "linewidth": 2,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": true,
      "steppedLine": false,
      "targets": [
        {
          "expr": "sum(container_memory_swap{name=~\".+\"}) by (name)",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "A",
          "step": 240
        },
        {
          "expr": "container_memory_usage_bytes{name=~\".+\"}",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "B",
          "step": 240
        }
      ],
      "thresholds": [
        
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "Memory Swap per Container",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": true,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "bytes",
          "label": "",
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "aliasColors": {
        
      },
      "bars": false,
      "dashLength": 10,
      "dashes": false,
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fill": 3,
      "fillGradient": 0,
      "grid": {
        
      },
      "gridPos": {
        "h": 7,
        "w": 12,
        "x": 0,
        "y": 24
      },
      "hiddenSeries": false,
      "id": 10,
      "legend": {
        "alignAsTable": true,
        "avg": false,
        "current": true,
        "max": false,
        "min": false,
        "rightSide": true,
        "show": true,
        "sort": "current",
        "sortDesc": true,
        "total": false,
        "values": true
      },
      "lines": true,
      "linewidth": 2,
      "links": [
        
      ],
      "nullPointMode": "null as zero",
      "options": {
        "alertThreshold": true
      },
      "percentage": false,
      "pluginVersion": "7.2.2",
      "pointradius": 5,
      "points": false,
      "renderer": "flot",
      "seriesOverrides": [
        
      ],
      "spaceLength": 10,
      "stack": true,
      "steppedLine": false,
      "targets": [
        {
          "expr": "sum(container_memory_rss{name=~\".+\"}) by (name)",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "A",
          "step": 240
        },
        {
          "expr": "container_memory_usage_bytes{name=~\".+\"}",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "B",
          "step": 240
        }
      ],
      "thresholds": [
        
      ],
      "timeFrom": null,
      "timeRegions": [
        
      ],
      "timeShift": null,
      "title": "Memory Usage per Container",
      "tooltip": {
        "msResolution": true,
        "shared": true,
        "sort": 0,
        "value_type": "individual"
      },
      "type": "graph",
      "xaxis": {
        "buckets": null,
        "mode": "time",
        "name": null,
        "show": true,
        "values": [
          
        ]
      },
      "yaxes": [
        {
          "format": "bytes",
          "label": "",
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        },
        {
          "format": "short",
          "label": null,
          "logBase": 1,
          "max": null,
          "min": null,
          "show": true
        }
      ],
      "yaxis": {
        "align": false,
        "alignLevel": null
      }
    },
    {
      "columns": [
        {
          "text": "Current",
          "value": "current"
        }
      ],
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fontSize": "100%",
      "gridPos": {
        "h": 10,
        "w": 8,
        "x": 16,
        "y": 24
      },
      "id": 36,
      "links": [
        
      ],
      "pageSize": null,
      "scroll": true,
      "showHeader": true,
      "sort": {
        "col": 1,
        "desc": true
      },
      "styles": [
        {
          "align": "auto",
          "colorMode": null,
          "colors": [
            "rgba(245, 54, 54, 0.9)",
            "rgba(237, 129, 40, 0.89)",
            "rgba(50, 172, 45, 0.97)"
          ],
          "decimals": 2,
          "pattern": "/.*/",
          "thresholds": [
            "10000000",
            " 25000000"
          ],
          "type": "number",
          "unit": "decbytes"
        }
      ],
      "targets": [
        {
          "expr": "sum(container_spec_memory_limit_bytes{name=~\".+\"} - container_memory_usage_bytes{name=~\".+\"}) by (name) ",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "metric": "",
          "refId": "A",
          "step": 240
        },
        {
          "expr": "sum(container_spec_memory_limit_bytes{name=~\".+\"}) by (name) ",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "B",
          "step": 240
        },
        {
          "expr": "container_memory_usage_bytes{name=~\".+\"}",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "C",
          "step": 240
        }
      ],
      "title": "Limit memory",
      "transform": "timeseries_aggregations",
      "type": "table-old"
    },
    {
      "columns": [
        {
          "text": "Current",
          "value": "current"
        }
      ],
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fontSize": "100%",
      "gridPos": {
        "h": 10,
        "w": 8,
        "x": 0,
        "y": 31
      },
      "id": 37,
      "links": [
        
      ],
      "pageSize": null,
      "scroll": true,
      "showHeader": true,
      "sort": {
        "col": 1,
        "desc": true
      },
      "styles": [
        {
          "align": "auto",
          "colorMode": null,
          "colors": [
            "rgba(245, 54, 54, 0.9)",
            "rgba(237, 129, 40, 0.89)",
            "rgba(50, 172, 45, 0.97)"
          ],
          "decimals": 2,
          "pattern": "/.*/",
          "thresholds": [
            "10000000",
            " 25000000"
          ],
          "type": "number",
          "unit": "decbytes"
        }
      ],
      "targets": [
        {
          "expr": "sum(container_spec_memory_limit_bytes{name=~\".+\"} - container_memory_usage_bytes{name=~\".+\"}) by (name) ",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "metric": "",
          "refId": "A",
          "step": 240
        },
        {
          "expr": "sum(container_spec_memory_limit_bytes{name=~\".+\"}) by (name) ",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "B",
          "step": 240
        },
        {
          "expr": "container_memory_usage_bytes{name=~\".+\"}",
          "hide": false,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "C",
          "step": 240
        }
      ],
      "title": "Usage memory",
      "transform": "timeseries_aggregations",
      "type": "table-old"
    },
    {
      "columns": [
        {
          "text": "Current",
          "value": "current"
        }
      ],
      "datasource": "${DS_PROMETHEUS}",
      "editable": true,
      "error": false,
      "fieldConfig": {
        "defaults": {
          "custom": {
            
          }
        },
        "overrides": [
          
        ]
      },
      "fontSize": "100%",
      "gridPos": {
        "h": 10,
        "w": 8,
        "x": 8,
        "y": 31
      },
      "id": 35,
      "links": [
        
      ],
      "pageSize": null,
      "scroll": true,
      "showHeader": true,
      "sort": {
        "col": 1,
        "desc": false
      },
      "styles": [
        {
          "align": "auto",
          "colorMode": "cell",
          "colors": [
            "rgba(50, 172, 45, 0.97)",
            "rgba(237, 129, 40, 0.89)",
            "rgba(245, 54, 54, 0.9)"
          ],
          "decimals": 2,
          "pattern": "/.*/",
          "thresholds": [
            "80",
            "90"
          ],
          "type": "number",
          "unit": "percent"
        }
      ],
      "targets": [
        {
          "expr": "sum(100 - ((container_spec_memory_limit_bytes{name=~\".+\"} - container_memory_usage_bytes{name=~\".+\"})  * 100 / container_spec_memory_limit_bytes{name=~\".+\"}) ) by (name) ",
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "metric": "",
          "refId": "A",
          "step": 240
        },
        {
          "expr": "sum(container_spec_memory_limit_bytes{name=~\".+\"}) by (name) ",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "B",
          "step": 240
        },
        {
          "expr": "container_memory_usage_bytes{name=~\".+\"}",
          "hide": true,
          "intervalFactor": 2,
          "legendFormat": "{{name}}",
          "refId": "C",
          "step": 240
        }
      ],
      "title": "Remaining memory",
      "transform": "timeseries_aggregations",
      "type": "table-old"
    }
  ],
  "refresh": "5m",
  "schemaVersion": 26,
  "style": "dark",
  "tags": [
    
  ],
  "templating": {
    "list": [
      {
        "allValue": ".+",
        "current": {
          
        },
        "datasource": "${DS_PROMETHEUS}",
        "definition": "",
        "hide": 0,
        "includeAll": true,
        "label": "Container Group",
        "multi": true,
        "name": "containergroup",
        "options": [
          
        ],
        "query": "label_values(container_group)",
        "refresh": 1,
        "regex": "",
        "skipUrlSync": false,
        "sort": 0,
        "tagValuesQuery": null,
        "tags": [
          
        ],
        "tagsQuery": null,
        "type": "query",
        "useTags": false
      },
      {
        "auto": true,
        "auto_count": 50,
        "auto_min": "50s",
        "current": {
          "selected": false,
          "text": "auto",
          "value": "$__auto_interval_interval"
        },
        "datasource": null,
        "hide": 0,
        "includeAll": false,
        "label": "Interval",
        "multi": false,
        "name": "interval",
        "options": [
          {
            "selected": true,
            "text": "auto",
            "value": "$__auto_interval_interval"
          },
          {
            "selected": false,
            "text": "30s",
            "value": "30s"
          },
          {
            "selected": false,
            "text": "1m",
            "value": "1m"
          },
          {
            "selected": false,
            "text": "2m",
            "value": "2m"
          },
          {
            "selected": false,
            "text": "3m",
            "value": "3m"
          },
          {
            "selected": false,
            "text": "5m",
            "value": "5m"
          },
          {
            "selected": false,
            "text": "7m",
            "value": "7m"
          },
          {
            "selected": false,
            "text": "10m",
            "value": "10m"
          },
          {
            "selected": false,
            "text": "30m",
            "value": "30m"
          },
          {
            "selected": false,
            "text": "1h",
            "value": "1h"
          },
          {
            "selected": false,
            "text": "6h",
            "value": "6h"
          },
          {
            "selected": false,
            "text": "12h",
            "value": "12h"
          },
          {
            "selected": false,
            "text": "1d",
            "value": "1d"
          },
          {
            "selected": false,
            "text": "7d",
            "value": "7d"
          },
          {
            "selected": false,
            "text": "14d",
            "value": "14d"
          },
          {
            "selected": false,
            "text": "30d",
            "value": "30d"
          }
        ],
        "query": "30s,1m,2m,3m,5m,7m,10m,30m,1h,6h,12h,1d,7d,14d,30d",
        "queryValue": "",
        "refresh": 2,
        "skipUrlSync": false,
        "type": "interval"
      },
      {
        "allValue": null,
        "current": {
          
        },
        "datasource": "${DS_PROMETHEUS}",
        "definition": "",
        "hide": 0,
        "includeAll": false,
        "label": "Node",
        "multi": true,
        "name": "server",
        "options": [
          
        ],
        "query": "label_values(node_boot_time, instance)",
        "refresh": 1,
        "regex": "/([^:]+):.*/",
        "skipUrlSync": false,
        "sort": 0,
        "tagValuesQuery": null,
        "tags": [
          
        ],
        "tagsQuery": null,
        "type": "query",
        "useTags": false
      }
    ]
  },
  "time": {
    "from": "now-24h",
    "to": "now"
  },
  "timepicker": {
    "refresh_intervals": [
      "5s",
      "10s",
      "30s",
      "1m",
      "5m",
      "15m",
      "30m",
      "1h",
      "2h",
      "1d"
    ],
    "time_options": [
      "5m",
      "15m",
      "1h",
      "6h",
      "12h",
      "24h",
      "2d",
      "7d",
      "30d"
    ]
  },
  "timezone": "browser",
  "title": "Docker and system monitoring",
  "uid": "mHHQt2pMk",
  "version": 6
}
```

version: '2'

services:
  grafana:
    image: grafana/grafana:7.2.2
    volumes:
      - './grafana/grafana:/var/lib/grafana'
    networks:
      - 'srv'
    user: 1000:1000
    restart: always
    depends_on:
      - prometheus
    labels:
      - 'traefik.enable=true'
      - 'traefik.http.routers.grafana.rule=Host(`grafana.${SITE}`)'
      - 'traefik.http.services.grafana.loadbalancer.server.port=3000'
      - 'traefik.http.routers.grafana.middlewares=basic_auth@docker'
    environment:
      - 'GF_METRICS_ENABLED=true'
      - 'GF_AUTH_ANONYMOUS_ENABLED=true'
      - 'GF_AUTH_ANONYMOUS_ORG_ROLE=Admin'
      - 'GF_AUTH_BASIC_ENABLED=false'
      - 'GF_AUTH_DISABLE_LOGIN_FORM=true'
      - 'GF_INSTALL_PLUGINS=grafana-piechart-panel'

  prometheus:
    image: prom/prometheus:v2.22.0
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--storage.tsdb.retention.time=30d'
      - '--web.console.libraries=/usr/share/prometheus/console_libraries'
      - '--web.console.templates=/usr/share/prometheus/consoles'
    networks:
      - 'srv'
    user: 1000:1000
    restart: always
    depends_on:
      - node_exporter
      - alertmanager
      - cadvisor
    volumes:
      - './grafana/prometheus/datas:/prometheus'
      - './grafana/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml'
      - './grafana/prometheus/rules:/etc/prometheus/rules'
    labels:
      - 'traefik.enable=true'
      - 'traefik.http.routers.prometheus.rule=Host(`prometheus.${SITE}`)'
      - 'traefik.http.services.prometheus.loadbalancer.server.port=9090'
      - 'traefik.http.routers.prometheus.middlewares=basic_auth@docker'

  node_exporter:
    image: prom/node-exporter:v1.0.1
    restart: always
    labels:
      - 'traefik.enable=true'
      - 'traefik.http.routers.node_exporter.rule=Host(`node_exporter.${SITE}`)'
      - 'traefik.http.services.node_exporter.loadbalancer.server.port=9100'
      - 'traefik.http.routers.node_exporter.middlewares=basic_auth@docker'
    networks:
      - 'srv'

  alertmanager:
    image: prom/alertmanager:v0.21.0
    networks:
      - 'srv'
    labels:
      - 'traefik.enable=true'
      - 'traefik.http.routers.alertmanager.rule=Host(`alertmanager.${SITE}`)'
      - 'traefik.http.services.alertmanager.loadbalancer.server.port=9093'
      - 'traefik.http.routers.alertmanager.middlewares=basic_auth@docker'
    restart: always

  cadvisor:
    image: gcr.io/google-containers/cadvisor:v0.36.0
    volumes:
    - '/:/rootfs:ro'
    - '/var/run:/var/run:rw'
    - '/sys:/sys:ro'
    - '/var/lib/docker/:/var/lib/docker:ro'
    networks:
      - 'srv'
    restart: always
    labels:
      - 'traefik.enable=true'
      - 'traefik.http.routers.cadvisor.rule=Host(`cadvisor.${SITE}`)'
      - 'traefik.http.services.cadvisor.loadbalancer.server.port=8080'
      - 'traefik.http.routers.cadvisor.middlewares=basic_auth@docker'