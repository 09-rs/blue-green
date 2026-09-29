# Blue-Green Deployment on AWS EC2

## Overview

This project demonstrates a Blue-Green deployment strategy using AWS EC2, Docker, and Nginx.

Two application environments are maintained simultaneously:

- Blue — Version 1
- Green — Version 2

Nginx acts as the traffic router and directs production traffic to either environment.

## Architecture

```text
                    AWS EC2
                       |
                    Port 80
                       |
                +--------------+
                |     Nginx    |
                | Traffic Router|
                +------+-------+
                       |
              +--------+--------+
              |                 |
          Blue :8081        Green :8082
          Version 1         Version 2
Containers
Container	Purpose	Port
blue-app	Blue environment	8081
green-app	Green environment	8082
traffic-router	Production traffic router	80
Blue Environment
BLUE ENVIRONMENT - Version 1
Green Environment
GREEN ENVIRONMENT - Version 2
Deployment Process

Initially, production traffic is routed to Blue.

Client → Nginx → Blue

The Green environment is then deployed and tested independently.

Traffic is switched to Green by changing the Nginx upstream configuration.

Client → Nginx → Green

Blue remains running during the deployment.

Rollback

If the Green deployment needs to be rolled back, traffic can be redirected to Blue.

Client → Nginx → Blue

This allows rollback without rebuilding or redeploying the Blue environment.

Verification

Blue:

curl http://localhost:8081

Green:

curl http://localhost:8082

Production traffic:

curl http://localhost

Container status:

docker ps
Technologies Used
AWS EC2
Ubuntu
Docker
Nginx
Linux
Bash
Blue-Green Deployment Strategy
Result

Successfully demonstrated:

Blue environment deployment
Green environment deployment
Production traffic routing
Blue → Green traffic switch
Green → Blue rollback
Both environments running simultane

