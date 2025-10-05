## Services

The Services page displays the current status of EPMware background services and allows administrators to start or stop them as needed.

![Services Page](../assets/images/administration/services-page.png)<br/>
*Services status and control panel*

### Available Services

| Service | Purpose | Status | Actions |
|---------|---------|--------|---------|
| **Workflow Service** | Processes workflow tasks and transitions | Running/Stopped | Start/Stop |
| **Deployment Service** | Executes metadata deployments | Running/Stopped | Start/Stop |
| **ERP Import Service** | Processes ERP data imports | Running/Stopped | Start/Stop |
| **Email Service** | Sends notifications | Running/Stopped | Start/Stop |
| **Scheduler Service** | Manages scheduled jobs | Running/Stopped | Start/Stop |

### Service Management

#### Starting Services

1. Navigate to **Administration → Services**
2. Identify stopped services (red status)
3. Click **Start** button for service
4. Wait for status to change to "Running"
5. Verify in service log

#### Stopping Services

1. Check for active processes
2. Click **Stop** button
3. Confirm stop action
4. Wait for graceful shutdown
5. Status changes to "Stopped"

!!! warning "Service Dependencies"
    Some services depend on others. For example, Deployment Service requires Workflow Service to be running.

### Service Configuration

Service parameters are configured in Global Settings:

| Setting | Default | Description |
|---------|---------|-------------|
| **Workflow Service Sleep Interval** | 5 seconds | Check frequency for new tasks |
| **Deployment Service Sleep Interval** | 5 seconds | Check frequency for deployments |
| **ERP Import Service Sleep Interval** | 5 seconds | Check frequency for imports |

### Service Monitoring

Monitor service health through:
- Status indicators on Services page
- Service logs in Administration → Logs
- System alerts for service failures
- Performance metrics dashboard

---
