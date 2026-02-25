
# Device Compliance Design

---

## Overview

This document outlines the device compliance strategy used within the endpoint security architecture. The goal of the compliance model is not simply to enforce configuration settings, but to provide reliable posture signals that inform Conditional Access decisions.

Rather than treating compliance as a static checklist, the design focuses on maintaining a measurable level of device trust that can be evaluated dynamically during authentication. Microsoft Intune acts as the policy authority for endpoint configuration, while Microsoft Entra ID consumes compliance status as part of identity-driven access enforcement.

---

## Design Objectives

The compliance model was designed around several practical objectives:

* Establish a baseline level of device trust for corporate-managed endpoints
* Provide clear posture signals to Conditional Access policies
* Reduce risk without introducing unnecessary friction for users
* Align security configuration with modern cloud-first device management practices
* Maintain operational simplicity for administrators and support teams

The emphasis throughout the design is consistency and predictability rather than aggressive enforcement that could disrupt productivity.

---

## Compliance as a Signal, Not a Control

A key architectural decision was to treat Intune compliance as a **signal** rather than a direct enforcement mechanism.

Microsoft Intune evaluates device posture against defined compliance policies. The result of that evaluation — compliant or non-compliant — is then consumed by Conditional Access.

This separation provides several advantages:

* Enforcement remains centralised within identity policy
* Compliance logic remains focused on endpoint health
* Policy changes can be implemented without redesigning access controls

By decoupling management from enforcement, the architecture remains flexible and easier to evolve.

---

## Baseline Compliance Requirements

Compliance policies were designed to reflect realistic enterprise expectations without over-engineering.

Typical posture indicators included:

* Encryption enabled on corporate endpoints
* Supported operating system versions
* Security configuration alignment
* Device integrity and health status

The objective was to ensure that devices accessing corporate resources met a minimum security baseline rather than enforcing highly restrictive configuration rules.

---

## Compliance Evaluation Flow

Within the broader architecture, the compliance process follows a structured lifecycle:

1. A device enrolls into Microsoft Intune through modern provisioning.
2. Configuration profiles and security baselines are applied.
3. Compliance policies evaluate device posture continuously.
4. The resulting compliance state is shared with Microsoft Entra ID.
5. Conditional Access policies use this signal during authentication.

This flow ensures that device posture remains dynamic rather than fixed at the time of enrollment.

---

## Integration with Conditional Access

Compliance status plays a critical role in access decisions but is never evaluated in isolation.

Conditional Access policies combine multiple signals:

* Device compliance from Intune
* Device risk from Microsoft Defender for Endpoint
* Authentication context and user identity

This layered approach prevents single-point dependency on compliance alone and enables more adaptive access outcomes.

For example:

* Compliant devices may receive full access to Microsoft 365 workloads.
* Non-compliant devices may be restricted to limited session access or blocked entirely, depending on policy configuration.

---

## Managed Endpoint Expectations

Corporate-managed endpoints are expected to maintain compliance through automated configuration and update policies.

Key considerations included:

* Automated update management to maintain supported OS versions
* Minimal manual user intervention
* Clear remediation paths when devices fall out of compliance

The design prioritised user transparency, allowing compliance enforcement to operate largely in the background.

---

## Handling Non-Compliant Devices

Non-compliance is treated as a recoverable state rather than an immediate failure.

When a device becomes non-compliant:

* Access may be restricted through Conditional Access
* Users receive guidance on remediation steps
* Compliance status updates automatically once issues are resolved

This approach supports both security and usability by encouraging recovery rather than creating permanent blocks.

---

## Operational Considerations

From an operational perspective, the compliance model was designed to remain sustainable over time.

Important considerations included:

* Avoiding excessive policy fragmentation
* Maintaining clear documentation of baseline expectations
* Monitoring compliance trends rather than individual device anomalies

Reports and monitoring dashboards provide visibility into overall device health, enabling proactive adjustments to policy when necessary.

---

## Relationship to the Architecture

Within the broader endpoint security architecture, device compliance acts as one of several trust signals.

* Microsoft Entra ID evaluates identity and policy logic.
* Microsoft Defender for Endpoint contributes risk telemetry.
* Microsoft Intune provides posture validation.

Together, these signals create a layered trust model that aligns with Zero Trust principles.

---

## Summary

The device compliance design focuses on creating reliable, identity-consumable posture signals rather than enforcing rigid endpoint restrictions. By positioning Microsoft Intune as a source of trust signals and integrating compliance into Conditional Access evaluation, the architecture maintains flexibility while supporting strong security outcomes.

This approach enables adaptive access decisions that reflect both device health and real-time risk without introducing unnecessary operational complexity.
