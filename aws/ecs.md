# 主要放些 Elastic Container Service (ECS) 相關的筆記

## 怎麼 debug ecs container 問題
1. 首先可以先創建一個臨時的 container 出來用
```bash
aws ecs run-task \
  --profile "<profile_name>" \
  --region "<region_name>" \
  --cluster "<cluster_name>" \
  --task-definition "<task_definition>" \
  --launch-type FARGATE \
  --enable-execute-command \
  --network-configuration "awsvpcConfiguration={subnets=["<subnet_name>"],securityGroups=["<security_group>"],assignPublicIp=ENABLED}"
```
2. 那接著就可以用 execute-command 來進入 container 裡面
```bash
aws ecs execute-command \
    --profile "<profile_name>" \
    --region "<region_name>" \
    --cluster "<cluster_name>" \
    --task "<task_id>" \
    --container "<container_name>" \
    --interactive \
    --command "/bin/sh"
```
3. 接著你就可以在 container 裡面去做 debug 了
