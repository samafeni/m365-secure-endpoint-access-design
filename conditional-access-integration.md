
# Conditional Access Integration

---

## Overview

This document describes how Conditional Access is integrated into the endpoint security architecture to enforce identity-driven access control. Rather than acting as an isolated feature, Conditional Access functions as the policy engine that evaluates authentication context, device posture, and risk telemetry before granting access to Microsoft 365 workloads.

The design aligns with Zero Trust principles by ensuring that access decisions are adaptive and continuously evaluated instead of relying on static trust assumptions.

---

## Role of Conditional Access in the Architecture

Within the overall architecture, Conditional Access sits between identity authentication and workload access. Microsoft Entra ID authenticates the user and collects contextual signals, while Conditional Access evaluates whether the authentication attempt satisfies defined security requirements.

This integration allows policy enforcement to remain centralised and consistent across services such as Teams, SharePoint, and Exchange Online.

Conditional Access does not replace endpoint management or threat protection platforms. Instead, it consumes signals from those platforms and translates them into access outcomes.

---

## Policy Design Approach

Policies were designed using a layered model that prioritises clarity and maintainability.

Key design considerations included:

* Policies should be easy to understand and audit
* Requirements should reflect real operational risk rather than theoretical threats
* Enforcement should be gradual to avoid disrupting users during rollout

Rather than creating many small overlapping policies, the design emphasised a smaller number of clearly defined access scenarios.

---

## Signal Integration

Conditional Access evaluates multiple signals simultaneously during authentication.

### Identity Signals

Identity-based context originates from Microsoft Entra ID and includes:

* User identity and group membership
* Authentication method and strength
* Sign-in behaviour where risk evaluation is enabled

Identity remains the primary control plane, ensuring that enforcement decisions begin with authentication context.

### Device Compliance Signals

Microsoft Intune provides compliance posture information used during policy evaluation.

Conditional Access can require devices to be marked compliant before granting access to sensitive workloads. This ensures that endpoint configuration aligns with organisational security expectations.

### Device Risk Signals

Microsoft Defender for Endpoint contributes device risk telemetry that enhances access evaluation.

Risk signals allow policies to respond to emerging threats dynamically. Devices with elevated risk may trigger additional requirements or restricted access paths depending on policy design.

---

## Access Outcomes

Policies are structured to produce one of three outcomes:

* **Allow** — Access is granted when all requirements are satisfied.
* **Limited Session** — Access is permitted under controlled conditions, typically for unmanaged or unknown devices.
* **Block** — Access is denied when risk or posture requirements are not met.

This layered outcome model reflects a Zero Trust mindset where access is adjusted based on context rather than granted universally.

---

## Managed vs Unmanaged Access Paths

A deliberate distinction exists between corporate-managed endpoints and unmanaged devices.

### Managed Endpoints

Devices enrolled through Intune and meeting compliance requirements are eligible for full access when authentication conditions are satisfied. Policy enforcement remains largely transparent to users, allowing productivity without compromising security posture.

### Unmanaged Devices

Personal or unregistered devices are routed through a restricted access path. Policies may enforce browser-based sessions or additional controls to minimise data exposure while still allowing limited collaboration.

This separation ensures that the architecture supports flexible working patterns without weakening overall security.

---

## Policy Evaluation Flow

The Conditional Access decision flow diagram illustrates how signals combine during authentication:

1. A user initiates an access request.
2. Microsoft Entra ID authenticates the identity and gathers context.
3. Conditional Access evaluates applicable policies.
4. Device compliance and risk signals are assessed.
5. Access is allowed, restricted, or blocked based on the combined evaluation.

By separating structural architecture from decision logic, the design maintains clarity between system components and policy behaviour.

---

## Operational Considerations

From an operational standpoint, Conditional Access policies were implemented gradually to reduce disruption.

Key considerations included:

* Monitoring sign-in logs during early deployment phases
* Starting with report-only mode to validate policy impact
* Communicating policy expectations clearly to users and support teams

This phased approach allowed the organisation to strengthen security posture without creating sudden changes in user experience.

---

## Relationship to Other Design Documents

Conditional Access integration builds on several other design areas:

* Device compliance design provides posture signals used during evaluation.
* Defender for Endpoint integration introduces risk-based context.
* Enrollment strategy ensures that managed endpoints can meet policy requirements.

Together, these components form a cohesive enforcement model aligned with identity-first security.

---

## Summary

Conditional Access acts as the central enforcement layer that brings together identity, device posture, and risk telemetry. By integrating signals from Microsoft Intune and Microsoft Defender for Endpoint into Microsoft Entra ID authentication workflows, the architecture enables adaptive access decisions that evolve alongside user behaviour and device health.

This integration supports a modern Zero Trust approach where trust is continuously evaluated, and access reflects real-time context rather than static assumptions.
