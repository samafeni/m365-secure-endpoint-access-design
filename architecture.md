# Endpoint Security Architecture

---

## Overview

This document captures an anonymised architectural view of an identity-first endpoint security design used to control access to Microsoft 365 workloads. The structure and decision-making approach reflect a real-world implementation, with organisational identifiers and environment-specific details intentionally removed.

The architecture focuses on how authentication context, device posture, and risk telemetry combine to support adaptive access decisions. Rather than concentrating enforcement within a single technology layer, responsibility is distributed across identity, endpoint management, threat detection, and policy evaluation.

Microsoft Entra ID operates as the central Zero Trust control point, while Microsoft Intune and Microsoft Defender for Endpoint provide continuous signals consumed during Conditional Access evaluation.

---

## Architecture Diagram

![Endpoint Secure Access Architecture](diagrams/endpoint-architecture.gif)

The diagram represents a simplified structural view of the environment, illustrating how identity, device management, and security signals converge before access to Microsoft 365 workloads is granted.

---

## Architectural Principles

Several design principles shaped the architecture:

* **Identity-First Security**
  Access decisions originate from Microsoft Entra ID rather than network location or individual application configuration.

* **Continuous Evaluation**
  Device compliance and risk telemetry are assessed dynamically during authentication instead of enforced through static trust assumptions.

* **Layered Enforcement**
  Endpoint management, threat intelligence, and Conditional Access policies operate together to minimise dependency on any single control.

* **Operational Visibility**
  Monitoring and telemetry flows remain embedded within the design to support ongoing policy refinement and incident awareness.

---

## Access Request and Context Collection

When a user attempts to access a Microsoft 365 workload such as Teams, SharePoint, or Exchange Online, authentication is processed through Microsoft Entra ID. During this stage, contextual attributes are evaluated, including:

* User identity and group membership
* Device registration and management state
* Client application and authentication method
* Network or location signals where applicable

These attributes form the basis for Conditional Access policy evaluation.

---

## Identity Layer — Zero Trust Control Point

Microsoft Entra ID serves as the central decision authority within the architecture. All authentication requests pass through this layer before tokens are issued to workloads.

Core responsibilities include:

* Identity authentication and token issuance
* Conditional Access policy evaluation
* Aggregation of compliance and risk signals
* Sign-in logging and audit telemetry

Positioning identity as the primary control plane reduces reliance on traditional perimeter-based security models.

---

## Device Management Signals — Microsoft Intune

Microsoft Intune contributes device posture signals used during access evaluation.

Compliance policies establish baseline expectations for managed endpoints, including:

* Encryption and security configuration alignment
* Supported operating system posture
* Device health and configuration status

Rather than acting as a direct enforcement mechanism, Intune provides a **compliance state signal** that Conditional Access policies consume. This separation preserves architectural clarity between management and enforcement layers.

---

## Risk Telemetry — Microsoft Defender for Endpoint

Microsoft Defender for Endpoint introduces additional context through device risk signals.

These signals represent the evolving security posture of endpoints, including threat indicators or behavioural anomalies. Integrating risk telemetry enables Conditional Access policies to respond dynamically to changes in device trust.

Risk data informs policy decisions but does not independently enforce access restrictions.

---

## Policy Enforcement — Conditional Access

Conditional Access functions as the policy engine translating identity, compliance, and risk signals into access outcomes.

Policies evaluate multiple conditions simultaneously, including:

* Device compliance state from Intune
* Device risk level from Defender for Endpoint
* Authentication strength requirements
* Session control enforcement

Based on the combined evaluation, access may be granted fully, restricted through limited sessions, or blocked entirely. This layered enforcement approach aligns with Zero Trust principles by adapting decisions to real-time context.

---

## Managed vs Unmanaged Device Paths

The architecture differentiates between corporate-managed endpoints and unmanaged or personal devices.

* **Corporate Managed Endpoints**
  Devices onboarded through Windows Autopilot and Intune follow a structured lifecycle. Compliance and risk signals allow these endpoints to satisfy policy requirements and receive full access where appropriate.

* **Unmanaged or BYOD Devices**
  Personal or unknown devices follow a constrained access path. Conditional Access policies enforce browser-based or reduced-privilege sessions to maintain productivity while preserving security boundaries.

---

## Monitoring and Telemetry

Operational visibility is maintained through aggregated telemetry across identity, management, and security platforms.

Typical monitoring signals include:

* Entra ID sign-in logs and audit events
* Intune compliance reporting
* Defender for Endpoint alerts and device risk insights

Embedding monitoring into the architecture reinforces the idea that secure access is a continuous operational process rather than a one-time configuration.

---

## Relationship to Conditional Access Decision Flow

While this diagram presents the structural architecture, the Conditional Access Decision Flow diagram illustrates the logical evaluation process behind policy enforcement.

Together, they provide complementary perspectives:

* **Architecture View** — component interaction and signal flow
* **Decision Flow View** — policy logic and access outcomes

Maintaining this separation helps preserve clarity between system design and enforcement behaviour.

---

## Summary

This endpoint security architecture reflects a modern, identity-centric approach to securing Microsoft 365 environments. By combining Microsoft Entra ID, Intune, Defender for Endpoint, and Conditional Access into a unified model, access decisions become adaptive and context-aware.

Rather than enforcing rigid network boundaries, the design prioritises identity verification, device posture, and risk awareness, supporting secure collaboration while maintaining operational flexibility.
