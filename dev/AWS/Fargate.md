# AWS Fargate

## What's this

- An ECS mechanism to allow container execution without the need of managing servers and clusters.

- Basically a AWS Lambda, but for containers.

## How do I do that

1. **Create a cluster** (or use the *default* one)

   - A cluster with a unique name can be created with the following command: `aws ecs create-clister --cluster-name-here fargate cluster`
   - Executing the command should make us recieve a similar output:

    ```js
        {
        "cluster": {
            "status": "ACTIVE",
            "statistics": [],
            "clusterName": "fargate-cluster",
            "registeredContainerInstancesCount": 0,
            "pendingTasksCount": 0,
            "runningTasksCount": 0,
            "activeServicesCount": 0,
            "clusterArn": "arn:aws:ecs:region:aws_account_id:cluster/fargate-cluster"
        }
    }
    ```

2. **Set up a Task Definition**

    - A Task Definition describes the container and it's volumes for a task in Amazon ECS.

    - We specify here which images to use, the nedded resources and other configurations.

    - It's completely **required** to run Docker containers inside Amazon ECS.

    - We can set up the definition with something of the like:

    ```js
    {
        "family": "sample-fargate",
        "networkMode": "awsvpc",
        "containerDefinitions": [
            {
                "name": "fargate-app",
                "image": "httpd:2.4",
                "portMappings": [
                    {
                        "containerPort": 80,
                        "hostPort": 80,
                        "protocol": "tcp"
                    }
                ],
                "essential": true,
                "entryPoint": [
                    "sh","-c"
                ],
                "command": [
                    "/bin/sh -c \"echo '<html> <head> <title>Amazon ECS Sample App</title> <style>body {margin-top: 40px; background-color: #333;} </style> </head><body> <div style=color:white;text-align:center> <h1>Amazon ECS Sample App</h1> <h2>Congratulations!</h2> <p>Your application is now running on a container in Amazon ECS.</p> </div></body></html>' >  /usr/local/apache2/htdocs/index.html && httpd-foreground\""
                ]
            }
        ],
        "requiresCompatibilities": [
            "FARGATE"
        ],
        "cpu": "256",
        "memory": "512"
    }
    ```

   - A similar JSON as the above can be passed to the AWS CLI as easy as the command:

    ```bash
    aws ecs register-task-definition --cli-input-json file://$HOME/tasks/fargate-task.json
    ```

3. **Check if everything went well**

    - You can check the set up Task Definition anytime with a:

    ```bash
    aws ecs list-task-definitions
    ```

4. **Create a Service**

    - An ECS Service is a mechanism the allows us to run and mantain and specific number of instances of a Task Definition simultaneosly in an ECS Cluster.

    - If any of our tasks fail or something, the ECS Service scheduler is responsible for launching another instance as to replace it and mantain the desired number of tasks executing the same time.

    - We can also run a service behind a **load balancer**.

    - A Service for **Fargate Tasks** always presents the **REPLICA scheduler strategy**, that maintains the desired number of tasks across our cluster.

    - We can create a Service for a previously set up **Task Definition**, with two instances for example, with the command:

    ```bash
    aws ecs create-service --cluster fargate-cluster --service-name fargate-service --task-definition sample-fargate:1 --desired-count 2 --launch-type "FARGATE" --network-configuration "awsvpcConfiguration={subnets=[subnet-abcd1234],securityGroups=[sg-abcd1234]}"
    ```

5. **Check things again**

    - We can list our set up services with the command:

    ```bash
    aws ecs list-services --cluster fargate-cluster
    ```

## Is it going to empty my pockets

- Maybe, it can be pretty pricy depending on your needs.

- The price depends on the **sum** of the CPU and Memory usage

  - **CPU cost** =  (n° of tasks) x (n° of vCPUS) x (vCPU cost per second) x (vCPU usage, in secs, per day) x (n° of days)

  - **Memory cost** = (n° of tasks) x (memory in GB) x (price per GB per second) x (memory usage, in secs, per day) x (n° of days)

  > The prices of the vCPU and Memory by second (billable by the our) are different for each AWS configured region

- Do your math.
