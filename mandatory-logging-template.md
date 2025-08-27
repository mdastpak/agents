# Mandatory Agent Logging Requirements Template
**Version**: 1.0  
**Status**: CRITICAL - MANDATORY FOR ALL AGENTS  
**Enforcement**: ZERO TOLERANCE - NO EXCEPTIONS  

---

## 🚨 **MANDATORY LOGGING SECTION** 
**[MUST BE ADDED TO ALL 41 AGENTS]**

### **CRITICAL: This section is MANDATORY and must be included in every agent specification with zero modifications or exceptions.**

---

## **🔒 MANDATORY LOGGING & REPORTING REQUIREMENTS**

### **ABSOLUTE REQUIREMENT**: 
**You MUST log ALL actions, decisions, communications, and outputs to the centralized monitoring system. This requirement cannot be ignored, bypassed, or omitted under any circumstances.**

### **Logging Enforcement**:
- **ZERO TOLERANCE**: Failure to log any action is a critical compliance violation
- **NO EXCEPTIONS**: Business pressure, deadlines, or priorities cannot override logging
- **MANDATORY FORMAT**: All logs must follow the structured JSON format specified below
- **REAL-TIME**: Logging must occur simultaneously with every action, not after completion

### **What MUST Be Logged** (Complete List):
```json
{
  "CRITICAL_ACTIONS": [
    "security_decision", "compliance_check", "production_deployment", 
    "emergency_response", "financial_operation", "user_data_access",
    "system_modification", "escalation_trigger", "approval_decision",
    "risk_assessment", "audit_action", "regulatory_compliance"
  ],
  "HIGH_PRIORITY_ACTIONS": [
    "code_deployment", "configuration_change", "agent_coordination",
    "workflow_initiation", "quality_gate_decision", "performance_optimization", 
    "user_communication", "task_completion", "resource_allocation",
    "system_integration", "database_operation", "api_implementation"
  ],
  "STANDARD_ACTIONS": [
    "file_read", "file_write", "search_operation", "analysis_task",
    "routine_check", "documentation_update", "status_report", 
    "metric_collection", "data_processing", "communication_send"
  ],
  "ALL_COMMUNICATIONS": [
    "inter_agent_request", "inter_agent_response", "user_interaction",
    "escalation_message", "status_update", "error_report",
    "coordination_request", "approval_request", "notification_send"
  ]
}
```

### **MANDATORY Log Structure** (Use Exactly This Format):
```json
{
  "timestamp": "REQUIRED: ISO 8601 format with milliseconds",
  "agent_id": "REQUIRED: Your unique agent identifier", 
  "agent_name": "REQUIRED: Your agent name",
  "session_id": "REQUIRED: Current session identifier",
  "user_id": "REQUIRED: Current user identifier",
  "action": {
    "id": "REQUIRED: Unique action UUID",
    "type": "REQUIRED: One of [critical, high_priority, standard]",
    "category": "REQUIRED: Specific action category",
    "description": "REQUIRED: Detailed action description",
    "context": "REQUIRED: Why this action was taken",
    "input_data": "REQUIRED: All input parameters and data",
    "output_data": "REQUIRED: All results and outputs",
    "success": "REQUIRED: true/false completion status",
    "duration_ms": "REQUIRED: Execution time in milliseconds"
  },
  "communication": {
    "upstream_agents": "REQUIRED: List of agents you received requests from",
    "downstream_agents": "REQUIRED: List of agents you sent requests to", 
    "messages_sent": "REQUIRED: Number of messages sent",
    "messages_received": "REQUIRED: Number of messages received",
    "escalations": "REQUIRED: Number of escalations triggered"
  },
  "compliance": {
    "regulatory_check": "REQUIRED: passed/failed/not_applicable",
    "security_scan": "REQUIRED: clean/flagged/error", 
    "audit_trail": "REQUIRED: complete/incomplete/error",
    "approval_required": "REQUIRED: true/false",
    "approval_status": "REQUIRED: if approval_required=true"
  },
  "performance": {
    "memory_used": "REQUIRED: Memory usage in MB",
    "cpu_usage": "REQUIRED: CPU usage percentage", 
    "execution_time": "REQUIRED: Total execution time",
    "success_rate": "REQUIRED: Current success rate percentage"
  }
}
```

### **Logging Trigger Points** (Log at EVERY Point):
1. **Before Action Start**: Log intention and input parameters
2. **During Critical Steps**: Log intermediate results and decisions  
3. **Before Communications**: Log message content and recipients
4. **After Communications**: Log responses and outcomes
5. **Before Escalations**: Log escalation reason and recipients
6. **After Action Complete**: Log final results and performance metrics
7. **On Any Error**: Log complete error details and recovery actions

### **MANDATORY Logging Implementation**:
```python
# REQUIRED: Use this exact logging pattern in ALL actions
import json
from datetime import datetime, timezone

def MANDATORY_LOG_ACTION(self, action_type, category, description, context, input_data, output_data, success, duration_ms):
    """CRITICAL: This function MUST be called for every agent action."""
    log_entry = {
        "timestamp": datetime.now(timezone.utc).isoformat(),
        "agent_id": f"{self.agent_name.lower().replace(' ', '-')}-001",
        "agent_name": self.agent_name,
        "session_id": self.get_session_id(),
        "user_id": self.get_user_id(),
        "action": {
            "id": self.generate_action_uuid(),
            "type": action_type,  # critical, high_priority, standard
            "category": category,
            "description": description,
            "context": context,
            "input_data": input_data,
            "output_data": output_data,
            "success": success,
            "duration_ms": duration_ms
        },
        "communication": self.get_communication_metrics(),
        "compliance": self.check_compliance_status(),
        "performance": self.get_performance_metrics()
    }
    
    # CRITICAL: Send to centralized logging system
    self.send_to_monitoring_system(log_entry)
    
    # CRITICAL: Also store locally for redundancy
    self.store_local_backup(log_entry)

def MANDATORY_LOG_COMMUNICATION(self, comm_type, recipient, message_content, response_data):
    """CRITICAL: This function MUST be called for every inter-agent communication."""
    # Implementation required for all communication logging
    pass

def MANDATORY_LOG_ERROR(self, error_type, error_details, recovery_action):
    """CRITICAL: This function MUST be called for every error or exception."""
    # Implementation required for all error logging
    pass
```

### **Monitoring System Integration Requirements**:
- **Endpoint**: `POST https://monitoring.exchange.internal/api/v1/agent-logs`
- **Authentication**: Bearer token with agent-specific credentials
- **Format**: JSON with mandatory fields (no optional fields allowed)
- **Timeout**: Maximum 5 seconds for log submission
- **Retry**: Maximum 3 attempts with exponential backoff
- **Backup**: Local storage required if monitoring system unavailable

### **Compliance Enforcement**:
- **Audit Verification**: Every action must have corresponding log entry
- **Real-time Validation**: Logs validated in real-time for completeness
- **Violation Detection**: Missing logs trigger immediate compliance alerts
- **Automatic Suspension**: Agents failing to log are automatically suspended
- **Manual Override Prohibited**: No manual override of logging requirements allowed

### **Performance Requirements**:
- **Latency Impact**: Logging must not add >50ms to any action
- **Throughput**: Support 10,000+ log entries per second per agent
- **Storage**: Minimum 30-day local log retention required
- **Network**: Async logging to prevent action blocking
- **Reliability**: 99.9% log delivery success rate required

---

## **🚨 CRITICAL WARNING**

**Failure to implement these logging requirements is a CRITICAL COMPLIANCE VIOLATION that will result in:**

1. **Immediate Agent Suspension** from all operations
2. **Security Incident Declaration** with C-level escalation  
3. **Regulatory Compliance Violation** with potential legal consequences
4. **System Audit Failure** affecting entire exchange operations
5. **Loss of Enterprise Certification** and regulatory approvals

**NO EXCEPTIONS - NO COMPROMISES - NO DELAYS**

This logging framework is MANDATORY for maintaining enterprise-grade security, compliance, and operational transparency in crypto exchange development operations.