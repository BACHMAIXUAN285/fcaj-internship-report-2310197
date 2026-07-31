---
title: "Triển Khai Hệ Thống"
date: 2026-07-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

Sau khi hoàn thành giai đoạn phát triển và đóng gói ứng dụng bằng công nghệ containerization (Docker), hệ thống **MedFlow** được triển khai lên hạ tầng điện toán đám mây Amazon Web Services (AWS). Mô hình triển khai hướng tới mục tiêu đảm bảo tính sẵn sàng cao (High Availability), khả năng mở rộng linh hoạt (Scalability), an toàn bảo mật và tối ưu hóa chi phí vận hành.

---

### Thiết Kế Kiến Trúc Hạ Tầng Triển Khai

#### Sơ đồ kiến trúc hạ tầng (Deployment Architecture)

Hệ thống ứng dụng mô hình container đa dịch vụ (multi-container) vận hành dưới dạng Serverless trên AWS ECS Fargate, kết hợp với Application Load Balancer để đón traffic từ Internet.

```mermaid
flowchart TD
    Client[Internet / End Users] -->|HTTP:80 / HTTPS:443| ALB[Application Load Balancer\nInternet-facing]
    
    subgraph AWS_VPC [AWS VPC - Default / Custom]
        ALB -->|Forward to Target Group\nHTTP:3000| TG[Target Group: medflow-client-tg\nType: IP, Health Check /]
        
        subgraph ECS_Cluster [AWS ECS Cluster]
            subgraph Fargate_Task [ECS Task: medflow-task\nLaunch Type: Fargate]
                Frontend[Container 1: medflow-client\nNext.js - Port 3000]
                Backend[Container 2: medflow-server\nNestJS - Port 4000]
                
                Frontend <-->|Localhost / 127.0.0.1| Backend
            end
        end
        
        TG -->|Direct Traffic| Frontend
    end

    subgraph AWS_Services [AWS Supporting Services]
        ECR_Client[(AWS ECR\nmedflow-client)] -.->|Pull Image| Frontend
        ECR_Server[(AWS ECR\nmedflow-server)] -.->|Pull Image| Backend
        Backend -.->|Store Logs| CW[AWS CloudWatch Logs]
    end