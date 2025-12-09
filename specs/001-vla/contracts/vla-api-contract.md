# VLA Model API Contract

**Version**: 1.0
**Date**: 2025-12-08
**Feature**: 001-vla

## Overview

This contract defines the API interface for Vision-Language-Action (VLA) models in humanoid robotics applications. It specifies the expected inputs, outputs, and behavior of VLA model implementations.

## API Endpoints

### 1. Process Command
**Endpoint**: `POST /vla/process_command`

**Description**: Process a visual observation and language command to generate a robotic action.

**Request Body**:
```json
{
  "visual_observation": {
    "image_data": "base64_encoded_image",
    "camera_intrinsics": {
      "fx": 525.0,
      "fy": 525.0,
      "cx": 319.5,
      "cy": 239.5
    }
  },
  "language_command": "Pick up the red cup from the table",
  "robot_state": {
    "joint_positions": [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0],
    "end_effector_pose": {
      "position": {"x": 0.5, "y": 0.0, "z": 0.2},
      "orientation": {"x": 0.0, "y": 0.0, "z": 0.0, "w": 1.0}
    }
  },
  "task_context": {
    "task_name": "object_manipulation",
    "priority": 1
  }
}
```

**Response**:
```json
{
  "action": {
    "type": "joint_position",
    "values": [0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7],
    "duration": 2.5,
    "confidence": 0.85
  },
  "predicted_trajectory": [
    {"joint_positions": [0.05, 0.1, 0.15, 0.2, 0.25, 0.3, 0.35], "timestamp": "2025-12-08T10:00:00Z"},
    {"joint_positions": [0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7], "timestamp": "2025-12-08T10:00:02Z"}
  ],
  "success": true,
  "execution_time_ms": 120
}
```

**Error Response**:
```json
{
  "error": {
    "code": "INVALID_INPUT",
    "message": "Language command is ambiguous or unclear",
    "details": "Command contains unclear references to objects"
  },
  "success": false
}
```

### 2. Model Status
**Endpoint**: `GET /vla/status`

**Description**: Get the current status of the VLA model.

**Response**:
```json
{
  "model_name": "RT-2",
  "version": "1.0.0",
  "status": "ready",
  "last_updated": "2025-12-08T09:00:00Z",
  "supported_tasks": ["grasping", "navigation", "manipulation"],
  "performance_metrics": {
    "success_rate": 0.85,
    "avg_inference_time_ms": 150
  }
}
```

## Data Schemas

### VisualObservation
- `image_data`: string (base64 encoded image data)
- `format`: string (image format, e.g., "rgb8", "bgr8", "gray8")
- `width`: integer (image width in pixels)
- `height`: integer (image height in pixels)
- `camera_intrinsics`: object (camera intrinsic parameters)
- `timestamp`: string (ISO 8601 formatted timestamp)

### LanguageCommand
- `text`: string (the natural language command)
- `language`: string (language code, e.g., "en", "de")
- `confidence_threshold`: float (minimum confidence required, 0.0-1.0)

### RobotAction
- `type`: string ("joint_position", "cartesian_velocity", "discrete_command")
- `values`: array (action values)
- `duration`: float (expected execution time in seconds)
- `constraints`: array (execution constraints)
- `confidence`: float (confidence in the action, 0.0-1.0)

## Error Codes

| Code | Description | HTTP Status |
|------|-------------|-------------|
| `INVALID_INPUT` | Input data is malformed or invalid | 400 |
| `AMBIGUOUS_COMMAND` | Language command is unclear or ambiguous | 400 |
| `VISUAL_UNCERTAINTY` | Visual input is unclear for action planning | 400 |
| `MODEL_UNAVAILABLE` | VLA model is not currently available | 503 |
| `EXECUTION_FAILED` | Action execution failed | 500 |

## Performance Requirements

- **Inference Time**: Must complete within 500ms for 95% of requests
- **Success Rate**: Should maintain >80% task success rate on benchmark tasks
- **Memory Usage**: Should not exceed 4GB RAM during inference
- **Reliability**: Should maintain 99% uptime during operational hours

## Security Considerations

- Input validation for all command strings to prevent injection attacks
- Authentication required for all API endpoints
- Rate limiting to prevent service overload
- Encryption of sensitive data in transit

## Versioning

This API follows semantic versioning (MAJOR.MINOR.PATCH):
- MAJOR: Breaking changes to the API contract
- MINOR: Backward-compatible additions
- PATCH: Backward-compatible bug fixes