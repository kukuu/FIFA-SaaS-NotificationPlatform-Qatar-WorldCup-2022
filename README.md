# FIFA SaaS Notification Platform: Qatar World Cup - 2022

As Head of Engineering for the FIFA World Cup 2022, I spearheaded the development of a scalable SaaS notification platform to enhance global fan engagement. The system delivered real-time updates (match alerts, promotions, and interactive content) via push notifications (text, carousel, video), leveraging a microservices architecture on AWS (Lambda, Kinesis, RDS/PostgreSQL). Event-driven data pipelines used Kafka for high-throughput messaging, while GraphQL (Apollo Server) and React/Redux powered the admin portal for dynamic content scheduling and segmentation. Notifications supported iOS/Android with optimized media (compressed PNGs/MP4s) and adhered to strict UX guidelines (e.g., 400x100px banners, 9:19 video aspect ratios).

The platform's content management system was designed to support multiple notification types, each optimized for performance and user engagement. Standard notifications included text-based alerts (title, subtitle, message) and image notifications (400x100px PNGs @300ppi, compressed via TinyPNG). For richer interactions, carousel notifications allowed up to 500kb PNGs (680x550px), dynamically loaded via a React-based admin UI. Video notifications leveraged MP4 footage (540x1140px, 9:19 aspect ratio) with embedded buttons for CTAs, timed using a scrubber in the Video Builder. All media was stored in S3, with CloudFront CDN ensuring low-latency global delivery.

The platform prioritized reliability and observability, integrating Sentry for error tracking, Prometheus/Grafana for monitoring, and SonarCloud for code quality. Development followed TDD/CI/CD practices via Dockerized deployments, GitFlow, and JIRA-managed sprints. My role included aligning stakeholders (e.g., FIFA, vendors) and mentoring engineers to adopt serverless best practices (AWS Lambda, Serverless Framework) for cost efficiency.

## Segmentation and Delivery
The Segment Panel enabled rule-based targeting (e.g., device type, location) using PostgreSQL for subscriber metadata. Rules (e.g., FIRST_SESSION, LOCATION) were evaluated dynamically via Lambda functions, while the Scheduling Panel supported time-based triggers (Cron expressions). Notifications were routed through Kafka for decoupled processing, with Kinesis handling real-time analytics. The User Explorer provided granular insights (device IDs, engagement history) via a GraphQL API, and the Media Library (React + Redux) allowed asset reuse and pruning.

## Architecture Overview

[!image]()

![Architecture](https://github.com/kukuu/FIFA-SaaS-NotificationPlatform-Qatar-WC-2022.MD/blob/main/FIFA-Saas-Notification-platform.png)


## Key Workflows

- **Image/Carousel Upload:** Compressed via Lambda (TinyPNG API), validated against pixel specs, and stored in S3 with CloudFront invalidation.

- **Video Processing:** FFmpeg Lambda transcoded uploads to 25fps MP4s; buttons timed via scrubber metadata in DynamoDB.

- **Dynamic Segmentation:** Rules (e.g., LOCATION) evaluated at send-time via Lambda, reducing PostgreSQL load.

- **Monitoring:** SonarCloud (code quality), Sentry (errors), Prometheus (throughput), Slack alerts.
